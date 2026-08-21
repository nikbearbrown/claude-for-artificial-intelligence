# Scaling and Transformation

A loan officer once told me she could spot a bad applicant by the shape of their pay stub. Not the number — the shape. Most people earned somewhere in a tight band. A few earned wildly more. The ones who worried her were the ones whose stated income sat far out in the tail, alone, unexplained.

She was describing a skewed distribution without using the word. And she was describing the exact problem you face the moment you open the LendingClub file and try to feed `annual_inc` to a model.

You have spent seven chapters making this dataset *correct*: missing values handled, outliers judged, types fixed, categories encoded. The data is now true. It is not yet *usable*. Two things are wrong with it as numbers — not as facts, as numbers. Some columns are violently skewed, with a long right tail that drags every average and squashes every plot. And the columns live on scales that have nothing to do with each other: `annual_inc` runs into six figures, `dti` sits between 0 and roughly 40, `loan_amnt` runs into the tens of thousands. A model that measures distance — anything with a regularizer, anything with gradient descent, anything that computes a Euclidean norm — will hear the loud columns and go deaf to the quiet ones.

This chapter is about fixing both. But the spine of the chapter is a single discipline: **check before you transform.** A log transform is not a tidying habit you apply to every numeric column. It is a claim about the world — that the variable's *ratios* matter more than its *differences*, that a jump from \$30k to \$60k is the same kind of event as a jump from \$300k to \$600k. Sometimes that claim is true. Sometimes it is exactly backwards. The skill is telling which.

## The Diagnosis Comes First

Here is the failure, made concrete. You ask AutoData — your Claude Code session pointed at the LendingClub CSV — to "scale the numeric columns for modeling," and it cheerfully standardizes everything and maybe logs a few. The code runs. No error. You have just possibly destroyed a near-normal column by logging it, and you have no record of *why* anything was done.

Resist. Diagnose first. The two numbers you want are the **skewness** of each column and a look at its **histogram**. Skewness measures asymmetry: a value near 0 means roughly symmetric, positive means a long right tail (the income case), negative means a long left tail. A common rule of thumb treats skewness above about 1 (or below −1) as "substantially skewed" and a candidate for transformation [Medium — this threshold is a convention, not a law; it appears in many applied texts but the exact cutoff varies].

```python
import pandas as pd
import numpy as np

df = pd.read_csv("lending_club.csv")  # the cleaned file from Chapter 6/7

numeric_cols = ["annual_inc", "loan_amnt", "revol_bal", "dti",
                "int_rate", "open_acc"]  # [verify against the actual LendingClub file]

skew_report = (
    df[numeric_cols]
    .skew()
    .sort_values(ascending=False)
    .rename("skewness")
    .to_frame()
)
print(skew_report)
```

Read the report top to bottom. The columns at the top — the ones with the largest positive skewness — are your transformation candidates. In the LendingClub data these are the money columns and a count column: `annual_inc`, `revol_bal`, `loan_amnt`, and a count like `open_acc` (number of open credit lines) [verify against the actual LendingClub file]. Income, in particular, is the textbook right-skewed variable: most borrowers cluster in a band, a few report enormous incomes, and the mean sits well above the median. [High — right skew in personal-income data is one of the most reliably documented distributional facts in economics; the specific column values are dataset-specific, so verify.]

The columns near zero are the ones you leave alone. And the column with a small *negative* or near-zero skewness — `int_rate` is a plausible candidate, since interest rates are assigned from a bounded grade scale and tend to pile up in the middle [verify against the actual LendingClub file] — is the one this chapter exists to protect. Do not log it. Logging a roughly symmetric variable does not "improve" it; it *introduces* skew where there was none, and makes the feature harder for a model to use, not easier.

![A two-by-two grid of histograms: a right-skewed income column is straightened to symmetry by a log transform, while a near-symmetric interest-rate column has skew introduced by the same log, with the damaged panel flagged.](images/08-scaling-and-transformation-fig-01.png)

