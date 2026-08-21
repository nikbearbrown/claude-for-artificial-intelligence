# Chapter 11 — Leakage, Splits, and Pipeline Order

A model that scores 0.94 on the validation set and 0.71 in production has not gotten worse overnight. It was never as good as 0.94. The number was a lie, and the lie was assembled, line by careful line, in a notebook that ran without a single error.

Picture the moment. You have spent ten chapters cleaning the LendingClub loan dataset. You parsed `int_rate` out of its `"13.56%"` string. You log-transformed `annual_inc`. You imputed the missing `emp_length` values, scaled `dti` and `revol_util`, one-hot encoded `home_ownership`, and resampled the minority class of `loan_status` so the defaulters were not drowned out nine-to-one. Then you split the data into train and test, fit a logistic regression, and the cross-validated AUC came back at 0.94. You wrote it in the deck. Three weeks later the model is live, scoring real applications, and the realized AUC is 0.71.

Nothing in your code threw an exception. That is precisely the problem. Data leakage is the silent killer of machine-learning projects because it produces no error message, no warning, no red text — only a number that is too good, which is the one kind of bad news a tired analyst is least inclined to question. This chapter is about the discipline that prevents it. It is the most consequential chapter in this book, because every cleaning decision you have learned to make can be made *correctly* and still poison your model if it happens in the wrong order, on the wrong slice of data, at the wrong moment in the workflow.

## What Leakage Actually Is

Data leakage is the use, during model training, of information that will not be available at the moment the model has to make a real prediction. [High] The model learns from a fact it could not legitimately know, and so its measured performance reflects a world that will not exist when it is deployed.

There are two broad families, and you must be able to tell them apart.

The first is **target leakage**: a feature contains information about the outcome that, in the real timeline, only becomes known *after* the outcome itself. On the LendingClub data, the canonical trap is a column like `total_rec_prncp` (total principal received) or a `recoveries` field `[verify against the actual file]`. These describe what happened to the loan over its life. If you are predicting whether a loan will default, a feature recording how much principal was eventually repaid is not a predictor — it is a paraphrase of the answer. Feed it to the model and you will see spectacular accuracy in the notebook and catastrophic failure in production, because at the moment you actually score a *new* applicant, no principal has been received yet. The column will be empty, or zero, or absent entirely.

Target leakage is a *modeling* error, and the human-judgment layer is the only thing that catches it. No automated profiler can tell you that `recoveries` is measured after the default event. That is a fact about the world — about the order in which loan events occur in time — and you have to supply it. This is the chapter's first appearance of the book's spine: the cleaning question is never "is this column numeric and complete?" It is "could I have known this value at prediction time?"

The second family is **preprocessing leakage**, and it is the one this chapter mostly drills, because it is mechanical, ubiquitous, and almost invisible. It happens when a transformation *learns something from the data* and you let it learn from data it should not see — specifically, from the test set, or from the validation fold, or from any rows the model is supposed to be evaluated against. This is the family that turned your honest cleaning into a 0.94 mirage.

## The Distinction That Prevents Almost Everything: fit Versus transform

Every scikit-learn transformer separates two operations. **`fit`** looks at data and *learns parameters* from it. **`transform`** *applies* those learned parameters to data. A `StandardScaler` fit on a column learns that column's mean and standard deviation; transform then subtracts the mean and divides by the standard deviation. A `SimpleImputer` with `strategy="median"` fit on a column learns the median; transform fills the blanks with it. A `OneHotEncoder` fit on a column learns the set of categories it will produce columns for; transform expands new data into those columns.

The whole of preprocessing-leakage prevention reduces to one rule. [High]

> **Fit on training data only. Transform everything.**

Concretely: you call `fit` (or `fit_transform`) on the training set, and you call `transform` — never `fit` — on the test set. The test set is treated as the future. The future does not get to teach your imputer what the median income is. It can only receive the median the training data already taught.

Here is why the violation is so seductive. Consider the most innocent line in data science:

