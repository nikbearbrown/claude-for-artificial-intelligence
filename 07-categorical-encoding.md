# Categorical Encoding: One Strategy, Three Wrong Answers

The model will not accept text. You have a clean dataframe now — `home_ownership`, `purpose`, `emp_title`, and `grade` are all spelled consistently after the last chapter — but the moment you hand them to a scikit-learn estimator it stops:

```python
ValueError: could not convert string to float: 'RENT'
```

So you reach for the one-liner everyone reaches for first:

```python
from sklearn.preprocessing import OrdinalEncoder
enc = OrdinalEncoder()
X = enc.fit_transform(df[["home_ownership", "purpose", "emp_title", "grade"]])
```

It runs. No error. Every category is now an integer, the model trains, and the metrics come back. The pipeline looks finished.

It is broken in three different ways at once, and the breakage is invisible because nothing crashed. You have just told your model that `RENT` is less than `OWN`, that `emp_title` "accountant" (encoded 3) is half of "doctor" (encoded 6), and you have — by luck — done the *only* one of the three that was actually fine, `grade`, for the wrong reason. This chapter is about why one encoder cannot serve three kinds of categorical, and how to tell which kind you are looking at.

![A three-row grid showing OrdinalEncoder applied to each categorical type: grade gets a true risk order, home_ownership is handed a fabricated RENT-greater-than-OWN order, and emp_title is told doctor equals twice accountant — only the first verdict is correct.](images/07-categorical-encoding-fig-01.png)

*Figure 7.1 — A single encoder produces a true order for the ordinal column and silent fabrications for both nominal columns; the breakage never throws an error.*

## Three Kinds of Categorical, Not One

The reason a single encoder fails is that "categorical" is not one thing. The LendingClub file contains all three of the types that demand different treatment [verify against the actual LendingClub file]:

**Low-cardinality nominal.** `home_ownership` — values like `RENT`, `OWN`, `MORTGAGE`, `OTHER`. A handful of categories, *no inherent order.* `OWN` is not greater than `RENT`; they are just different. `purpose` is the same shape: a dozen-ish values (`debt_consolidation`, `credit_card`, `home_improvement`, `medical`…), unordered. [Medium]

**High-cardinality nominal.** `emp_title` — tens of thousands of distinct job titles even after the cleaning of the last chapter. Still no order, but now *many* categories. [Medium] [verify against the actual LendingClub file]

**Ordinal.** `grade` — `A`, `B`, `C`, `D`, `E`, `F`, `G`. These *do* have an order: an A-grade borrower is rated less risky than a G-grade borrower, and that ordering is the whole point of the column. `sub_grade` (`A1`…`G5`) is the same with finer resolution.

The semantic difference among these three is not visible in the dtype. All three are `object` columns of strings. The difference lives in what the categories *mean*, and meaning is exactly what an AI assistant cannot read off the column. It can tell you `grade` has seven values; it cannot know that those seven are ranked unless you tell it. [High]

## Encoder One: Ordinal Encoding — Right for `grade`, a Lie for the Rest

`OrdinalEncoder` maps each category to an integer: `A`→0, `B`→1, and so on. For an ordered column this is exactly correct *if you supply the order.* By default scikit-learn orders categories alphabetically, which for `grade` happens to coincide with the real risk order (A < B < ... < G) — a lucky accident you should never rely on. Make the order explicit:

```python
from sklearn.preprocessing import OrdinalEncoder

grade_order = [["A", "B", "C", "D", "E", "F", "G"]]
grade_enc = OrdinalEncoder(categories=grade_order)
df["grade_enc"] = grade_enc.fit_transform(df[["grade"]])
# A=0, B=1, ... G=6  — the distance now encodes increasing risk
```

This is right because the integer distance is *meaningful*: a model that learns "higher number = higher risk" is learning something true about the world. The number line and the risk line agree.

Now apply the same encoder to `home_ownership` and watch it lie. Alphabetical order gives `MORTGAGE`→0, `OTHER`→1, `OWN`→2, `RENT`→3. The model now believes `RENT` (3) is three units "more" than `MORTGAGE` (0), and that `OWN` sits exactly between them. None of that is true. There is no axis on which renting is greater than mortgaging. You have manufactured an ordering out of alphabetical accident and handed it to the model as if it were signal. A linear model will fit a coefficient to this fake order; a tree will split on thresholds that mean nothing. [High]

This is the first of the three breakages: **ordinal encoding fakes an order on nominal data.**

