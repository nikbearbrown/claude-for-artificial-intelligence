# Text in Tabular Data

There is a column in the LendingClub file you have been pretending is not there. You profiled it back in Chapter 2, saw it was free text, and quietly set it aside. It is the field where borrowers wrote, in their own words, why they wanted the money — `desc`, or `title`, depending on the vintage [verify against the actual LendingClub file]. A sample, lightly disguised:

> "Debt consolidation — paying off 3 credit cards at 24% APR. Stable job 6 yrs."

> "MEDICAL BILLS!!!!"

> "wedding"

> ""

> "Borrower added on 12/14/13 > I have been a customer with my bank for over a decade and have never missed a payment. This loan would consolidate two high-interest balances into one manageable monthly payment and I am committed to..."

Look at what that column is. It is filthy. Punctuation is inconsistent. Case is all over the place — `MEDICAL BILLS!!!!` shouting next to a lowercase `wedding`. Some entries are a single word; some are empty; some are paragraph-long, and some carry boilerplate the platform stamped in (`Borrower added on...`). It is, by every structural standard from Chapter 6, a mess.

And it carries signal. A borrower who writes a careful, specific paragraph about consolidating high-interest debt is telling you something different from a borrower who writes `wedding` or nothing at all. The *reason* for a loan, and the *care* with which someone explains it, correlate with whether they pay it back [Medium — this is a well-documented finding for LendingClub specifically in several studies; verify the direction and strength on your file]. Drop this column, as most people do because text is annoying, and you throw away predictive signal you cannot recover from the numeric features.

This chapter is about not dropping it. It is about turning dirty text into clean features that sit beside `annual_inc_log` and `dti` in the same model — and about the judgment of deciding whether the text was worth keeping at all.

## First, Decide Whether to Keep It

The research notes call the central artifact here the **text retention versus drop decision**, and the order matters: you decide *whether* the column earns its place before you spend an afternoon engineering features from it. The decision is not "text is always valuable." It is a weighing.

Two cheap diagnostics inform it. First, how much of the column is even populated?

```python
import pandas as pd

df = pd.read_csv("lending_club_clean.csv")
text_col = "desc"  # [verify against the actual LendingClub file]

filled = df[text_col].notna() & (df[text_col].str.strip() != "")
print(f"non-empty: {filled.mean():.1%}")
print(df.loc[filled, text_col].str.len().describe())
```

In many LendingClub vintages the `desc` field is empty for a large fraction of loans [verify against the actual LendingClub file]. That is itself a fact worth modeling — *whether someone wrote a description at all* may be a feature — but it also tempers how much you should invest in the words themselves.

Second, does the populated text show any relationship to the target? A two-minute check: does the default rate differ between borrowers who wrote something and borrowers who left it blank?

```python
print(df.groupby(filled)["default"].mean())
```

If those two numbers differ meaningfully, the column has signal and you keep it. If they are identical and the text is 90% empty, you may honestly choose to drop it and write down why. **That written justification is the deliverable** — not the decision itself. A dropped column with a one-line reason is good data science; a dropped column with no reason is negligence.

A caution sits inside that diagnostic, and it is the most important sentence in the chapter. The fact that the *presence* of a description correlates with default does not mean the *words* do — and the two have wildly different cost. A borrower who bothered to write anything at all may simply be a more engaged borrower, and you can capture that with a single `desc_empty` flag in five lines of code. Engineering five hundred TF-IDF columns to chase signal that turns out to live entirely in "did they write something" is effort spent for nothing, and worse, it inflates your feature count and your overfitting risk. So the retention decision has two layers: does text help at all, and if so, does the *content* help beyond the cheap metadata? Answer them in that order. Many real projects discover the honest answer is "the metadata is most of it," and stop there with a clear conscience and a far simpler model.

There is also a provenance question this column raises that numeric columns rarely do. Free text written by people can contain personal information, names, employer details, even medical specifics — `MEDICAL BILLS!!!!` is the polite version. Before you vectorize, you owe a glance at what is actually in the field and whether feeding it into a model, or worse into an external LLM for summarization, creates a privacy or compliance exposure your numeric features never did. The research notes flag exactly this: using a large language model to label or summarize the text may improve features, but it creates provenance, privacy, and reproducibility questions that a `CountVectorizer` running locally on your laptop does not. That trade-off is not the assistant's call. It is yours.

## Clean Before You Count