```python
# THE LEAK — looks harmless, ruins everything
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)        # fit on ALL the data
X_train, X_test = train_test_split(X_scaled, test_size=0.2)
```

The scaler computed the mean and standard deviation of the *entire* dataset, including the rows that will later become your test set. The test rows have therefore contributed to the parameters used to scale the training rows, and the training distribution now carries a faint imprint of the test distribution. Your test set is no longer a clean stand-in for the future. It has whispered to the training data, and the whisper inflates your score.

The fix is to split first, then fit only on the part you are allowed to learn from:

```python
# THE FIX — split before you learn anything
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, stratify=y, random_state=42
)

scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)   # learn from train
X_test_scaled  = scaler.transform(X_test)         # apply to test
```

The difference between these two snippets is the difference between 0.94 and 0.71. Note the `stratify=y` argument: because LendingClub default is the rare class, you split in a way that preserves the class ratio in both halves, so your test set is not accidentally starved of defaulters. [Medium]

![Two parallel timelines. WRONG WAY: fit_transform on all data, then split, with a dashed arrow showing the test set whispering its statistics backward into the fit, producing an inflated 0.94 labelled a lie. RIGHT WAY: split first and seal the test set, fit on train and resample in-fold, transform the test set, evaluate, producing an honest lower 0.71.](images/11-leakage-splits-and-pipeline-order-fig-01.png)

*Figure 11.1 — Fit on all data before splitting and the test set leaks backward into training, inflating the score; split first and fit on train only, and the lower number is the true one.*

## Which Operations Leak

Not every transformation can leak. The test is simple: **does the operation learn anything from the data?** If it does, it must be fit on training data only. If it does not — if it applies a fixed, data-independent rule — its placement relative to the split does not matter for leakage (though it may still matter for other reasons).

Operations that **learn** and therefore must be fit on train only:

- **Imputation** (Chapter 5). The median, mean, or most-frequent value is *learned* from the data. Computing the median over the full dataset leaks the test set's central tendency into training. Fit the imputer on train; transform test.
- **Scaling and standardization** (Chapter 8). Means, standard deviations, min/max ranges, quantiles for a `QuantileTransformer` — all learned. All must come from train only.
- **Encoding that learns categories or statistics.** A plain `OneHotEncoder` learns the *set* of categories, which is a mild form of learning; the dangerous version is **target encoding**, where you replace a category like a LendingClub `addr_state` with the mean default rate for that state. That mean is computed from the target. Compute it over the whole dataset and you have piped the answer directly into the feature. Target-derived features are target leakage wearing a feature's clothing, and they must be computed inside the training fold, never before the split.
- **Feature selection that consults the target.** If you pick the top-*k* features by correlation with `loan_status` using all the data, your "selected" features already know about the test rows. Selection is model fitting; it goes inside the fold.
- **Resampling for class imbalance** (Chapter 9). This is the subtle one and it gets its own section.

Operations that do **not** learn, and so are split-agnostic for leakage purposes:

- Parsing `"13.56%"` into the float `13.56` (Chapter 6). The rule does not depend on the data's distribution.
- Lowercasing a string, stripping whitespace, fixing `"Full-time"` / `"full time"` capitalization (Chapter 6).
- A fixed log transform, `np.log1p(annual_inc)`, that uses no learned parameter.
- Dropping a column you have decided is leaky.

These are safe to do before the split because they encode a decision you made, not a statistic the data taught. The honest convenience is real: you can do the deterministic structural cleaning up front and reserve the split-then-fit discipline for the learned transformations. But when in doubt, push it inside. There is no penalty for fitting a deterministic step inside the pipeline; there is a 0.23-AUC penalty for fitting a learned step outside it.

## Resampling Must Happen Inside the Fold

Chapter 9 taught you to fight LendingClub's class imbalance — defaulters are perhaps 12–15% of loans `[verify against the actual file]` — with techniques like SMOTE, which synthesizes new minority-class examples by interpolating between real ones. The single most common leakage error in imbalanced learning is to resample *before* splitting or *before* cross-validation.