## Encoder Two: One-Hot — Right for `home_ownership`, a Catastrophe for `emp_title`

The fix for unordered categories is one-hot encoding: one binary column per category, no false ordering implied. `RENT` becomes `[0,0,0,1]`, `OWN` becomes `[0,0,1,0]`. The model sees four independent indicators and no spurious arithmetic.

```python
from sklearn.preprocessing import OneHotEncoder

ohe = OneHotEncoder(handle_unknown="ignore", sparse_output=False)
home_ohe = ohe.fit_transform(df[["home_ownership"]])
print(home_ohe.shape[1], "columns for home_ownership")   # ~4-5 columns
```

For `home_ownership` (4–5 categories) and `purpose` (a dozen-ish), this is the right tool: a small, honest set of indicator columns. The `handle_unknown="ignore"` argument matters — it tells the encoder what to do when a category appears at prediction time that it never saw in training, which on real data it will. [Medium]

Now point one-hot at `emp_title` and the catastrophe is structural, not subtle:

```python
title_ohe = OneHotEncoder(handle_unknown="ignore", sparse_output=False)
# DON'T actually run this on the full column without watching memory:
n_titles = df["emp_title"].nunique()
print(f"One-hot on emp_title would create {n_titles:,} columns")
# tens of thousands of columns  [verify against the actual LendingClub file]
```

One-hot encoding `emp_title` creates one column per distinct job title — tens of thousands of columns, almost all zero in almost every row. This is the curse of dimensionality made concrete: the feature matrix explodes, memory balloons, training slows to a crawl, and every individual title column is so sparse that the model cannot learn anything stable from it. A title that appears in three rows gets its own feature that is on for three rows and off for half a million. The model overfits to noise or ignores the column entirely. [High]

This is the second breakage: **one-hot encoding blows up on high-cardinality nominal data.**

## Encoder Three: Handling High Cardinality Without Exploding

`emp_title` is unordered, so ordinal is wrong, and high-cardinality, so one-hot is wrong. It needs a third strategy. Three defensible options, each with a judgment attached:

**Frequency / count encoding.** Replace each title with how often it appears. Cheap, one column, no explosion — but it asserts that two titles sharing a frequency are interchangeable, which is a strong and often false claim.

```python
freq = df["emp_title"].value_counts(normalize=True)
df["emp_title_freq"] = df["emp_title"].map(freq).fillna(0)
```

**Grouping rare categories.** Keep the top *N* titles as themselves, collapse the long tail into `"other"`, then one-hot the result. This bounds the column count and concentrates signal where there is enough data to learn from. The judgment is the cutoff: where does "common enough to matter" end?

```python
top = df["emp_title"].value_counts().head(30).index
df["emp_title_grouped"] = df["emp_title"].where(
    df["emp_title"].isin(top), other="other")
# now one-hot emp_title_grouped -> ~31 columns, not 30,000
```

**Target encoding.** Replace each title with the mean of the target (`loan_status` default rate) for that title. Powerful, compact — and dangerous. It leaks the target into the features, so it must be fit *inside* cross-validation folds, on training data only, or it will inflate your metrics with information the model would not have at prediction time. The literature flags target encoding precisely because it trades interpretability and leakage-safety for performance. Use it only when you understand the leakage mechanism and can defend the cross-validation discipline. [High]

```python
# Target encoding — only fit on training folds, never on the full data
# (leakage risk is real; see Kuhn & Johnson on this exact trap)
```

Which of the three is right is *not* a coding question. It depends on whether titles carry signal worth preserving, how much data backs the rare ones, and whether your model and stakeholders can tolerate target-encoding's leakage risk. The AI can write all three. Choosing among them is the judgment.

### Two Traps Hiding in "It Ran Fine"

Beyond the three big mismatches, categorical encoding carries two traps that surface only at prediction time — the worst possible moment to discover them.

**The unseen-category trap.** Your training data contains the `purpose` values present in the rows you trained on. The day a new application arrives with a `purpose` you never saw — a category LendingClub added after your snapshot, or simply a rare value absent from your sample — a naive encoder either crashes or, worse, silently produces a row of all zeros that the model misreads. This is why `OneHotEncoder(handle_unknown="ignore")` is not optional boilerplate; it is the explicit decision about *what the model should do when the world shows it something new.* The default — to error — is sometimes the right call (you *want* to know about a new category), and "ignore" is sometimes right (you want the pipeline to keep running). Which one you choose is a judgment about how the model will be deployed, and it belongs to you, not to the encoder's defaults. [Medium]