Assume the diagnostic said keep. Now clean — and clean *less* aggressively than your instinct wants. Every normalization step erases a distinction, and some distinctions are signal. `MEDICAL BILLS!!!!` in all caps with four exclamation points might genuinely predict differently than a calm lowercase `medical bills`; if you lowercase and strip punctuation reflexively, you have decided that urgency does not matter before checking whether it does.

A reasonable, reversible baseline cleaning:

```python
import re

def clean_text(s: str) -> str:
    if not isinstance(s, str):
        return ""
    s = s.lower()                              # case-fold
    s = re.sub(r"borrower added on .*?>", " ", s)  # strip platform boilerplate [verify]
    s = re.sub(r"[^a-z0-9\s]", " ", s)         # drop punctuation
    s = re.sub(r"\s+", " ", s).strip()         # collapse whitespace
    return s

df["desc_clean"] = df[text_col].apply(clean_text)

# Keep the raw signals you just smoothed away, as separate features:
df["desc_len"]   = df[text_col].fillna("").str.len()
df["desc_caps"]  = df[text_col].fillna("").str.count(r"[A-Z]")
df["desc_bang"]  = df[text_col].fillna("").str.count("!")
df["desc_empty"] = (~filled).astype(int)
```

Notice the move: before lowercasing destroys the capitalization, capture it as `desc_caps`; before stripping punctuation destroys the exclamation marks, capture `desc_bang`. You get the cleaned text *and* the metadata you would otherwise have erased. This is the difference between cleaning text and merely flattening it.

## Bag-of-Words and TF-IDF: Words Become Columns

To put words into a model that expects numbers, you vectorize. The simplest representation is **bag-of-words**: count how often each word appears in each entry, ignoring order. scikit-learn's `CountVectorizer` does this and produces a sparse matrix — one column per word in the vocabulary, one row per loan, mostly zeros.

```python
from sklearn.feature_extraction.text import CountVectorizer

cv = CountVectorizer(
    max_features=500,      # cap the vocabulary; keep the 500 most frequent terms
    stop_words="english",  # drop "the", "and", "to" — frequent and meaningless
    min_df=20,             # ignore terms appearing in fewer than 20 loans
)
X_counts = cv.fit_transform(df["desc_clean"])
print(X_counts.shape)        # (n_loans, ~500)
print(cv.get_feature_names_out()[:20])
```

Raw counts have a problem: common words dominate. The word "loan" appears in nearly every description and therefore distinguishes nothing. **TF-IDF** — term frequency–inverse document frequency — fixes this by down-weighting words that appear everywhere and up-weighting words that are distinctive to particular entries. A word's weight rises with how often it appears in *this* entry and falls with how many entries contain it at all. The logic traces directly to Karen Spärck Jones's 1972 introduction of inverse document frequency. [High — IDF originates with Spärck Jones (1972); the combined TF-IDF weighting is developed in Salton and Buckley (1988).]

```python
from sklearn.feature_extraction.text import TfidfVectorizer

tfidf = TfidfVectorizer(max_features=500, stop_words="english", min_df=20)
X_tfidf = tfidf.fit_transform(df["desc_clean"])
```

[Medium — `CountVectorizer` and `TfidfVectorizer` parameters above are current scikit-learn API; verify against your installed version.]

These features are transparent: you can read the vocabulary and see exactly which words the model leans on. That transparency is a real virtue and a real dispute. Modern embedding models (sentence transformers, LLM embeddings) often predict better by capturing meaning that bag-of-words misses — "credit card debt" and "revolving balances" mean nearly the same thing, but TF-IDF treats them as unrelated columns. The cost is inspectability: an embedding is 384 opaque numbers, and you cannot point at one and say "this is the 'medical' signal." For a credit model that may need to be explained to a regulator, transparent and slightly weaker can beat opaque and slightly stronger. That is a judgment, not a default.

Three vectorizer settings do most of the work, and each is a decision about the world rather than a knob to maximize. `max_features` caps the vocabulary: keep too few terms and you starve the signal, keep too many and most columns are near-empty noise that invites overfitting. `min_df` drops terms that appear in fewer than some number of documents — a word that shows up in three loans cannot generalize, no matter how predictive it looks in those three. And `ngram_range` decides whether you count single words or also short phrases: with `ngram_range=(1, 2)` the vectorizer treats "debt consolidation" as its own feature, not just "debt" and "consolidation" separately. Phrases often carry sharper signal than their component words — "high interest" means something the two words apart do not — but they multiply the vocabulary fast, so pair bigrams with a firmer `min_df`. There is no universally correct setting. Each is tuned against the held-out metric, inside the fold, never by peeking at the test set.

