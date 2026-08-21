# Imputation: Filling Holes Without Inventing Facts

At the end of the last chapter you converted a pile of `9999999`s and `0`s in `annual_inc` to `NaN`. Those new holes joined the ones already in the file. Run a missingness count and the LendingClub data tells a layered story:

```python
miss = df.isna().mean().sort_values(ascending=False)
print((miss[miss > 0] * 100).round(1))
```

You will see something like this [Medium] [verify against the actual LendingClub file]: `mths_since_last_delinq` missing in well over half the rows; `emp_title` and `emp_length` missing in a single-digit-to-teens percentage; `revol_util` missing in a tiny fraction; and now `annual_inc` missing in a small slice — the slice you created.

The instinct, especially under deadline, is to reach for one line: `df.fillna(df.mean())`. It runs. It removes every `NaN`. The dataframe looks complete. And for at least one of these columns, it is *demonstrably wrong* — not stylistically suboptimal, but wrong in a way that injects false information into your model. This chapter is about why, and about the discipline that replaces the reflex.

## The Mechanism Decides the Strategy

Chapter 3 gave you the vocabulary, due to Donald Rubin's 1976 framework: data can be missing completely at random (MCAR), missing at random conditional on observed variables (MAR), or missing not at random (MNAR), where the missingness depends on the unobserved value itself. [High] That taxonomy is not academic decoration. It is the single most important input to choosing an imputation strategy, because *the reason a value is missing constrains what a defensible fill looks like.*

Walk the LendingClub columns through it.

**`revol_util` — plausibly MCAR.** Revolving-utilization is missing in a small, scattered fraction of rows with no obvious pattern. [Medium] [verify against the actual LendingClub file] When missingness is roughly random, the observed values are an unbiased sample of all values, and a simple imputation — median, given the skew — distorts the distribution least. This is the one place the simple reflex is closest to defensible.

**`emp_length` — plausibly MAR.** Employment length is missing more often for certain employment situations, and it correlates with other observed fields like `emp_title` and `annual_inc`. [Medium] [verify against the actual LendingClub file] When missingness depends on *observed* variables, you can do better than a global fill by *conditioning on those variables* — model `emp_length` from the fields that predict it.

**`mths_since_last_delinq` — MNAR, and the trap.** This column is missing in the majority of rows, and the reason is structural: it is blank precisely for borrowers who *have never been delinquent.* [High] [verify against the actual LendingClub file] The missingness is not noise. It is the most informative thing the column tells you. A blank here means "no delinquency on record" — a fact about the borrower, not an absence of data.

That third case is where mean imputation commits its crime.

## Why Mean Imputation Is Demonstrably Wrong Here

Consider what `df['mths_since_last_delinq'].fillna(df['mths_since_last_delinq'].mean())` actually does. Among borrowers who *have* been delinquent, suppose the average gap is around 34 months. [Medium] [verify against the actual LendingClub file] Mean imputation now writes "34 months since last delinquency" into every row that was blank — that is, into every borrower who *never had a delinquency at all.*

You have just told your model that the most reliable borrowers in the file — the ones with spotless records — had a delinquency about three years ago. You have erased the single strongest signal in the column and replaced it with a fabrication. The direction of the error is perverse: the cleaner the borrower, the bigger the lie.

Let the numbers show it.

```python
col = pd.to_numeric(df["mths_since_last_delinq"], errors="coerce")

print("Observed (had a delinquency):")
print("  count :", col.notna().sum())
print("  mean  :", round(col.mean(), 1))
print("  missing (never delinquent):", col.isna().sum())

# The wrong move:
mean_filled = col.fillna(col.mean())
print("\nAfter mean imputation:")
print("  Every never-delinquent borrower now reads:", round(col.mean(), 1), "months")
print("  Variance collapses from", round(col.var(), 1),
      "to", round(mean_filled.var(), 1))
```

Two damages, both visible in the output. First, the *meaning* is inverted: "never delinquent" became "delinquent ~34 months ago." Second — and this happens with mean imputation on *any* column — the variance collapses. Every imputed value sits exactly on the mean, so the spread shrinks, correlations attenuate, and any standard error computed downstream is too small. Mean imputation lies twice: once about the value, once about your certainty.