Here is the mechanism. SMOTE creates a synthetic defaulter by interpolating between two real defaulters. If you resample the whole dataset and then split, a synthetic point in your training set may have been built from a real point that landed in your test set. The test "future" has now been used to manufacture training data. Worse, plain random oversampling literally *duplicates* minority rows; duplicate one before splitting and the same row can appear in both train and test, so the model is tested on rows it memorized.

The rule, tying directly back to Chapter 9: [High]

> **Resample inside the cross-validation fold, after the split, on training data only. Never resample the test set at all.**

You never resample the test set, because the test set must reflect the real, imbalanced world the model will face. You evaluate on the true 12% base rate, not a synthetic 50/50.

The clean way to enforce this is the `imbalanced-learn` library's `Pipeline`, which is leakage-aware: it applies the resampler only during `fit`, never during `transform`/`predict`. [Medium — verify imblearn version behavior]

```python
from imblearn.pipeline import Pipeline as ImbPipeline
from imblearn.over_sampling import SMOTE
from sklearn.linear_model import LogisticRegression

clf = ImbPipeline(steps=[
    ("smote", SMOTE(random_state=42)),     # fires only on train, inside each fold
    ("model", LogisticRegression(max_iter=1000)),
])
```

When this pipeline is dropped into `cross_val_score`, SMOTE runs separately inside each fold, on that fold's training portion only. The held-out portion stays untouched and imbalanced. That is the only honest measurement.

## The Correct Order of Operations

There is a defensible sequence for a tabular cleaning-and-modeling pipeline. The ordering is not arbitrary; each step assumes the previous one is done. [Medium — order is sound but not the only valid arrangement]

1. **Deterministic structural cleaning** (Chapter 6): parse strings to numbers, fix dtypes, normalize capitalization and whitespace. Data-independent, so it can precede the split.
2. **Drop leaky columns by judgment** (this chapter): remove `total_rec_prncp`, `recoveries`, and any post-outcome field. A human decision about the timeline.
3. **Split** into train and test — and from here, the test set is sealed.
4. **Impute** missing values (Chapter 5): fit on train.
5. **Encode** categoricals (Chapter 7): fit on train; handle unknown categories so a state that appears only in test does not crash transform.
6. **Scale / transform** numerics (Chapter 8): fit on train.
7. **Resample** for imbalance (Chapter 9): train fold only.
8. **Fit the model**.

Steps 4 through 8 all live *after* the seal and, in honest evaluation, *inside* each cross-validation fold. The way you guarantee that — without hand-discipline you will eventually forget on a Friday afternoon — is to stop hand-coding the order and let scikit-learn enforce it structurally.

## Pipeline and ColumnTransformer: Making Leakage Structurally Impossible

The deep reason to use a scikit-learn `Pipeline` is not tidiness. It is that a pipeline *cannot* leak preprocessing, by construction. When you call `pipeline.fit(X_train, y_train)`, every step's `fit` sees only `X_train`. When you call `pipeline.predict(X_test)`, every step runs `transform` only. The fit/transform discipline is no longer something you remember; it is something the object guarantees.

`ColumnTransformer` lets you route different columns to different transformers — numeric columns to an imputer-plus-scaler, categorical columns to an imputer-plus-encoder — and bundles them so the whole thing fits as one unit on the training fold.

Here is the leakage-proof structure for the LendingClub data, end to end:

```python
import numpy as np
import pandas as pd
from sklearn.compose import ColumnTransformer
from sklearn.impute import SimpleImputer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split, cross_val_score, StratifiedKFold
from imblearn.pipeline import Pipeline as ImbPipeline
from imblearn.over_sampling import SMOTE

# --- column groups (verify exact names against the file) ---
numeric_features = ["loan_amnt", "int_rate", "annual_inc", "dti", "revol_util"]   # [verify against the actual file]
categorical_features = ["home_ownership", "purpose", "term", "grade"]              # [verify against the actual file]
LEAKY = ["total_rec_prncp", "recoveries", "total_pymnt"]                           # [verify against the actual file]

df = pd.read_csv("lending_club.csv").drop(columns=LEAKY, errors="ignore")  # step 2: drop by judgment
y = (df["loan_status"] == "Charged Off").astype(int)                       # define the target  [verify]
X = df.drop(columns=["loan_status"])

# step 3: split first; the test set is now sealed
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, stratify=y, random_state=42
)

# steps 4-6: per-type preprocessing, each fit on train only
numeric_pipe = ImbPipeline(steps=[
    ("impute", SimpleImputer(strategy="median")),
    ("scale", StandardScaler()),
])
categorical_pipe = ImbPipeline(steps=[
    ("impute", SimpleImputer(strategy="most_frequent")),
    ("encode", OneHotEncoder(handle_unknown="ignore")),
])

preprocess = ColumnTransformer(transformers=[
    ("num", numeric_pipe, numeric_features),
    ("cat", categorical_pipe, categorical_features),
])

# steps 7-8: resample + model, wired so SMOTE fires only on training folds
full_pipeline = ImbPipeline(steps=[
    ("preprocess", preprocess),
    ("smote", SMOTE(random_state=42)),
    ("model", LogisticRegression(max_iter=1000)),
])

# honest cross-validated estimate: everything re-fit inside each fold
cv = StratifiedKFold(n_splits=5, shuffle=True, random_state=42)
scores = cross_val_score(full_pipeline, X_train, y_train, cv=cv, scoring="roc_auc")
print(f"CV AUC: {scores.mean():.3f} (+/- {scores.std():.3f})")

# final honest test on the sealed set
full_pipeline.fit(X_train, y_train)
test_auc = full_pipeline.score  # use roc_auc_score on predict_proba in practice
```

Read what this code guarantees. The `OneHotEncoder` learns categories from the training fold only; `handle_unknown="ignore"` means a `purpose` value that appears only in the test set produces an all-zero encoding instead of crashing — a real-world necessity, since the future contains categories the past never saw. The `SimpleImputer` medians come from train. The `StandardScaler` statistics come from train. SMOTE synthesizes only inside training folds. The test set is touched exactly once, at the very end, with `transform` and `predict`. There is no line in this pipeline where the future can teach the past.

### Before and After

| Aspect | The leaky notebook | The leakage-proof pipeline |
|---|---|---|
| When you scale/impute | `fit_transform` on all rows, then split | split first, `fit` on train, `transform` on test |
| Where SMOTE runs | on the whole dataset before splitting | inside each CV fold, training portion only |
| Target-derived features | computed over all rows | computed inside the fold or not at all |
| Post-outcome columns | left in "because they were numeric" | dropped by human judgment before the split |
| Reported AUC | 0.94 — and false | lower — and true |
| What you learn in production | that the 0.94 was a story | nothing surprising; the estimate held |

The lower number is the better number. It is the one that survives contact with reality. This is GIGO stated in reverse: a model's measured quality is bounded not only by the quality of its data but by the integrity of the procedure that measured it. Garbage validation in, garbage confidence out.

## The Leakage Audit, as a Five-Column Artifact

Carry this table across the project. For each feature and each pipeline step, fill the row before you trust the model. The middle three columns are where the human judgment lives; no profiler fills them for you.

| Pipeline state | Diagnostic evidence | Action | Assumption introduced | Validation check |
|---|---|---|---|---|
| `recoveries` present | values nonzero only after default | drop before split | "this is measured after the outcome" | confirm column absent from `X` |
| `annual_inc` scaling | scaler fit on full data | move fit inside pipeline, post-split | "test income distribution is unknown at train time" | scaler params computed on `X_train` only |
| `loan_status` imbalance | SMOTE applied pre-split | move SMOTE into `ImbPipeline` | "the deployed base rate stays imbalanced" | test set never resampled |
| `addr_state` target encoding | mean default per state from all rows | compute inside fold | "state risk is estimated, not known" | encoder refit each fold |

## Exercises: The Leakage Hunt