*Figure 8.1 — The same log transform that rescues a right-skewed income column degrades a near-symmetric interest-rate column — which is why you diagnose each column before you transform it.*

Always look at the picture, not just the number. Skewness is a single summary and can be fooled — a bimodal column can have low skewness while being deeply non-normal. Plot.

```python
import matplotlib.pyplot as plt

fig, axes = plt.subplots(2, 3, figsize=(14, 7))
for ax, col in zip(axes.ravel(), numeric_cols):
    df[col].plot.hist(bins=60, ax=ax)
    ax.set_title(f"{col}  (skew={df[col].skew():.2f})")
plt.tight_layout()
plt.savefig("transform_audit_raw.png", dpi=120)
```

This is the first panel of what the research notes call the **transform audit plot set**: the raw distribution, before you touch anything. You will produce a matching "after" panel later and put them side by side. The audit is not decoration. It is the evidence that justifies every decision — the thing you paste into the cleaning report so that six months from now, someone (possibly you) can see *why* income got logged and interest rate did not.

## Why Log, and What Log Assumes

When a variable is right-skewed and strictly positive, the natural-log transform pulls the long tail in and spreads the crowded low end out. Mechanically, it does this because the log function grows slowly: the distance from log(1,000) to log(10,000) equals the distance from log(10,000) to log(100,000). Each is a factor of ten, and log treats equal *ratios* as equal *distances*.

That last sentence is the whole assumption. Logging income says: the meaningful thing about income is *proportional* change. The difference between a \$25,000 borrower and a \$50,000 borrower (a doubling) is treated as the same size of event as the difference between \$200,000 and \$400,000 (also a doubling), even though in raw dollars the second gap is eight times larger. For income and risk, that is often the *right* claim — a doubling of income changes someone's financial life similarly at both ends, while a flat \$25,000 means everything to one borrower and nothing to the other. For a near-normal, additively-meaningful variable like an interest rate, it is the *wrong* claim, which is why you checked first.

There is one mechanical trap. Log is undefined at zero and negative numbers, and columns like `revol_bal` (revolving balance) and `annual_inc` can contain zeros [verify against the actual LendingClub file]. The standard fix is `log1p`, which computes log(1 + x) and is therefore defined at x = 0.

```python
# Log-transform the right-skewed, non-negative columns ONLY.
to_log = ["annual_inc", "revol_bal", "loan_amnt", "open_acc"]  # [verify]
for col in to_log:
    df[f"{col}_log"] = np.log1p(df[col])

# Re-check skewness after transformation.
after = df[[f"{c}_log" for c in to_log]].skew().rename("skew_after")
print(after)
```

If the transform did its job, the post-transform skewness values will have collapsed toward zero. If a value is still large, the log was not enough (you may have a genuine multi-modal column, or extreme outliers you should have handled back in Chapter 4) — and that is information, not failure. Document it.

> **A note on the AutoData reflex.** When you ask Claude Code to "handle the skew," it will often reach for `np.log` directly and crash on the zeros, or silently produce `-inf`. Watch for it. The correct instruction is specific: *"Use `log1p` only on the columns I list, which are non-negative and right-skewed; leave `int_rate` untransformed because it is approximately symmetric; then print before-and-after skewness for each."* The assistant writes the code. You supply the judgment about which columns and why. That division of labor is the entire point of the book.

## Box-Cox and Yeo-Johnson: When You Want the Data to Pick

The log transform is one member of a family. The Box-Cox transformation (Box and Cox, 1964) generalizes it: it has a parameter λ that the procedure tunes to make the result as close to normal as possible, with log emerging as the special case λ = 0. Box-Cox requires strictly positive inputs. Its cousin, the Yeo-Johnson transform, handles zeros and negatives, so it is the safer default for a messy column you have not fully scrubbed. scikit-learn exposes both through `PowerTransformer`.

```python
from sklearn.preprocessing import PowerTransformer

pt = PowerTransformer(method="yeo-johnson", standardize=False)
df["annual_inc_yj"] = pt.fit_transform(df[["annual_inc"]])
print("fitted lambda:", pt.lambdas_)  # near 0 ≈ log-like behavior
```

