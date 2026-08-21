# Chapter 1 — The GIGO Problem: Why Data Quality Beats Model Cleverness

## A model that learned the wrong lesson

Picture the Friday deadline from the introduction. You did the responsible thing: you built a clean pipeline, cross-validated honestly, and tried three models. The gradient-boosted classifier wins. On your held-out test set it reports **89% accuracy** at predicting whether a LendingClub loan will be charged off. You write it up, feeling good.

Then someone asks the question that should always be asked first: *how often does a loan actually get charged off?*

You go back to the data. In this slice of LendingClub, fully-paid and current loans dominate; charged-off and defaulted loans are the minority — somewhere in the neighborhood of one loan in eight. [verify against the actual LendingClub file] Which means a model that predicts "fully paid" for every applicant, that learns nothing, that is a single line of code returning a constant — that model is right roughly **87% of the time.** [verify against the actual LendingClub file]

Your 89%-accurate model beat the do-nothing baseline by about two points. And it did so, you discover when you look closer, mostly by predicting "fully paid" almost all the time. On the loans you actually care about — the defaults, the ones that lose the lender money — it is barely better than a coin flip. The accuracy number was never measuring what you thought it measured. The data's class imbalance set a trap, and the model walked straight into it. You will learn to defuse that specific trap in Chapter 9. The point here is broader: **the model did not fail. The data, unexamined, made the model meaningless.**