![Before/after histograms of a missing-not-at-random column: the wide observed distribution on the left collapses, after mean imputation, into a single towering spike of never-delinquent borrowers stacked on the mean.](images/05-imputation-fig-01.png)

*Figure 5.1 — Filling an MNAR blank with the mean crushes the column's spread into one spurious spike, inverting the very signal the missingness encoded.*

## The Right Move for MNAR: Make Absence a Feature

When missingness is informative, the correct response is not to fill the value — it is to *encode the fact that it was missing.* Two complementary moves.

**A missing-indicator flag.** Add a binary column that records whether the original value was present. This preserves the signal "never delinquent" as a feature your model can use directly.

```python
df["had_delinquency"] = col.notna().astype(int)
```

**A semantically honest fill for the numeric column.** Now that the *fact* of never-delinquency lives in `had_delinquency`, you can fill the numeric column with a value that the model can learn to interpret jointly with the flag. A large sentinel (e.g., a value beyond the observed maximum) communicates "delinquency is far in the past or never," and tree-based models handle it cleanly. [Medium]

```python
sentinel = col.max() + 12      # beyond any observed gap
df["mths_since_last_delinq_filled"] = col.fillna(sentinel)
```

The pairing matters. The flag carries the categorical truth; the filled column carries an ordering that does not contradict it. What you must *not* do is fill with the mean and discard the flag, because that throws away the only real information the column contained. The decision here is pure judgment: an AI can tell you the column is 60% missing, but only a human who understands that LendingClub leaves this field blank for clean borrowers can know that the missingness *is the data.* [High]

## The Right Move for MAR: Condition on What You Know

For `emp_length`, missingness tracks observed fields, so a conditional imputation beats a global one. The principled tool is multivariate imputation by chained equations — the workflow Stef van Buuren systematized — where each incomplete variable is modeled from the others, iteratively. [High] scikit-learn ships an experimental version as `IterativeImputer`. [Medium / verify API in your environment]

```python
from sklearn.experimental import enable_iterative_imputer  # noqa: F401
from sklearn.impute import IterativeImputer

# emp_length must already be numeric (Chapter 6 turns "10+ years" -> 10)
num_cols = ["emp_length_num", "annual_inc", "loan_amnt", "revol_bal"]
imp = IterativeImputer(random_state=0, max_iter=10)
df[num_cols] = imp.fit_transform(df[num_cols])
```

Notice the order dependency, flagged in the comment: you cannot run this until `emp_length` is a number, and turning `"10+ years"` into `10` is structural cleaning — the next chapter. This is a recurring truth of real pipelines: the steps are entangled, and the cleanest narrative order (outliers, then imputation, then structure) is not always the safe *execution* order. Document the dependency rather than pretending it away.

A cheaper, often-sufficient MAR move is group-wise imputation — fill `emp_length` with the median *within* a meaningful group rather than globally:

```python
df["emp_length_num"] = df.groupby("home_ownership")["emp_length_num"] \
                          .transform(lambda s: s.fillna(s.median()))
```

This respects the conditional structure without a full model, and it is far easier to explain to a stakeholder than chained equations — which is itself a reason to prefer it when it suffices.

## The Right Move for MCAR: Keep It Simple, But Use the Median

For `revol_util`, scattered and roughly random, a single-column fill is defensible. Because the column is right-skewed, use the *median*, not the mean — the median is the resistant center, unmoved by the same tail extremes you wrestled with in Chapter 4. [High]

```python
from sklearn.impute import SimpleImputer
imp = SimpleImputer(strategy="median")
df["revol_util"] = imp.fit_transform(df[["revol_util"]])
```

Even here, add a flag if the missingness fraction is non-trivial. The cost of a `revol_util_missing` indicator is one column; the benefit is that you have not asserted certainty you do not have.

### Why "Just Drop the Rows" Is Not Free

The simplest response to missing data is to delete any row with a hole — `df.dropna()`. It is tempting because it requires no decision about *what value* belongs in the gap. But it makes a much larger decision silently: it changes *which borrowers your model is about.* Drop every row missing `mths_since_last_delinq` and you have deleted the *majority* of the file — every borrower who was never delinquent, which is to say most of the good borrowers. Your "clean" dataset is now a non-random sample skewed toward the delinquent, and any default-rate estimate from it will be wildly pessimistic. [High]

