# Outlier Detection: The Judgment a Boxplot Cannot Make

You ask Claude Code to profile the income column of the LendingClub loan file, and the summary comes back fast: `annual_inc` ranges from `0` to `9500000`, with a median near `65000` and a mean dragged well above it. Buried in the tail are a handful of borrowers reporting more than two million dollars a year. At the very bottom sit rows with an income of exactly `0`. [verify against the actual LendingClub file]

A naive reading says: trim the tail, drop the zeros, move on. The boxplot agrees. Run `df['annual_inc'].plot.box()` and the whiskers strangle the bulk of the distribution into a thin band while dozens of points float far above as flagged outliers. The chart looks decisive.

It is not. It cannot be. Because the question the boxplot answers — *which points lie far from the center?* — is not the question you actually need answered. The question you need answered is: *which of these extreme values are real, and which are wrong?* A surgeon really does earn $1.2 million. A loan applicant who fat-fingered an extra digit really does report `9999999`. Both sit in the same region of the tail. The IQR rule cannot tell them apart, because the difference between them is not statistical. It is about the world.

This is the chapter where the book's spine becomes unavoidable. AI writes the diagnostic. You decide what the diagnostic *means*.

## Why Outliers Are a GIGO Problem, Not a Cleaning Chore

The garbage-in-garbage-out principle says model quality is bounded by data quality. Outliers are where that bound bites hardest, because a single extreme value can move a mean, inflate a variance, dominate a regression coefficient, or set the scale of a standardization step that touches every other feature. [High] Frank Hampel's robust-statistics tradition formalized exactly this: some estimators are *sensitive* to a single contaminating point, others are *resistant*, and the difference matters enormously when your data is dirty. [High]

But sensitivity cuts both ways. If you treat every extreme value as contamination and delete it, you have not cleaned the data — you have edited reality to match your model's comfort zone. The $1.2 million surgeon is the *most informative* applicant in the file for understanding high-income default behavior. Drop her and you have made your model worse at precisely the prediction it most needs to get right. John Tukey, who gave us the boxplot in *Exploratory Data Analysis* (1977), was explicit that flagged points are *candidates for investigation*, not automatic deletions. [High] The boxplot is a question, not a verdict.

So the work of this chapter is not "find and remove outliers." It is: build the diagnostic, then exercise the judgment the diagnostic cannot supply.

## Profiling the Suspect Columns

Start by looking, not deciding. The LendingClub file has several right-skewed numerical columns where extremes live: `annual_inc`, `loan_amnt`, and `revol_bal`. [verify against the actual LendingClub file] Skew matters because the symmetric intuition behind "outlier = far from the mean" breaks down the moment a distribution has a long right tail. In a skewed distribution, the tail is *supposed* to be long.

```python
import pandas as pd

df = pd.read_csv("loans.csv", low_memory=False)

for col in ["annual_inc", "loan_amnt", "revol_bal"]:
    s = pd.to_numeric(df[col], errors="coerce")
    print(f"\n=== {col} ===")
    print(s.describe(percentiles=[.01, .25, .5, .75, .95, .99, .999]))
    print("skewness:", round(s.skew(), 2))
```

Read the percentiles before you read the max. For `annual_inc`, you will typically see a 99th percentile in the low-to-mid six figures and a maximum orders of magnitude higher — the signature of a few extreme values sitting far past the bulk of the distribution. [Medium] [verify against the actual LendingClub file] The skewness will be well above 1, confirming the right tail is real, not an artifact.

This is the first judgment fork. A high skew tells you that a symmetric outlier rule (mean ± 3 standard deviations) will misfire, because the mean and standard deviation are themselves distorted by the tail. You reach instead for resistant tools.

## Three Detectors, Three Different Stories

Let Claude Code generate the standard battery, but understand that each detector encodes a different assumption about what "normal" means.