![A three-bar chart comparing an 87 percent majority-class baseline, an 89 percent overall model accuracy, and the same model's roughly 52 percent accuracy on the minority charged-off class shown in red, revealing the headline number hides near-chance performance where it matters.](images/01-the-gigo-problem-why-data-quality-beats-model-cleverness-fig-01.png)

*Figure 1.1 — The headline 89% sits two points above a do-nothing baseline and collapses to a coin flip on the defaults the model exists to catch.*

This is the GIGO problem. Garbage in, garbage out. And it is the reason this book spends thirteen chapters on data and none on inventing new algorithms.

## The thesis, stated plainly

**Model quality is bounded by data quality.** [High] This is the spine of the book, and it deserves to be stated as precisely as possible.

It does *not* mean that data is more important than models in some vague, motivational sense. It means something structural: the information your model can possibly extract is limited by the information actually present, correctly, in the training data. A model is a function that maps inputs to outputs by finding patterns. If the patterns in the data are artifacts of how the data was collected — a units error, a mislabeled target, a missingness pattern that correlates with the outcome — the model will find those artifacts and reproduce them, because it cannot tell the difference between a real pattern and a defect that looks like one.

There is a comforting fantasy in machine learning that a sufficiently powerful model will "see through" the noise. Sometimes, with enough data, it averages out random noise. But most data-quality problems are not random noise. They are *systematic*. A column where income is sometimes in dollars and sometimes in thousands of dollars is not noisy; it is bimodal in a way that encodes a hidden categorical variable (which data-entry convention was used) that has nothing to do with the borrower. No amount of model capacity recovers the truth, because the truth was destroyed before the model ever saw it.

This is why we say **the ceiling is set before you choose the model.** Cleverness in the machinery cannot exceed the quality of the material. A master carpenter cannot build a sound table out of rotten wood; they can only build a more impressive-looking rotten table.

### Why a better model cannot rescue you

It is worth being precise about *why* model sophistication does not help, because the intuition that "a bigger model will figure it out" is seductive and wrong in a specific, instructive way.

A supervised model learns a relationship between inputs `X` and a target `y` from examples. It has access to exactly one thing: the values in the file. It has no access to the world those values were supposed to measure. So when a value is wrong — when `annual_inc` reads `48` because someone entered thousands of dollars, or when a charged-off loan is mislabeled "Fully Paid" — the model sees a *valid training example* and dutifully adjusts its parameters to fit it. The error is not filtered out as implausible; it is *learned*. A more flexible model with more capacity does not learn the error less. It learns it *better*, fitting the corrupted point more precisely than a simple model would. This is the cruel inversion at the heart of GIGO: against systematic data errors, **model power is a liability, not an asset.** [High]

Random errors can sometimes wash out because they are uncorrelated with the target — the model averages over them. Systematic errors do not wash out, because they correlate with something. A units convention that varies by data-entry vintage correlates with *when* the loan was issued, which correlates with economic conditions, which correlates with default. The model finds that chain of correlations and reports it as insight. You ship a model that has, in effect, learned to predict default from a clerk's keyboard habits. No held-out test set catches this, because the test set has the same defect. The only thing that catches it is a human who looked at the income column and asked why some values were a thousand times smaller than the rest.

## Data cascades: why this keeps happening

If the GIGO principle is so obvious, why is it violated constantly, in well-funded teams, in production systems that matter?

The most useful answer comes from a 2021 study by Nithya Sambasivan and colleagues at Google, who interviewed AI practitioners working on high-stakes systems — healthcare, conservation, finance — and documented a recurring failure pattern they named **data cascades**: "compounding events causing negative, downstream effects from data issues, that result in technical debt over time" (Sambasivan et al., 2021). [High]

The shape of a cascade is always the same. An upstream data problem is small, cheap to fix, and invisible — a units inconsistency, an undocumented missing-value convention, a label collected sloppily. Because it is invisible, nobody fixes it. It flows downstream into modeling, where it is amplified. It surfaces eventually — in a bad prediction, a biased outcome, a deployment that quietly fails — at which point it is expensive, entangled, and hard to trace back to its origin. Often the team responds by adding model complexity to paper over a data problem, which makes the cascade worse.

The study's most-quoted finding is in its title: *Everyone wants to do the model work, not the data work.* [High] The researchers found that data work was systematically undervalued — described by practitioners themselves as "grunt work," rewarded less than modeling, and starved of tools and time. The incentives point at the model. The risk lives in the data. That mismatch is the engine of the GIGO problem, and naming it is the first step to resisting it.

> **Why this matters for you, specifically.** As a first-job data scientist, you are most likely to be *handed* the data, not to have collected it. You are downstream of decisions you did not make and cannot see. The discipline this book teaches — profile before you trust, ask why before you fix, document every assumption — is exactly the discipline that catches a cascade before it compounds.

To make the shape vivid, trace one plausible cascade through the LendingClub data. Upstream, the `desc` free-text field — borrowers' written explanations of why they want the loan — was collected for early loans and quietly dropped for later ones. [verify against the actual LendingClub file] That is a small, invisible fact about data collection. A modeler in a hurry includes `desc`-derived features (does the borrower mention "medical," "debt," "wedding"?) because, on the loans where `desc` exists, those features predict default beautifully. The features work — on the old loans. But `desc` is blank for the recent loans, which are exactly the ones the deployed model will score. In production, the powerful text features are always empty, the model leans on whatever is left, and its real-world performance silently collapses below what the test set promised. The defect was free to fix at the start (notice `desc` is era-dependent, decide not to depend on it). By the time it surfaces as degraded production accuracy, it is buried under a pipeline, a dashboard, and a quarter of decisions made on bad scores. That is a cascade: cheap upstream, expensive downstream, and invisible until it is not.

![A left-to-right four-stage flow tracing a data cascade from a cheap upstream defect through modeling and pipeline amplification to a red final stage where the failure surfaces in production, with a rising cost track above and falling visibility below.](images/01-the-gigo-problem-why-data-quality-beats-model-cleverness-fig-02.png)

*Figure 1.2 — The same defect costs almost nothing to fix upstream and a quarter of bad decisions to find downstream; only its price changes as it flows.*

## Three kinds of defects, and which ones are yours

Open a real file and the defects come in three flavors. Sorting them is the first analytical move.

**Mechanical defects** are about format. The interest rate `13.49%` is stored as text; the term ` 36 months` has a leading space and units baked in; the employment length `10+ years` is a string that hides an ordinal number. These are unambiguous and have correct fixes. An AI assistant can resolve them well, because the question — *how do I turn this string into a number?* — is a question about syntax. We tackle these in Chapter 6.

**Analytical defects** are about distribution and structure. The `loan_status` target is imbalanced; `annual_inc` and `revol_bal` are heavily right-skewed; `mths_since_last_delinq` is missing for most rows. These are not "wrong" — they are properties of the data that will mislead a model if you do not handle them deliberately. The fix requires statistical reasoning, and the right choice depends on what you intend to do downstream.

**Judgment defects** are about meaning, and they are irreducibly yours. Is `annual_inc` of $9,500,000 a real high earner or a misplaced decimal? Is a blank in `mths_since_last_delinq` an error, or does it mean *this borrower has never been delinquent* — a fact so informative you would be foolish to throw it away? Is the difference between `emp_title` values "RN" and "Registered Nurse" two jobs or one? No tool can answer these, because the answer is not in the data. It is in the world the data is *about*.

The reason this distinction matters is that the AutoData workflow can largely automate the first category, can assist with the second under your supervision, and **cannot touch the third without you.** When you find yourself letting the assistant decide a judgment defect, you have lost the plot.

## The human-judgment layer

Let us make the irreducible part concrete, because it is easy to nod along to "judgment matters" and then quietly outsource it anyway.

An AI coding assistant, prompted well, will profile `annual_inc`, notice the long right tail, and report that there are values above $1,000,000. It might even suggest, helpfully, that you cap income at the 99th percentile to "handle outliers." That suggestion is **code masquerading as a decision.** Capping income asserts that incomes above the cap are not real — that a borrower reporting $2,000,000 is an error to be flattened toward the herd. For some lenders that is exactly wrong: high-income, high-loan-amount borrowers are a real and important segment. For others, with a population where seven-figure incomes are implausible, the cap is sensible. The assistant cannot know which world you are in. *You* have to know.

Here is the principle in its operational form, the one to internalize:

> **Every cleaning action answers a question about the world, not just a question about syntax.**

- Drop a row → you assert that row does not represent a valid observation.
- Fill a blank with the mean → you assert the blank means "typical."
- Fill a blank with a sentinel and a flag → you assert the *fact of missingness* is itself informative.
- Cap an outlier → you assert values beyond the cap are not real events.
- Merge two categories → you assert the distinction between them does not matter for your purpose.

Each of these is a claim about reality, and each can be wrong. The AI writes the line of code in seconds. You own the claim forever. The research literature is blunt about this: data work is consequential and assumption-laden (Sambasivan et al., 2021), and the assumptions do not announce themselves. Your job is to make them visible.

### Three things the assistant cannot decide

It helps to name the categories of decision that stay human no matter how good the tooling gets, because they recur in every chapter of this book.

*Is this missing value ignorable?* A blank in `mths_since_last_delinq` might mean "we lost the value" or "this borrower has never been delinquent." Those readings demand opposite handling — impute in the first case, flag-and-preserve in the second — and the data does not say which is true. Only knowledge of how the field was defined does. (We spend all of Chapter 3 on this.)

*Is this extreme value a real event or an error?* An `annual_inc` of $250,000 on a small personal loan might be a surgeon or a typo. A `revol_bal` ten times the median might be a real heavy borrower or a units glitch. Removing real extremes throws away the most informative rows; keeping real errors poisons the model. The statistic that flags the value is automatic; the verdict on each value is not. (Chapter 4.)

*Does this category distinction matter?* Are `home_ownership` values "MORTGAGE" and "OWN" meaningfully different for predicting default, or should they collapse? Is `emp_title` "RN" the same job as "Registered Nurse"? Merging categories simplifies the model and can erase signal; splitting them preserves signal and can shatter it into noise. The right answer depends on what you are modeling and why. (Chapters 6 and 7.)

In every case the assistant can compute, plot, and propose. It cannot be *accountable*, and accountability is the thing a decision actually requires. When a loan is denied because of your cleaned data, a regulator does not interview the model. They interview you.

## A first AutoData session

Let us do the responsible version of the Friday task: before any modeling, profile the target. This is the AutoData pattern — you prompt the assistant, it generates code, you read the code and the result, and *you* draw the conclusion.

You might prompt Claude Code with something like:

> *Load the LendingClub CSV. Show the distribution of `loan_status`, collapse it into a binary "charged off vs. fully paid" target, and compute what accuracy a majority-class baseline would get.*

The generated code is ordinary pandas — and you should read every line of it, because reading it is how you keep the judgment:

```python
import pandas as pd

loans = pd.read_csv("lending_club.csv", low_memory=False)

# What does the raw target actually look like?
print(loans["loan_status"].value_counts(dropna=False))

# Judgment call: which statuses count as "bad"? This is YOURS, not the tool's.
# "Charged Off" and "Default" are clear losses. "Current" is unresolved —
# we exclude it because its outcome is not yet known.
bad = ["Charged Off", "Default"]
resolved = loans[loans["loan_status"].isin(bad + ["Fully Paid"])].copy()
resolved["charged_off"] = resolved["loan_status"].isin(bad).astype(int)

rate = resolved["charged_off"].mean()
print(f"Charged-off rate among resolved loans: {rate:.1%}")
print(f"Majority-class baseline accuracy:      {max(rate, 1 - rate):.1%}")
```

Read what just happened. The line that matters most is not code at all — it is the comment. *Which statuses count as "bad"?* is a judgment defect. The assistant can list the unique values of `loan_status`; it cannot decide that a "Current" loan should be excluded because its fate is undecided, or that "Late (31-120 days)" is too ambiguous to label. You decided that. You should be able to defend it.

The output will tell you, in plain numbers, how high the bar already is:

```
Charged-off rate among resolved loans: 13.2%   [verify against the actual LendingClub file]
Majority-class baseline accuracy:      86.8%   [verify against the actual LendingClub file]
```

**Before/after, in one sense:** *before* this five-minute profile, "89% accuracy" sounded like success. *After* it, you know 89% is two points above doing nothing, and you know to measure your model on the minority class instead. You have not cleaned a single value yet. You have only looked — and looking changed what every downstream number means. That is the entire argument of the book in miniature.

## Exercises

**1. Find the baseline.** Load any binary-target dataset you have access to (or the LendingClub data). Without building a model, compute the majority-class baseline accuracy. Write one sentence: "A model is only worth deploying if it beats ____% by a margin that justifies its cost." Fill in the blank with a real number.

**2. Classify the defects.** Take five columns from the LendingClub data — say `int_rate`, `annual_inc`, `mths_since_last_delinq`, `emp_title`, and `loan_status`. For each, label its primary defect as *mechanical*, *analytical*, or *judgment*. For the judgment ones, write the question-about-the-world that you would have to answer to clean them.

**3. Catch the cascade.** Describe, in a short paragraph, a plausible data cascade for LendingClub: an upstream defect that is cheap to fix now but, if ignored, compounds into an expensive downstream failure. Name the defect, the amplification, and the eventual symptom.

**4. Audit the assistant.** Prompt an AI assistant to "clean the `annual_inc` column." Do not run its code. Instead, list every claim-about-the-world its suggested code would silently assert. How many of those claims did it ask you to confirm?

## The AI Wayback Machine: W. Edwards Deming

> Long before "data science" was a job title, **W. Edwards Deming** (1900–1993) was telling manufacturers a version of the GIGO principle that they did not want to hear. Deming, an American statistician and management theorist, argued that quality could not be inspected *into* a product at the end of the line — it had to be built into the process that produced it, and that process had to be understood statistically. His work helped rebuild post-war Japanese manufacturing and gave us the durable insight that **most defects come from the system, not from the individual operator.**
>
> Translate that into your file. The income units error, the imbalanced target, the missing-value convention — these are not the fault of any single borrower or clerk. They are properties of the *system* that collected and stored the data. Deming would tell you that chasing individual bad rows while ignoring the process that generated them is a losing game. He would tell you to profile the process — to understand *why* the data looks the way it does — before you start fixing values. That is exactly the move from "fix the syntax" to "ask the question about the world." Deming spent a career insisting that you cannot manage what you do not measure, and you cannot measure what you have not first understood. The GIGO problem is Deming's lesson, ported from the factory floor to the CSV.

## Bridge to Chapter 2

You now have the thesis and the discipline: model quality is bounded by data quality, defects come in three kinds, and the judgment layer is yours alone. But discipline needs a target. Before you can clean a dataset, you have to *choose* one and *understand* it — to ask whether it is even fit for the job you have been asked to do. In the next chapter we put the LendingClub data on the bench and score it, column by column, against a strict thirteen-property scorecard. We find out exactly which defects it contains, where they live, and whether this dataset can carry the weight of every lesson still to come.

## Sources

- Deming, W. E. (1986). *Out of the Crisis*. MIT Press. (For the systems-quality argument summarized here.)
- McKinney, W. (2010). Data Structures for Statistical Computing in Python. *Proceedings of the 9th Python in Science Conference (SciPy)*, 56–61.
- Pedregosa, F., et al. (2011). Scikit-learn: Machine Learning in Python. *Journal of Machine Learning Research*, 12, 2825–2830.
- Sambasivan, N., Kapania, S., Highfill, H., Akrong, D., Paritosh, P., & Aroyo, L. M. (2021). "Everyone wants to do the model work, not the data work": Data Cascades in High-Stakes AI. *Proceedings of the 2021 CHI Conference on Human Factors in Computing Systems (CHI '21)*.
- Wickham, H. (2014). Tidy Data. *Journal of Statistical Software*, 59(10), 1–23.

## Tags

#gigo #data-quality #data-cascades #class-imbalance #LendingClub #Deming #judgment