```python
tfidf_bigram = TfidfVectorizer(
    max_features=800, stop_words="english",
    min_df=30, ngram_range=(1, 2),  # unigrams + bigrams
)
```

What the model learned is itself inspectable, and you should inspect it. After fitting, line up each TF-IDF column against the model's coefficient and read the largest positive and largest negative terms. This is not optional polish — it is how you catch a vectorizer that latched onto an artifact. If the single most predictive "word" turns out to be a fragment of the platform's `Borrower added on` boilerplate, or a date token, the model is not reading borrower intent; it is reading a timestamp, and your cleaning step missed it. Reading the top terms is the text-feature equivalent of the histogram in Chapter 8: the diagnostic that tells you whether the feature means what you think it means.

## Putting Text Beside the Tabular Columns

The payoff is combining the text features with the numeric ones in a single model. The clean way is a `ColumnTransformer`, which routes each kind of column to its own preprocessing and concatenates the result.

```python
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LogisticRegression
from sklearn.pipeline import Pipeline

numeric_features = ["annual_inc_log", "dti", "int_rate",
                    "desc_len", "desc_caps", "desc_bang", "desc_empty"]  # [verify]

pre = ColumnTransformer(transformers=[
    ("num",  StandardScaler(), numeric_features),
    ("text", TfidfVectorizer(max_features=500, stop_words="english",
                             min_df=20), "desc_clean"),
])

model = Pipeline(steps=[
    ("pre", pre),
    ("clf", LogisticRegression(max_iter=1000, class_weight="balanced")),
])
```

The `ColumnTransformer` is doing real work here that is easy to underrate. Numeric columns and text columns need entirely different preprocessing — one gets centered and scaled, the other gets tokenized and weighted — and the temptation of a beginner is to vectorize the text in a separate cell, scale the numbers in another, and `hstack` the two matrices by hand. That works once, in a notebook, and then betrays you the moment you need to apply the same transformation to new data, because nothing has recorded the vocabulary, the IDF weights, or the scaler's mean. The `ColumnTransformer` packages all of it into one fitted object that knows how to transform a fresh row exactly the way it transformed the training rows. It is the difference between a sequence of cells that happened to produce a model and an artifact you can actually deploy.

![Routing diagram: a raw table with numeric columns and a dirty desc text column splits into two preprocessing branches — numerics through StandardScaler, the desc text through TfidfVectorizer — which a ColumnTransformer concatenates into one fused feature matrix; the retained text branch is highlighted, and a struck-out path shows that dropping desc loses predictive signal.](images/10-text-in-tabular-data-fig-01.png)

*Figure 10.1 — The `ColumnTransformer` routes numeric and text columns through separate preprocessing and fuses them into one model-ready matrix; the red branch is the text signal most people discard.*

Two things this structure buys you beyond that, and both connect to chapters around it. The `class_weight="balanced"` carries Chapter 9's imbalance handling forward — the text features do not exempt you from the rare-default problem. And wrapping everything in a `Pipeline` means the `TfidfVectorizer` is *fit inside the cross-validation fold*, on training text only. This is the same discipline as the scaler in Chapter 8 and SMOTE in Chapter 9: **the vectorizer learns a vocabulary and IDF weights from the data, which makes it a learned transformation, which means it leaks if you fit it on the full dataset before splitting.** Vectorize first, split second, and the test set's words have contaminated your vocabulary. Chapter 11 makes this the whole subject.

## Before and After

Did the text earn its keep? Compare the model with and without the text block, on a leakage-safe split, using the minority-class metrics from Chapter 9.

```python
from sklearn.model_selection import cross_val_score, StratifiedKFold

cv = StratifiedKFold(5, shuffle=True, random_state=0)

# numeric only
num_only = Pipeline([("sc", StandardScaler()),
                     ("clf", LogisticRegression(max_iter=1000,
                              class_weight="balanced"))])
print("numeric only PR-AUC:",
      cross_val_score(num_only, df[numeric_features], df["default"],
                      cv=cv, scoring="average_precision").mean().round(3))

# numeric + text
print("numeric + text PR-AUC:",
      cross_val_score(model, df, df["default"],
                      cv=cv, scoring="average_precision").mean().round(3))
```