```python
import numpy as np

def flag_outliers(s):
    s = pd.to_numeric(s, errors="coerce").dropna()

    # 1. Z-score: assumes roughly symmetric, uses mean and SD
    z = (s - s.mean()) / s.std()
    z_flags = (z.abs() > 3).sum()

    # 2. IQR / Tukey fences: resistant, distribution-free
    q1, q3 = s.quantile(.25), s.quantile(.75)
    iqr = q3 - q1
    lo, hi = q1 - 1.5 * iqr, q3 + 1.5 * iqr
    iqr_flags = ((s < lo) | (s > hi)).sum()

    # 3. Modified Z (median absolute deviation): most resistant
    med = s.median()
    mad = (s - med).abs().median()
    mod_z = 0.6745 * (s - med) / mad
    mad_flags = (mod_z.abs() > 3.5).sum()

    return pd.Series({"z>3": z_flags, "iqr": iqr_flags, "mad": mad_flags})

print(flag_outliers(df["annual_inc"]))
```

On a right-skewed column the three will disagree, sometimes wildly. The z-score, fooled by the inflated standard deviation, may flag *fewer* points than you expect — the very extremes that bloat the SD also widen the threshold. The IQR rule, resistant to the tail, flags more. The MAD-based modified z-score, the most resistant of the three, flags the most. [Medium]

Here is the trap, and it is a GIGO trap: the temptation is to pick the detector that flags the "right" number of points and call it objective. But there is no objective number. Each detector is answering "how far is far?" with a different, defensible definition. The choice among them is *your* choice, and it should be driven by what the column means, not by which output looks tidiest.

For `annual_inc`, the IQR or MAD rule is more honest than the z-score, precisely because the column is skewed. But none of them has yet told you the one thing you need: which flagged points are *errors*.

It is worth being precise about why the z-score misfires here, because the failure is instructive rather than incidental. The z-score is `(value − mean) / standard_deviation`, and both the mean and the standard deviation are computed from the data — including the very extremes you are trying to flag. A single `9999999` in `annual_inc` does not just sit far from the center; it drags the center toward itself and inflates the standard deviation so that the threshold `mean ± 3·SD` widens to accommodate it. The estimator the detector relies on has been corrupted by the thing it is supposed to detect. This is the practical face of Hampel's distinction between sensitive and resistant statistics: the mean and standard deviation have a breakdown point of zero — a single bad value can move them without limit — while resistant statistics tolerate a substantial fraction of contamination before they break (the median withstands up to half the data being corrupted; the quartiles that define the IQR withstand up to a quarter). [High] On clean, symmetric data the difference is academic. On a skewed column with a few data-entry errors, it is the difference between a detector that works and one that hides the worst offenders inside its own widened fence.

A second-order point, easy to miss: anomaly-detection algorithms more sophisticated than these three — isolation forests, local outlier factor, one-class SVMs — change the math but not the epistemics. They can flag which points are unusual with more nuance, especially across many columns at once. None of them can tell you whether an unusual point is a real rare event or a mistake, because that distinction does not live in the numbers. It lives in how the data was generated. Reaching for a fancier detector when the real problem is "I don't know whether `9999999` is a typo" is solving the wrong problem with more compute. [Medium]

## The Ambiguous Tail: Where Judgment Lives

Pull the flagged extremes and look at them as rows, not as numbers.

```python
inc = pd.to_numeric(df["annual_inc"], errors="coerce")
extremes = df.loc[inc > inc.quantile(.999),
                  ["annual_inc", "emp_title", "loan_amnt", "purpose", "grade"]]
print(extremes.sort_values("annual_inc", ascending=False).head(20))
```

Now the difference that no detector could see becomes visible to a human. You will likely find two distinct populations sharing the same tail [Medium] [verify against the actual LendingClub file]:

**Plausibly real.** A borrower reporting `$450,000` with `emp_title` of "Anesthesiologist," requesting an `$8,000` loan to consolidate credit cards, graded A. Every field is internally consistent. High earners exist. This is signal.