**The dummy-variable trap.** One-hot encoding *k* categories produces *k* columns, but those columns are perfectly collinear — knowing any *k−1* of them tells you the last. For tree models and most regularized learners this is harmless. For an ordinary linear regression it makes the design matrix singular and the coefficients unidentifiable. The fix, `drop="first"`, removes one column and makes the rest interpretable as contrasts against a baseline category. [Medium] Whether you need it depends entirely on which model consumes the features — which means you cannot choose the encoder correctly without knowing what comes after it. The encoding step is not isolated; it is in conversation with the model.

```python
# For linear models, drop a reference level to avoid collinearity:
ohe_linear = OneHotEncoder(drop="first", handle_unknown="ignore")
# For trees, keep all levels — collinearity does not hurt them:
ohe_tree = OneHotEncoder(handle_unknown="ignore")
```

Neither trap throws an obvious error during training on your sample. Both produce a model that is wrong in a way the metrics on that sample will not reveal. That is the through-line of this chapter: categorical encoding fails *silently*, and the only defense is understanding what each column means and what the downstream model needs.

## The Encoding Decision Table

Here is the artifact, in the book's recurring five-column shape — the decision recorded next to the evidence and the assumption.

| Column | Type (evidence) | Wrong encoder & why | Chosen encoder | Assumption / risk |
|---|---|---|---|---|
| `grade` | Ordinal — A<B<...<G is real risk order | One-hot (throws away the order) | `OrdinalEncoder` with explicit `categories` | Distances between grades treated as equal steps |
| `home_ownership` | Low-card nominal — 4–5 values, no order | Ordinal (fakes RENT>OWN) | One-hot | A handful of extra columns; fine |
| `purpose` | Low-card nominal — ~12 values, no order | Ordinal (fakes order) | One-hot | ~12 columns; manageable |
| `emp_title` | High-card nominal — tens of thousands | One-hot (column explosion) | Group rare → one-hot, or frequency | Cutoff for "rare" is a judgment; target enc. risks leakage |

Read the third column — "wrong encoder & why" — as the lesson. Each row names an encoder that would *run without error* and produce a *broken model*. That is the danger of categorical encoding: the failures are silent. Nothing throws. The metrics come back. And two of your three columns are feeding the model fiction.

## Putting It Together: A ColumnTransformer

In practice you apply the three strategies in one composed transformer, which also enforces the train/test discipline you met in Chapter 5 — fit on train, apply to test, no leakage.

```python
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import OneHotEncoder, OrdinalEncoder

# group rare emp_titles first (structural prep)
top = df["emp_title"].value_counts().head(30).index
df["emp_title_grouped"] = df["emp_title"].where(
    df["emp_title"].isin(top), other="other")

preprocess = ColumnTransformer([
    ("ordinal", OrdinalEncoder(categories=[["A","B","C","D","E","F","G"]]),
        ["grade"]),
    ("nominal_low", OneHotEncoder(handle_unknown="ignore"),
        ["home_ownership", "purpose"]),
    ("nominal_high", OneHotEncoder(handle_unknown="ignore"),
        ["emp_title_grouped"]),
])

X = preprocess.fit_transform(df)   # fit on TRAIN only in a real split
```

Three encoders, three column groups, one object that travels with the model. The structure of the transformer *is* the documentation: anyone reading it can see that `grade` was treated as ordered and `home_ownership` as unordered — which is the human judgment made legible in code.

A word on why the `ColumnTransformer` matters beyond convenience. It binds the encoding decisions to the *fit/transform* discipline you met in Chapter 5: the encoder learns its category vocabulary from the training rows only, and applies that fixed vocabulary to validation and test. Encode the full dataset before splitting and you leak — the model's feature space was defined using rows it is supposed to be predicting blind. With high-cardinality fields and target encoding the leakage is severe enough to manufacture accuracy that evaporates in production. The transformer is not just tidy; it is the mechanism that makes the leakage discipline automatic instead of a thing you have to remember on every column. [High]

There is also a quiet ordering question worth surfacing: encoding generally comes *after* imputation, because most encoders will choke on or silently mishandle a `NaN` category, and *after* structural cleaning, because you cannot order `grade` correctly until it is a clean `A`–`G` rather than `" a "`. The "right" narrative order of the book — outliers, imputation, structure, encoding — is also, mostly, the right execution order. Where it is not, the `ColumnTransformer` is where the dependency becomes visible, because a misordered step fails here loudly rather than three chapters downstream quietly.