Listwise deletion is only defensible when missingness is genuinely MCAR *and* the lost rows are a small fraction. The moment missingness is MAR or MNAR — which, on this file, it mostly is — deletion introduces exactly the bias imputation exists to avoid. The reflex `dropna()` is not the safe conservative choice it feels like. It is an imputation strategy in disguise, one that imputes "this kind of borrower does not exist."

### KNN Imputation: A Middle Path

Between the simplicity of a median fill and the machinery of chained equations sits `KNNImputer`, which fills a missing value with the average of its *k* nearest complete neighbors in feature space. [Medium / verify API] It respects local structure — a borrower missing `revol_util` is filled from other borrowers who resemble her on the columns that *are* present — without committing to a full iterative model.

```python
from sklearn.impute import KNNImputer
num_cols = ["annual_inc", "loan_amnt", "revol_bal", "int_rate"]
knn = KNNImputer(n_neighbors=5)
df[num_cols] = knn.fit_transform(df[num_cols])
```

Two cautions make it a judgment call rather than a default. First, KNN requires the features to be on comparable scales — otherwise the "distance" is dominated by whichever column has the largest raw magnitude, which on this file is `annual_inc`. That is a forward reference to scaling (Chapter 8) and a reminder that the pipeline steps are entangled. Second, KNN inherits whatever bias lives in the neighbors: if high earners are systematically missing a field, their "nearest neighbors" may also be unusual, and the fill propagates the pattern. KNN is a reasonable choice for MCAR and mild MAR. It is not a cure for MNAR, where the missingness encodes information no neighbor can supply.

### What About Categorical Missingness?

Everything so far has concerned numeric columns, but the file also has missing *categories* — `emp_title` is blank for borrowers who left the field empty. The mechanics differ but the principle holds. You do not "average" a category; the analogues are mode imputation (fill with the most common value) and, far more often the right move, treating "missing" as *its own category*.

```python
df["emp_title"] = df["emp_title"].fillna("unknown")
```

Mode imputation has the same flaw as mean imputation: it asserts that every borrower who skipped `emp_title` holds the single most common job in the file, which is plainly false and concentrates a fabricated mass on one value. Making "missing" an explicit category is almost always more honest, because — exactly as with the delinquency flag — *the act of leaving the field blank may itself be informative.* A borrower who declined to state a job title may differ systematically from one who entered "teacher." Mode imputation erases that difference; an explicit `"unknown"` category preserves it for the model to use. The judgment is the same one you made for `mths_since_last_delinq`: ask whether the absence carries meaning before you paper over it.

## Two Rules That Outrank Any Strategy

**Fit on train, apply to test.** Every imputer in scikit-learn separates `fit` (learn the fill value) from `transform` (apply it). The reason is leakage: if you compute the median over the *entire* dataset before splitting, your test set's values have leaked into your training pipeline, and your reported accuracy is inflated. Fit the imputer on training data only; carry the learned values to validation and test. This is mechanical, and it is where the casual `df.fillna(df.median())` fails silently — it has no notion of train versus test. [High]

**Imputation is a hypothesis, not a fact.** Every filled cell is a guess. The honest pipeline records which cells were imputed (that is what the indicator columns are for) and, where inference matters, acknowledges that the uncertainty is now understated. For pure prediction you can often tolerate this; for any analysis where you report an effect size or a confidence interval, single imputation's collapsed variance will bite you, and multiple imputation — pooling several imputed datasets — is the more honest tool. Disputed in the literature, settled in practice: simple imputation can be competitive for prediction and poor for inference. [High]

## The Imputation Comparison Grid

Here is the artifact this chapter carries forward — the same five-column shape the book uses for every cleaning decision, applied to the columns above.