**Plausibly an error.** A borrower reporting `$9,999,999` — a number that screams *placeholder*, a field someone filled with all nines to get past a form validation — with an `emp_title` like "teacher" and a loan request that makes no sense against that income. Or a row with `annual_inc` of exactly `0` requesting a $20,000 loan, which a lender would never originate. This is noise.

The detectors put both rows in the same bucket. Only domain knowledge separates them. The question "is $9,999,999 a real income?" is not a question about the column. It is a question about how the LendingClub application form behaved, what validation it enforced, and what a human applicant does when a required field blocks submission. *Every cleaning action answers a question about the world, not a question about syntax.*

![A right-skewed income histogram with a detector fence at the 99.9th percentile; the flagged tail beyond it is shaded red and contains two points side by side — a plausibly real 450,000-dollar anesthesiologist and a 9,999,999 all-nines placeholder error — that no statistical detector can tell apart.](images/04-outlier-detection-fig-01.png)

*Figure 4.1 — A single flagged tail holds both a genuine high earner and an all-nines data-entry error; the detector marks the region, but only domain judgment separates real from wrong.*

This is the irreducible human layer. You can ask Claude Code to surface the rows, sort them, join `emp_title` against `annual_inc` for plausibility, even draft a rule. You cannot ask it to *know* that nine-nines means "I gave up on the form." That inference requires a model of how the data was generated, and that model lives in your head, informed by how lending applications work.

## From Flag to Decision: The Four Moves

Once you have looked, you have four defensible responses, and the right one depends entirely on what the value means and what your model is for.

![A decision fan branching from a single flagged extreme value into four moves — retain, correct, convert to missing shown in red as the workhorse, and cap — each labeled with the claim about the world it asserts, while delete-row is demoted and crossed out as a non-default.](images/04-outlier-detection-fig-02.png)

*Figure 4.2 — Four defensible moves on a flagged extreme, each asserting a different claim about the world; convert-to-missing (red) is the underused workhorse, and deleting the row is not a default.*

**Retain.** The $450,000 anesthesiologist stays. It is real and informative. Deleting real extremes to make a distribution prettier is data falsification dressed up as cleaning.

**Correct.** Where you have ground truth, fix the value. Rarely available in a raw extract, but if `annual_inc` is `0` and `emp_length` is "10+ years" with a healthy `loan_amnt`, you may have provenance to repair it. Usually you do not — which pushes you to the next move.

**Convert to missing.** This is the workhorse and it is underused. The `9999999` and the `0` are not credible incomes; treating them as *missing* hands them to your imputation strategy (Chapter 5) rather than forcing a binary keep/delete. You are saying: "I do not believe this value, but I do not want to throw away the rest of the row." This is almost always better than deletion, because the borrower's `grade`, `purpose`, and `loan_amnt` may still be valid.

```python
# Convert implausible incomes to NaN, preserve the rest of the row
mask_impossible = (inc == 0) | (inc >= 9_000_000)   # form-error signatures
df.loc[mask_impossible, "annual_inc"] = np.nan
print(f"Converted {mask_impossible.sum()} implausible incomes to NaN "
      f"for downstream imputation.")
```

**Cap (winsorize).** For a model where you want to keep the row's influence but limit a single point's leverage, cap at a percentile. Use this sparingly and document it, because it changes real values: a $2M income capped to the 99th percentile is now reporting a lie you introduced.

Notice that *delete the row* is not on the list as a default. Deletion is the most destructive option and the most casually chosen. Reserve it for rows that are corrupt across multiple fields, not for a single extreme value in one column. There is a quiet bias hiding in casual deletion, too: if you drop every high-income row "to clean the tail," you are not removing errors at random — you are systematically removing the wealthiest applicants, and any model trained on what remains will be biased toward the middle of the income distribution. The deletion looks neutral. Its effect is not. This is how a cleaning step that nobody documented becomes a fairness problem nobody can trace.