### Before and After

| Column | Naive (ordinal-everything) | What the model "learns" | Correct |
|---|---|---|---|
| `grade` | A=0…G=6 | A < G in risk — *true* | Same, but order made explicit, not accidental |
| `home_ownership` | MORTGAGE=0…RENT=3 | RENT > OWN > OTHER — *false* | One-hot: four independent flags, no order |
| `emp_title` | accountant=3, doctor=6 | doctor = 2× accountant — *false* | Group rare + one-hot, or frequency |

The naive column is what ships when someone runs `OrdinalEncoder` on the whole categorical block and moves on. One of three rows is right. The other two are confident, silent fabrications.

## Exercises: Matching Encoder to Meaning

**1. Three columns, three encoders.** Encode `grade`, `home_ownership`, and `emp_title` correctly, each with its appropriate strategy. Then deliberately encode all three with `OrdinalEncoder` and train the same model both ways. Report the difference and identify which columns' coefficients are now meaningless.

**2. Count the explosion.** Compute how many columns one-hot encoding `emp_title` would produce versus grouping to the top 30 first. Report both numbers and estimate the memory difference. State the cutoff you would choose for "rare" and defend it.

**3. The order you supply.** Encode `grade` with default alphabetical ordinal encoding and with an explicit reversed order (G=0…A=6). Show that the model fits either one. Explain why "it ran and the metric is fine" does not tell you the order was correct — and what *does* tell you.

**4. Make the AI guess the type.** Give Claude Code the four column names and ask it to choose an encoder for each *without* telling it which are ordered. See whether it recognizes `grade` as ordinal. Then tell it the business meaning and watch the recommendation change. The exercise demonstrates that encoding choice requires semantic knowledge the AI does not have until you supply it.

## A Bridge to Scaling and Transformation

Your categoricals are now numbers — honestly typed, correctly ordered or correctly unordered. But the numeric columns you cleaned earlier still live on wildly different scales: `annual_inc` runs into the hundreds of thousands, `int_rate` sits between 5 and 30, `grade_enc` between 0 and 6. A distance-based model or a regularized regression treats a one-unit change in each as equivalent, which means income's sheer magnitude would dominate everything else by accident. And several of those columns — `annual_inc`, `loan_amnt`, `revol_bal` — are still badly right-skewed, the same skew that made outlier detection hard back in Chapter 4. The next chapter asks when to put every feature on a common scale, when a log transform is warranted, and — crucially — when it is *not*, because transforming a column that is already well-behaved is its own quiet way of degrading the data.

> ### The AI Wayback Machine: Ronald A. Fisher
>
> When **Ronald A. Fisher** sat down with agricultural trial data in the 1920s and 30s, he confronted the same problem you face with `home_ownership` and `grade`: how do you bring *categories* — a variety of wheat, a type of fertilizer, a block of land — into a quantitative analysis without pretending they are quantities? His answer, the design of experiments and the analysis of variance, was built on treating categorical factors as *factors* — discrete, named levels — rather than smuggling them onto a number line where they did not belong. [High]
>
> That distinction is exactly the one this chapter turns on. `grade` is a factor with an order; `home_ownership` is a factor without one; `emp_title` is a factor with too many levels to one-hot. Fisher's discipline — name the structure of the variable before you do arithmetic on it — is what separates correct encoding from the silent fabrications that `OrdinalEncoder`-on-everything produces.
>
> A useful prompt for an AI assistant: *"Using Fisher's distinction between ordered and unordered factors, classify these LendingClub categorical columns and explain why treating an unordered factor as a number line injects false structure into the model."* The assistant can encode the columns. Fisher's century-old insight — that a category's *structure* determines what arithmetic is legitimate — is what tells you whether the encoding is faithful or fiction. [High]

## Sources

- Kuhn, M., & Johnson, K. (2019). *Feature Engineering and Selection.* CRC Press. — Encoding choices, high-cardinality strategies, target-encoding leakage risk. [High]
- pandas development team (current). "Categorical data." *pandas documentation.* — Ordered vs. unordered `category` dtype; the nominal/ordinal distinction in code. [Medium]
- scikit-learn developers (current). "Encoding categorical features." *scikit-learn User Guide.* — `OneHotEncoder`, `OrdinalEncoder`, `handle_unknown`; verify API behavior in your environment. [Medium]
- Wickham, H. (2014). "Tidy Data." *Journal of Statistical Software*, 59(10). — The tidy shape that encoding produces a model-ready version of. [High]