If the text version's PR-AUC is meaningfully higher, you have measured the cost of the convenient drop — the signal you would have thrown away. If it is not, you have *earned* the right to drop the column and a number to justify it. Either outcome is a defensible decision backed by evidence. That is the entire point.

| Pipeline state | Diagnostic | Action | Assumption introduced | Validation check |
|---|---|---|---|---|
| Raw `desc` text | dirty, mixed case, mostly empty [verify] | inspect fill rate + default rate by filled/empty | text *may* carry signal | default rate differs by filled vs. empty |
| Cleaned text | case/punctuation lost in cleaning | capture `len`, `caps`, `bang` before flattening | urgency/effort may be signal | features non-degenerate |
| TF-IDF vectors | common words dominate raw counts | TF-IDF down-weights ubiquitous terms | distinctive words matter more | top-weighted terms are interpretable |
| Combined model | does text help? | compare PR-AUC with vs. without text | text earns its place only if it lifts the metric | leakage-safe CV, vectorizer fit in-fold |

## Exercises: Make the Text Earn Its Place

1. **The drop decision.** Compute the fill rate of the `desc` column and the default rate among filled vs. empty entries. Based only on these two diagnostics, write the one-paragraph justification you would attach to either keeping or dropping the column. State the evidence, then the decision.

2. **Cheap features first.** Before any vectorization, build only the metadata features — description length, count of capital letters, count of exclamation marks, an empty-or-not flag — and fit a model on those plus the numeric columns. How much of the text's signal turns out to live in *how* people wrote rather than *what* they wrote?

3. **Counts vs. TF-IDF.** Vectorize `desc_clean` two ways and compare PR-AUC. Then print the ten highest-weighted TF-IDF terms. Do they make sense as predictors of default? Name one term that surprises you and hypothesize why it carries signal.

4. **Leak it, then fix it.** Fit a `TfidfVectorizer` on the full dataset, then split and evaluate. Now fit it inside the CV fold via the `Pipeline`. Compare the PR-AUC. Explain why the first number is dishonest. (Chapter 11 generalizes this.)

## Bridge

You have now done every local cleaning operation the book set out to teach: missingness, outliers, types, categories, scale, imbalance, and text. Each was a decision, each rested on an assumption about the world, and each could leak if performed in the wrong order. That last clause has come up in the last three chapters in a row — fit the scaler in-fold, resample in-fold, vectorize in-fold. It is time to stop previewing it and confront it directly. Chapter 11 is about leakage, splits, and the order of operations: the difference between a pipeline that looks brilliant in your notebook and one that actually works on data it has never seen.

##  AI Wayback Machine

**Karen Spärck Jones** was a British computer scientist who, in 1972, introduced inverse document frequency — the idea that a word's importance falls as it appears in more documents. It is the "IDF" in TF-IDF, and the reason your model down-weights "loan" and pays attention to "consolidation." She also argued, decades before it was fashionable, that computing was too important to be left to men.

**Run this:**

```
Who is Karen Spärck Jones, and how does their work connect to the TF-IDF text features we built in this chapter? Keep it to three paragraphs. End with the single most surprising thing about their career or ideas.
```

→ Search **"Karen Spärck Jones"** on Wikipedia.

**Now make the prompt better.** Try one of these:

- Ask it to explain, with a small worked example, how inverse document frequency is actually computed.
- Add a constraint: "Answer including how bag-of-words and TF-IDF compare to modern neural embeddings, and what each gives up."

What changes? What gets better? What gets worse?

## Sources

- Spärck Jones, K. "A Statistical Interpretation of Term Specificity and Its Application in Retrieval." *Journal of Documentation*, 1972. — Origin of inverse document frequency, the core of TF-IDF.
- Salton, G., and Buckley, C. "Term-weighting Approaches in Automatic Text Retrieval." *Information Processing & Management*, 1988. — Classic source for TF-IDF term weighting; supports adding text features without becoming an NLP text.
- Jurafsky, D., and Martin, J. H. *Speech and Language Processing* (3rd ed. draft). Stanford. — Accessible authority on basic text-representation concepts; cite by draft version, as it changes.
- Pedregosa et al. "Scikit-learn." *JMLR*, 2011; the scikit-learn text feature-extraction and `ColumnTransformer` documentation (verify against installed version). — Implementation references for `CountVectorizer`, `TfidfVectorizer`, and combining text with tabular features.