| Column | Mechanism (evidence) | Action | Assumption introduced | Validation check |
|---|---|---|---|---|
| `mths_since_last_delinq` | MNAR — blank = never delinquent | Add `had_delinquency` flag + sentinel fill | Absence is meaningful and orderable | Default rate differs by flag value |
| `emp_length` | MAR — tracks `annual_inc`, `home_ownership` | Group-wise median or `IterativeImputer` | Observed fields predict the missing one | Imputed distribution ≈ observed distribution within groups |
| `revol_util` | MCAR — scattered, no pattern | Median fill (+ optional flag) | Observed values are a fair sample | Pre/post distribution barely shifts |
| `annual_inc` | Errors→NaN (Ch. 4) | Median or model-based, fit on train | Implausible values were truly errors | Filled values are domain-plausible |

The grid forces the discipline: you cannot fill the cell until you have written down *why* it was empty. The mechanism column is the human's job; the action column is where the AI writes the code.

## Exercises: Filling Without Lying

**1. Watch the variance collapse.** Take any numeric column with missingness. Compute its variance, mean-impute it, recompute the variance. Report the drop and explain, in one sentence, what that drop does to a standard error you might report later.

**2. The MNAR test.** Build the `had_delinquency` flag, then compare `loan_status` outcome rates for borrowers with the flag on versus off. If the rates differ, you have just proven the missingness was informative — and that mean imputation would have destroyed a real predictor. Report the two rates.

**3. MAR done two ways.** Impute `emp_length` with (a) the global median and (b) the within-`home_ownership` median. Compare the resulting distributions. Argue which is more defensible and name the assumption each one makes.

**4. Make the AI defend the default.** Ask Claude Code to "impute all missing values" with no further instruction. Read what it produces. Then write a short critique: which columns did it get right, which mechanism did it ignore, and where would its default have inverted a signal? The exercise is to catch the plausible-looking wrong answer.

## A Bridge to Structural Cleaning

Three times in this chapter the work stalled on a problem that was not about missingness at all. `IterativeImputer` needed `emp_length` as a number, but the raw column reads `"10+ years"`. The median fill needed `revol_util` as a float, but the raw column reads `"45.3%"`. You cannot impute a string. Before you can decide *what value* belongs in an empty cell, the column has to be the right *type* — a number stored as a number, a category stored consistently, whitespace stripped, the schema honest about what each column is. That is the next chapter: turning the file's text-shaped numbers and inconsistent labels into the tidy shape every downstream step silently assumes.

> ### The AI Wayback Machine: Donald Rubin
>
> In 1976, **Donald Rubin** published a short paper in *Biometrika* that did something deceptively simple: it gave names to the *reasons* data goes missing. Missing completely at random, missing at random, missing not at random — three mechanisms that, before Rubin, were lumped together as "holes in the data." His insight was that you cannot choose a fix until you understand the cause, because the cause determines whether a fill is harmless, helpful, or a fabrication. [High]
>
> That is exactly the lesson the LendingClub `mths_since_last_delinq` column teaches. The 60% of rows that are blank are not missing by accident; they are blank *because the borrower was never delinquent* — Rubin's MNAR, where the missingness depends on the value itself. Mean-fill it and you erase the signal. Flag it and you keep it.
>
> A useful prompt for an AI assistant: *"Using Donald Rubin's MCAR/MAR/MNAR framework, classify the missingness in each of these LendingClub columns and explain which imputation strategy each mechanism warrants — and where mean imputation would inject a false fact."* The assistant can write the imputer in seconds. Rubin's framework is what tells you, the human, whether the imputer is filling a hole or digging one. [High]

## Sources

- Rubin, D. B. (1976). "Inference and Missing Data." *Biometrika*, 63(3), 581–592. DOI: 10.1093/biomet/63.3.581. — The MCAR/MAR/MNAR framework; foundation for matching strategy to mechanism. [High]
- Little, R. J. A., & Rubin, D. B. (2019). *Statistical Analysis with Missing Data* (3rd ed.). Wiley. — Standard reference; what can be stated confidently versus what requires modeling assumptions. [High]
- van Buuren, S. (2018). *Flexible Imputation of Missing Data* (2nd ed.). CRC Press. — Chained-equations (MICE) workflow and practical guidance. [High]
- scikit-learn developers (current). "Imputation of missing values." *scikit-learn User Guide.* — `SimpleImputer`, `IterativeImputer`, `KNNImputer`, `MissingIndicator`; verify API behavior in your environment. [Medium]