### Outliers Are Contextual, Not Just Univariate

So far every detector has looked at one column in isolation. But some of the most informative outliers are not extreme in *any single* column — they are extreme in the *combination*. A reported `annual_inc` of `$40,000` is unremarkable. A `loan_amnt` of `$35,000` is unremarkable. The two *together* — a borrower asking to borrow nearly a full year's income — is a contextual outlier that a univariate scan will never flag. The same logic runs the other way: an income of `$30,000` paired with a `revol_bal` of `$200,000` is internally implausible in a way neither field reveals alone.

```python
# A simple contextual diagnostic: loan size relative to income
ratio = pd.to_numeric(df["loan_amnt"], errors="coerce") / \
        pd.to_numeric(df["annual_inc"], errors="coerce").replace(0, np.nan)
print(ratio.describe(percentiles=[.95, .99, .999]))
# rows where the ask dwarfs the income are worth a human look
print(df.loc[ratio > 1.0, ["annual_inc", "loan_amnt", "purpose", "grade"]].head())
```

The lesson is not that you must build a multivariate detector for every pair of columns — that way lies combinatorial paralysis. The lesson is that "is this value an outlier?" is the wrong question when the real risk is "is this *row* coherent?" Whether a $40k borrower asking for $35k is an error, a desperate applicant, or a perfectly normal debt-consolidation case is, once again, a question about the world. The ratio surfaces the candidates. You decide what they mean.

### Provenance Beats Statistics

One more discipline, and it is the one practitioners skip most: before you decide an extreme value is an error, ask *where the column came from*. `annual_inc` on LendingClub is self-reported by the borrower and, for many loans, never verified — which makes both the genuine extremes and the placeholder errors more likely than they would be in an audited field. [Medium] A column populated by a sensor, a transaction system, or an audited ledger has a different error profile from a column a stressed human typed into a web form to get a loan. The same numeric value — say, a suspiciously round `$500,000` — means different things depending on whether a human could have typed it or a machine recorded it. No detector knows the provenance. You do, or you can find out by reading the data dictionary. The provenance is the prior that turns a flag into a decision.

### Before and After

| State | `annual_inc` rows | What a regression "sees" |
|---|---|---|
| Raw | `0`, `9999999`, `450000`, `65000`… | Mean inflated; a single `9999999` dominates the income coefficient; `0` pulls the low end into nonsense |
| Naive (delete all IQR outliers) | `65000`-ish only | The $450k surgeon is gone; model is now blind to real high earners — *new* GIGO introduced |
| Judged | `0`→NaN, `9999999`→NaN, `450000` retained, `65000` retained | Errors handed to imputation; real extremes preserved; the distribution is honest |

The middle row is the one that gets shipped most often, and it is worse than doing nothing, because it looks like cleaning while quietly deleting the most informative observations in the file.

## The Ambiguous-Extreme-Value Case Table

The artifact this chapter produces — and that you carry forward across the book — is a small table that records the *decision*, not just the flag. The boxplot is the question; this table is the answer, and crucially it records the reasoning so a reviewer (or future you) can audit it.

| Column | Extreme value | Detector flag | Plausibility evidence | Decision | Risk retained |
|---|---|---|---|---|---|
| `annual_inc` | `9999999` | IQR, MAD | All-nines placeholder; `emp_title`="teacher" | → NaN (impute) | May lose a genuine rare earner |
| `annual_inc` | `450000` | IQR | `emp_title`="Anesthesiologist", grade A, small loan | Retain | Leverage on income coefficient |
| `annual_inc` | `0` | MAD | Impossible for an originated loan | → NaN (impute) | None meaningful |
| `revol_bal` | very high | IQR | Consistent with high `loan_amnt` | Retain | High variance in feature |