[Medium — `PowerTransformer` with `method="yeo-johnson"` and the `lambdas_` attribute are current scikit-learn API; verify against your installed version, since defaults and parameter names occasionally change.]

Should you prefer Box-Cox/Yeo-Johnson over a plain log? Often the plain log is fine and more interpretable — a logged income is still recognizably "income, on a ratio scale," whereas a Yeo-Johnson output with λ = 0.31 is a number only a model loves. Reach for the power transform when you genuinely want the data to choose the shape and you do not need the feature to remain human-readable. This is a real dispute in the field, not a settled rule: the research notes flag that automated, data-driven transformations can improve a metric while quietly destroying interpretability and reproducibility. Choose deliberately.

## Standardization: Putting Columns on Speaking Terms

Transformation fixes *shape*. Standardization fixes *scale*. They are different jobs and you usually do both, in that order — transform first (so the column is roughly symmetric), then standardize (so it has mean 0 and standard deviation 1).

The motivation is the scale mismatch you saw in the histograms. `annual_inc_log` now lives around 10–13; `dti` lives around 0–40; a binary flag lives at 0 or 1. Any model that adds up squared distances or penalizes coefficient size will treat the large-numbered column as more important purely because its numbers are bigger. Standardization removes the unit so that "one step" means the same thing — one standard deviation — in every column.

```python
from sklearn.preprocessing import StandardScaler

features = ["annual_inc_log", "revol_bal_log", "loan_amnt_log",
            "open_acc_log", "dti", "int_rate"]  # [verify]

scaler = StandardScaler()
X_scaled = scaler.fit_transform(df[features])
X_scaled = pd.DataFrame(X_scaled, columns=features, index=df.index)
print(X_scaled.describe().loc[["mean", "std"]].round(3))
```

Every column now reports a mean of ~0 and a standard deviation of ~1.

Two warnings the research literature insists on. First, **not every model needs this.** Tree-based methods — decision trees, random forests, gradient-boosted trees — split on thresholds one feature at a time and are invariant to monotonic rescaling. Standardizing before a random forest is harmless but pointless, and the field genuinely disputes how much routine preprocessing is worth the added complexity. Scaling matters for linear and logistic regression, SVMs, k-nearest neighbors, k-means, and neural nets; it is largely irrelevant for trees. Match the preprocessing to the model.

A third point, easy to miss: standardization is not the only scaler, and `StandardScaler` quietly assumes your column is roughly symmetric — because it subtracts the *mean* and divides by the *standard deviation*, both of which a few extreme values can yank around. That is precisely why you transform before you standardize: on a raw, skewed `annual_inc`, the standard deviation is inflated by the long tail, so "one standard deviation" becomes a meaninglessly large step and most of your borrowers get crushed into a narrow band near zero. If you have a column you deliberately chose *not* to transform but which still carries outliers, `RobustScaler` — which centers on the median and scales by the interquartile range — resists those extremes and is the better instrument. The lesson generalizes: a scaler encodes an assumption about the distribution it is fed, so the diagnosis from the top of this chapter governs the scaler choice too, not just the transform choice. [Medium — `RobustScaler` is current scikit-learn API; verify against your installed version.]

Second — and this is the beat that points straight at Chapter 11 — **fit the scaler on training data only.** The `scaler` learns a mean and standard deviation. If you `fit` it on the whole dataset before splitting, you have let the test set's statistics leak into your training pipeline. The mean of the training income is information you are allowed to use; the mean computed over data that includes the test rows is not. The correct pattern is `scaler.fit(X_train)` then `scaler.transform(X_test)`, which is exactly why scikit-learn `Pipeline` exists — to bind the scaler to the fold so it can never see what it should not. We hold that thought until Chapter 11, but plant the flag now: **scaling is a learned transformation, and learned transformations leak if you fit them too early.**

## Before and After

Put the two audit panels side by side and the work becomes legible.