**1. Spot the leak (Apply).** You are handed a notebook with this opening: `df = pd.read_csv("loans.csv"); df = df.fillna(df.mean()); X_train, X_test = train_test_split(df, ...)`. Identify the leak in one sentence, name which family it belongs to, and rewrite the three lines correctly.

**2. The timeline test (Analyze).** For each of these LendingClub-style columns, decide whether it is safe to use when predicting default at application time, and write the one-sentence world-question that justifies your call: `fico_range_high`, `last_pymnt_amnt`, `dti`, `total_rec_int`, `emp_length`. `[verify column meanings against the actual file]`

**3. Build it (Create).** Using `ColumnTransformer` and `imblearn`'s `Pipeline`, assemble a complete preprocessing-plus-resampling-plus-model pipeline for the LendingClub data, then run it through `cross_val_score` with `StratifiedKFold`. Confirm by inspection that no step is fit outside the fold.

**4. Measure the cost of the lie (Evaluate).** Run two pipelines on the same data: one that scales and resamples *before* the split, one that does it correctly inside the pipeline. Report both AUCs and write a short paragraph explaining to a non-technical manager why the higher number is the one you do not trust.

## Bridge

You now have a pipeline that is honest as well as clean — one where the measured number means what it says. But an honest pipeline is still a black box to anyone who did not build it. The next person to touch this model — a colleague, an auditor, a regulator asking why a particular applicant was scored the way they were — cannot see the dozens of judgment calls baked into your `ColumnTransformer`. They cannot see that you dropped `recoveries` because it is measured after default, or that you imputed `emp_length` with the median because the missingness looked MAR rather than informative. Those decisions are invisible in the code's behavior and irreplaceable in its justification. Chapter 12 turns the invisible audit trail into a visible one: the cleaning report, the document that makes every judgment call accountable.

## AI Wayback Machine: Ron Kohavi

Long before "data leakage" was a phrase practitioners traded warnings about, **Ron Kohavi** was working out how to measure a model's performance honestly. His 1995 study comparing cross-validation and the bootstrap for accuracy estimation became one of the foundational treatments of *how to know whether your model is as good as it looks* — the exact question this chapter exists to answer. [Medium — verify publication details]

Kohavi's later career makes the lineage sharper still: he became a leading figure in the practice of online controlled experiments — A/B testing at scale — where a leaked variable or a contaminated control group does not merely embarrass an analyst but misdirects the decisions of an entire company. The throughline is a single discipline: the number you report must come from a procedure that could not have cheated. Cross-validation is that discipline made mechanical, and the `Pipeline` object you built in this chapter is Kohavi's principle compiled into software — a structure that makes it impossible for the evaluation to see what it must not.

Ask an AI assistant the Wayback prompt: *"Explain how Ron Kohavi's work on cross-validation helps a modern data scientist avoid a GIGO failure in data leakage and pipeline sequencing."* Then check its answer against this chapter. The assistant can recite the history; only you can confirm that your own pipeline honors it.

## Sources

- Kohavi, R. (1995). *A Study of Cross-Validation and Bootstrap for Accuracy Estimation and Model Selection.* IJCAI. [Medium — verify exact venue/pages]
- Kaufman, S., Rosset, S., Perlich, C., & Stitelman, O. (2012). *Leakage in Data Mining: Formulation, Detection, and Avoidance.* ACM Transactions on Knowledge Discovery from Data. [Medium]
- Pedregosa, F., et al. (2011). *Scikit-learn: Machine Learning in Python.* Journal of Machine Learning Research, 12, 2825–2830.
- Chawla, N. V., Bowyer, K. W., Hall, L. O., & Kegelmeyer, W. P. (2002). *SMOTE: Synthetic Minority Over-sampling Technique.* Journal of Artificial Intelligence Research, 16, 321–357. DOI 10.1613/jair.953.
- scikit-learn developers. *Pipeline and composite estimators* and *Encoding categorical features* (current documentation; verify API and defaults against the installed version at drafting time).
- imbalanced-learn developers. *Pipeline* (current documentation; verify resampler-only-on-fit behavior against installed version). [Medium]