Fill one row per genuinely ambiguous case. The discipline is not the table's format; it is forcing yourself to write down the evidence *before* the decision. A flag with no recorded evidence is a guess wearing a lab coat.

## Exercises: Reading the Tail

**1. The two populations.** Pull the top 0.1% of `annual_inc`. Sort by income and read across `emp_title`, `loan_amnt`, and `grade`. Write one sentence per row classifying it as plausibly-real or plausibly-error, and state the evidence. You should find you cannot do this from the number alone.

**2. Detector disagreement.** Run the z-score, IQR, and MAD detectors on `loan_amnt`. They will disagree less than on `annual_inc` (loan amounts are capped by the platform). Explain *why* the disagreement shrinks, and what that tells you about which detector to trust for a bounded versus an unbounded column.

**3. The deletion cost.** Fit a simple model predicting `loan_status` with and without the real high-income extremes retained. Report how the income coefficient changes. Argue, in two sentences, whether the change makes the model better or worse — and note that "the metric improved" is not automatically "the model is better."

**4. Write the rule, own the threshold.** Have Claude Code draft a function that converts implausible incomes to NaN. Then change the threshold from `9_000_000` to `1_000_000` and explain what real borrowers you would now be erasing. The point is that the threshold is a judgment, and the AI cannot choose it for you.

## A Bridge to Imputation

When you converted `9999999` and `0` to `NaN`, you did not solve a problem — you *moved* it. Those cells are now missing, and they joined the missingness you already mapped in Chapter 3. But they are a special kind of missing: they are missing *because you decided the original value was a lie.* That provenance matters for what you do next. An income that is missing because the applicant skipped the field is not the same as an income that is missing because you rejected `9999999`. The next chapter asks the question those NaN cells now force: *given how a value went missing, what is the least wrong way to fill it?* And it shows, on this exact column, why the most popular answer — mean imputation — is demonstrably wrong.

> ### The AI Wayback Machine: John Tukey
>
> Long before "data science" had a name, **John Tukey** (1915–2000) insisted that the first job of an analyst was to *look* at the data, not to test it. His *Exploratory Data Analysis* (1977) gave us the boxplot, the stem-and-leaf display, and the word "bit" — but its deeper gift was a stance: that a flagged extreme value is a *prompt to investigate*, never an instruction to delete. Tukey distrusted summaries that hid their own assumptions, which is exactly the distrust you need when a boxplot strangles the LendingClub income distribution and presents you with a wall of flagged points.
>
> Ask an AI assistant to channel that stance. A useful prompt: *"Explain how John Tukey's approach to exploratory data analysis would change how I treat the flagged extreme values in the LendingClub `annual_inc` column — specifically, why I should investigate before I delete."* The answer you want is not code. It is the reminder that the resistant summary, the visual diagnostic, and the human eye on the raw rows are three steps toward a decision — and that the decision is still yours. Tukey built the tools that make the question visible. He never pretended the tools could answer it. [High]

## Sources

- Tukey, J. W. (1977). *Exploratory Data Analysis.* Addison-Wesley. — Boxplots and the stance that flagged extremes are candidates for investigation, not automatic deletions. [High]
- Hampel, F. R. (1974). "The Influence Curve and Its Role in Robust Estimation." *Journal of the American Statistical Association.* — Why some estimators are sensitive to single contaminating points and others resistant. [High]
- Barnett, V., & Lewis, T. (1994). *Outliers in Statistical Data* (3rd ed.). Wiley. — Outlier treatment depends on the data-generating context. [High]
- Sambasivan, N., et al. (2021). "Everyone wants to do the model work, not the data work: Data Cascades in High-Stakes AI." *CHI.* — Under-valued data work produces downstream failures; grounds the GIGO frame. [High]
- pandas / scikit-learn documentation (current). — `describe`, quantile methods, and outlier-handling APIs; verify exact behavior against your project environment. [Medium]