| Column | Raw skewness | Action | After skewness | Why |
|---|---|---|---|---|
| `annual_inc` | high positive (e.g. ~5–10) | `log1p` + standardize | near 0 | ratios matter; long right tail; non-negative |
| `revol_bal` | high positive | `log1p` + standardize | near 0 | same logic as income |
| `open_acc` (count) | moderate positive | `log1p` + standardize | reduced | count variable, right-skewed |
| `int_rate` | near 0 | **standardize only** | unchanged | approximately symmetric — logging would *add* skew |
| `dti` | mild | standardize only | unchanged | not skewed enough to warrant a transform |

*(All skewness magnitudes above are illustrative — [verify against the actual LendingClub file].)*

The table is the deliverable. Anyone reading it can see not just what you did but the claim about the world behind each row. That is the difference between a cleaning pipeline and a cleaning *decision record*.

## Exercises: Check Before You Transform

1. **Diagnose, do not assume.** Compute the skewness and plot the histogram for every numeric column in the LendingClub file. Rank them. Predict, *before* you transform anything, which three columns will benefit most from a log and which one you must leave alone. Then transform and check whether your prediction held.

2. **Break it on purpose.** Apply `log1p` to `int_rate` (the near-normal column). Plot before and after, and report the skewness both ways. Write two sentences explaining what the log *did* to a variable that did not need it — and why "no error" is not the same as "correct."

3. **Log vs. Yeo-Johnson.** Transform `annual_inc` two ways — plain `log1p` and `PowerTransformer`. Compare the resulting skewness and the interpretability of the output. Which would you put in a model you have to explain to a credit-risk committee, and why?

4. **The leakage trap (preview).** Fit a `StandardScaler` on the full dataset, then fit a second one on a training split only, and compare the means each learned. Are they different? By how much? Write one sentence on why the second one is the only honest choice. (We make this rigorous in Chapter 11.)

## Bridge

You now have features that are correctly shaped and on a common scale. But there is a column we have been quietly ignoring while we did all this arithmetic: `loan_status`, the thing you are actually trying to predict. When you finally look at it, you will find that the borrowers who default — the ones the whole model exists to catch — are a small minority of the rows. Most loans are paid back. A model that simply predicts "paid back" every single time will be right most of the time and useless all of the time. That is the class-imbalance problem, and it is where we go next.

##  AI Wayback Machine

**George Box** was a British statistician who, with David Cox, introduced the Box-Cox family of transformations in 1964 — the formal answer to the question "what shape should this variable be?" He is also the source of the line every data scientist eventually quotes: *all models are wrong, but some are useful.*

**Run this:**

```
Who is George Box, and how does their work connect to the log and power transformations we used in this chapter? Keep it to three paragraphs. End with the single most surprising thing about their career or ideas.
```

→ Search **"George E. P. Box"** on Wikipedia.

**Now make the prompt better.** Try one of these:

- Ask it to walk through the original Box-Cox transformation in detail, including what the parameter λ actually does.
- Add a constraint: "Answer including criticisms or limits of automatically choosing a transformation to maximize normality."

What changes? What gets better? What gets worse?

## Sources

- Box, G. E. P., and Cox, D. R. "An Analysis of Transformations." *Journal of the Royal Statistical Society, Series B*, 1964. — Foundational paper for the transformation family; grounds the chapter's claim that a transform encodes an assumption about scale and error structure.
- Tukey, J. W. *Exploratory Data Analysis*. Addison-Wesley, 1977. — Canonical source for inspecting distributions visually before acting; supports "diagnose before you transform."
- Hampel, F. R. "The Influence Curve and Its Role in Robust Estimation." *Journal of the American Statistical Association*, 1974. — Technical grounding for why a column's extreme tail affects different statistics and models differently.
- Pedregosa et al. "Scikit-learn: Machine Learning in Python." *JMLR*, 2011; and the current scikit-learn documentation for `StandardScaler` and `PowerTransformer` (verify against your installed version, access date matters). — Implementation references for standardization and power transforms.
