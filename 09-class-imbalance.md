# Class Imbalance

You train your first model on the LendingClub data. It is a logistic regression, the features are clean and scaled from Chapter 8, and the target is `loan_status` — did the loan default or get paid back? You run it. The accuracy comes back at 0.84.

Eighty-four percent. On your first try. You feel the small warm glow of a thing that worked.

Now ask the model one question: *of the loans that actually defaulted, how many did you catch?* You compute the recall on the default class. It is near zero. The model catches almost none of them. It achieved 84% accuracy by doing the laziest thing a classifier can do — predicting "paid back" for every single applicant, including the ones who will not pay you back. It learned that defaults are rare and decided, quite rationally, never to predict one.

The warm glow should turn cold. Because the defaults are the *entire reason the model exists.* Nobody builds a credit-risk model to identify the people who will repay. You build it to find the minority who will not. A model that is 84% accurate and blind to every default is not a good model with a small flaw. It is a useless model wearing a good number as a disguise.

![Confusion matrix for a majority-class classifier: every actual default falls into the predicted-paid cell, leaving a column of zeros under default, beside a callout reading accuracy 0.84 and recall on defaults 0.00.](images/09-class-imbalance-fig-01.png)

*Figure 9.1 — A "predict the majority always" model earns 84% accuracy while catching zero defaults — the metric that matters reads zero, hidden behind the metric that does not.*

This is class imbalance, and it is the most common way a competent-looking data science project quietly fails.

## Feel the Problem Before You Fix It

Start by looking at the target, which we have been ignoring for eight chapters.

```python
import pandas as pd

df = pd.read_csv("lending_club_clean.csv")  # cleaned + scaled from Ch. 8

# Collapse loan_status to a binary default flag.
# [verify against the actual LendingClub file: the exact status strings
#  vary by vintage — e.g. "Fully Paid", "Charged Off", "Default",
#  "Current", "Late (31-120 days)", etc.]
bad = {"Charged Off", "Default", "Late (31-120 days)",
       "Does not meet the credit policy. Status:Charged Off"}
df = df[df["loan_status"].isin(
    bad | {"Fully Paid", "Does not meet the credit policy. Status:Fully Paid"}
)].copy()
df["default"] = df["loan_status"].isin(bad).astype(int)

counts = df["default"].value_counts()
ratio = counts[0] / counts[1]
print(counts)
print(f"imbalance ratio  (paid : default) = {ratio:.1f} : 1")
print(f"minority share = {df['default'].mean():.1%}")
```

In LendingClub data the defaulted/charged-off class is the clear minority. Depending on the vintage and how you define "bad," the share of defaults typically lands somewhere in the mid-teens percent or lower, which puts the imbalance at roughly 5:1 or steeper [verify against the actual LendingClub file]. This imbalance is *real* — it is the actual rate at which loans go bad, not something we injected for a teaching example. That matters: the book's rule is that class imbalance is never artificially created, because the whole skill is reading imbalance that the world handed you. [High — the principle; the specific ratio is dataset-specific, so verify.]

Now reproduce the trap, deliberately, so you feel it.

```python
from sklearn.dummy import DummyClassifier
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score, recall_score, confusion_matrix

X = df.drop(columns=["default", "loan_status"])
y = df["default"]
X_tr, X_te, y_tr, y_te = train_test_split(
    X, y, test_size=0.25, stratify=y, random_state=0
)

dummy = DummyClassifier(strategy="most_frequent").fit(X_tr, y_tr)
pred = dummy.predict(X_te)

print("accuracy:", accuracy_score(y_te, pred).round(3))
print("recall on defaults:", recall_score(y_te, pred).round(3))
print(confusion_matrix(y_te, pred))
```

The `DummyClassifier` predicts the majority class always. Its accuracy will look respectable — roughly equal to the majority share — and its default-recall will be exactly 0.0. The confusion matrix will show a column of zeros: not a single default predicted. Stare at that for a moment. *This is the baseline your real model has to beat,* and accuracy cannot tell you whether it did.

Note `stratify=y` in the split. With a rare class you must stratify, or a random split can hand you a test set with too few defaults to measure anything — or, in a small sample, none at all.

## Stop Measuring the Wrong Thing

The first fix is not to the model. It is to the question you ask of it.

Accuracy is the wrong metric under imbalance because it rewards ignoring the minority class. Replace it with metrics that look at the minority directly:

- **Precision** (of the loans you *flagged* as defaults, how many really defaulted): high precision means few false alarms.
- **Recall** / sensitivity (of the loans that *actually* defaulted, how many you caught): high recall means few misses.
- **F1**: the harmonic mean of the two, when you care about both.
- **PR-AUC** (area under the precision–recall curve): the single most informative summary under strong imbalance. Davis and Goadrich (2006) showed that ROC curves can look reassuringly good on imbalanced data while the precision–recall curve — which a baseline cannot fake — reveals the model is poor. [High — this is the central result of that paper.]

```python
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import classification_report, average_precision_score

clf = LogisticRegression(max_iter=1000).fit(X_tr, y_tr)
proba = clf.predict_proba(X_te)[:, 1]

print(classification_report(y_te, clf.predict(X_te), digits=3))
print("PR-AUC:", average_precision_score(y_te, proba).round(3))
```

Read the `default` row of the report, not the accuracy line. That is where the truth lives.

There is no single "right" metric. Which error matters more — a missed default (you lent money you will not recover) or a false alarm (you declined a borrower who would have repaid) — is a business and ethical judgment, not a statistical one. The field has, if anything, become *more* insistent on this point in recent years as fairness and deployment concerns made the cost of false negatives and false positives explicitly domain-dependent. The metric is a place where the irreducibly human layer of this book shows itself: a tool can compute any of these numbers, but only a person can decide which one the model will be held to.

It helps to make the costs literal. A missed default is not "one error" — it is a specific dollar amount, the unrecovered principal on that loan, which might be \$15,000. A false alarm is also not "one error" — it is the foregone interest margin on a loan you declined, which might be a few hundred dollars. When the two errors cost such different amounts, treating them as equally bad (which is exactly what accuracy and even F1 implicitly do) is itself a modeling error. The honest version of this chapter ends not at a metric but at an *expected-cost* calculation: for each candidate threshold, multiply the false negatives by the cost of a missed default and the false positives by the cost of a false alarm, sum them, and pick the threshold that minimizes the total. That number — total expected cost in dollars — is the only metric the business actually cares about, and every statistical metric above is a proxy for it. AutoData can compute the curve for every threshold in one loop; supplying the two cost figures is the part no model can do for you, because they encode the institution's appetite for risk.

One more framing worth knowing, because it changes how you think about the rarest cases. When the minority class is *very* rare — well below the 5:1 here, into the 100:1 range of true fraud — some practitioners stop treating it as classification at all and reframe it as **anomaly detection**: model what "normal" looks like and flag departures from it, rather than trying to learn a tiny positive class directly. That is a different toolbox (isolation forests, one-class methods) and the wrong tool for LendingClub's mid-teens default rate, where you have plenty of minority examples to learn from. But it is worth knowing the boundary exists, because reaching for SMOTE on a 1,000:1 problem is a category error — there is not enough real minority structure to interpolate between, and the synthetic points become pure noise. The research literature treats anomaly framing, resampling, weighting, and threshold tuning as four approaches each with its own failure mode, not a ladder you climb. You choose among them by the shape of the problem.

## Three Ways to Make the Model Care

Once you are measuring the right thing, you can intervene. There are three broad families, and they are not interchangeable.

**Class weights.** The cheapest fix, and often the first one to try. You tell the model that mistakes on the minority class cost more, so it stops ignoring them. In scikit-learn this is one argument.

```python
clf_w = LogisticRegression(max_iter=1000, class_weight="balanced")
clf_w.fit(X_tr, y_tr)
```

`class_weight="balanced"` automatically weights each class inversely to its frequency. No new data is created; the model's objective is simply re-tilted. Recall on defaults usually jumps, precision usually falls — you have told the model to be more willing to cry "default," so it catches more real ones and also more false ones. That trade is the whole game.

**Undersampling and oversampling.** Instead of reweighting, you rebalance the data itself — either by throwing away majority examples (random undersampling, which discards real data) or duplicating minority examples (random oversampling, which can overfit to the copies). The trade between the two is concrete: undersampling is fast and can even help on a large dataset where you have majority examples to spare, but on a small one it amounts to deleting hard-won signal. Oversampling keeps every row but, by stamping out exact duplicates of the minority, tempts the model to memorize a handful of borrowers rather than learn the pattern. Neither is free; both change what the model is trained on.

**SMOTE.** The Synthetic Minority Over-sampling Technique (Chawla et al., 2002) is the famous middle path: instead of duplicating minority rows, it *synthesizes* new ones by interpolating between a minority example and its nearest minority neighbors. The minority class gets bigger without exact copies. The `imbalanced-learn` library implements it.

```python
from imblearn.over_sampling import SMOTE
from imblearn.pipeline import Pipeline as ImbPipeline
from sklearn.linear_model import LogisticRegression

pipe = ImbPipeline(steps=[
    ("smote", SMOTE(random_state=0)),
    ("clf", LogisticRegression(max_iter=1000)),
])
```

[Medium — `imblearn.over_sampling.SMOTE` and `imblearn.pipeline.Pipeline` are current API; verify against your installed `imbalanced-learn` version, as parameter names and defaults shift between releases.]

SMOTE is a tool, not a cure. Chawla and the survey literature (He and Garcia, 2009) are clear that it can manufacture implausible synthetic points — a SMOTE-generated "borrower" interpolated between two real ones may correspond to no real person, and on high-dimensional or categorical-heavy data it can blur class boundaries rather than sharpen them. Each of these methods — resampling, weighting, threshold tuning — has a documented failure mode. None is automatic.

**Threshold tuning.** Often overlooked and frequently the best move: change nothing about training, and instead move the decision threshold. By default a classifier calls "default" when its predicted probability exceeds 0.5. There is nothing sacred about 0.5. If catching defaults matters more than avoiding false alarms, lower the threshold to 0.3 and you catch more of them. You can pick the threshold directly off the precision–recall curve to hit a recall target the business specifies. The quiet appeal of threshold tuning is that it leaves the training data untouched — no synthetic points, no discarded rows, no reweighting — so it introduces no new assumption about what the data *should* look like and nothing to leak across a split. You train once and decide, afterward, how aggressive to be. For that reason it is often worth trying *before* you reach for resampling at all: it may close most of the gap with none of the risk.

```python
from sklearn.metrics import precision_recall_curve
prec, rec, thr = precision_recall_curve(y_te, proba)
# choose the threshold that meets your recall floor, e.g. recall >= 0.70
```

## The Beat That Matters Most: Imbalance Handling Goes Inside the Fold

Here is the mistake that will silently inflate every number you report, and it is worth more than all the technique above.

It is tempting to SMOTE the whole dataset first, then split into train and test. **Do not.** When you oversample before splitting, synthetic minority points generated from a given real point can land in the training set while their "parent" lands in the test set — or near-duplicates straddle the split. The model effectively sees the test data during training. Your cross-validation scores come back gorgeous and your production model fails, because the gorgeous scores were measuring leakage, not skill.

The rule: **resampling is part of the model, so it belongs inside the cross-validation fold, applied to training data only, never before the split.** This is exactly why `imbalanced-learn` provides its own `Pipeline` — wrapping SMOTE inside the pipeline means that when `cross_val_score` carves out a fold, SMOTE runs only on that fold's training portion and the held-out portion stays pristine.

![Two pipeline paths: the wrong path runs SMOTE on the full data before splitting, with synthetic minority points leaking across into the test set; the right path splits first and runs SMOTE only inside each training fold, leaving the test untouched.](images/09-class-imbalance-fig-02.png)

*Figure 9.2 — SMOTE before the split lets synthetic minority points straddle train and test and inflates every score; SMOTE inside the fold keeps the held-out data pristine.*

```python
from sklearn.model_selection import StratifiedKFold, cross_val_score

cv = StratifiedKFold(n_splits=5, shuffle=True, random_state=0)
scores = cross_val_score(pipe, X, y, cv=cv, scoring="average_precision")
print("PR-AUC per fold:", scores.round(3))
print("mean PR-AUC:", scores.mean().round(3))
```

Because `pipe` contains the SMOTE step, the resampling happens *after* each fold is split. This is a preview of Chapter 11, where leakage becomes the whole subject. For now, hold one sentence: **anything that learns from the data — a scaler, an imputer, a resampler — must be fit inside the fold, or it leaks.**

## Before and After

A compact decision memo — the **minority-class evaluation memo** the research notes ask for — makes the whole chapter auditable:

| Pipeline state | Diagnostic | Action | Assumption introduced | Validation check |
|---|---|---|---|---|
| Raw model, accuracy only | 84% accuracy, **0.0 recall on defaults** | switch to PR-AUC + per-class recall | accuracy is misleading here | confusion matrix shows zero defaults caught |
| Imbalance ~5:1+ [verify] | minority = the prediction target | apply class weights / SMOTE | minority errors cost more | recall on defaults rises |
| SMOTE applied | risk of synthetic-point leakage | move SMOTE inside the CV fold | resampling is part of the model | per-fold PR-AUC, not whole-data score |
| Default threshold 0.5 | recall below business floor | tune threshold off PR curve | 0.5 is arbitrary | recall meets the stated target |

The point is not that any one row is the right answer. The point is that each row names the *assumption* — and assumptions are the thing a human owns and an automated tool cannot.

## Exercises: Make the Imbalance Real

1. **Earn the cold feeling.** Train the majority-class `DummyClassifier` on `loan_status`. Report its accuracy and its recall on defaults. Write the one sentence you would say to a manager who is excited about the accuracy number.

2. **Three interventions, one table.** Train logistic regression four ways — plain, with `class_weight="balanced"`, with SMOTE, and plain-but-with-a-tuned-threshold. Report precision, recall, F1, and PR-AUC for the default class for each. Which would you ship, and what business question did you have to answer to decide?

3. **Leak it, then fix it.** Apply SMOTE to the full dataset, *then* split and evaluate. Record the PR-AUC. Now do it correctly with SMOTE inside the CV fold. Record that PR-AUC. Explain the gap.

4. **Pick the metric, defend it.** For a credit-risk model, argue in a short paragraph whether a missed default or a false alarm is the costlier error, and translate that argument into a specific metric and threshold target. There is no universally correct answer — that is the exercise.

## Bridge

We have been treating the features as a tidy block of numbers. But buried in the LendingClub file is a column we have not touched: the free-text fields where borrowers described, in their own words, why they wanted the loan. Those words are messy — inconsistent punctuation, all caps, one-word entries beside paragraph-long pleas. And they carry signal about who repays. Dropping them is easy and lossy. Next chapter, we make text into features.

##  AI Wayback Machine

**Nitesh Chawla** is a computer scientist whose 2002 paper introduced SMOTE — the synthetic over-sampling technique that became the default reflex for imbalanced classification, and which this chapter treats as one tool among several rather than a cure.

**Run this:**

```
Who is Nitesh Chawla, and how does their work connect to the class-imbalance problem we covered in this chapter? Keep it to three paragraphs. End with the single most surprising thing about their career or ideas.
```

→ Search **"Nitesh Chawla"** on Wikipedia.

**Now make the prompt better.** Try one of these:

- Ask it to walk through how the original SMOTE algorithm generates a synthetic example, step by step.
- Add a constraint: "Answer including documented failure modes and criticisms of SMOTE."

What changes? What gets better? What gets worse?

## Sources

- Chawla, N. V., Bowyer, K. W., Hall, L. O., and Kegelmeyer, W. P. "SMOTE: Synthetic Minority Over-sampling Technique." *Journal of Artificial Intelligence Research*, 2002. DOI 10.1613/jair.953. — Foundational over-sampling paper; lets the chapter teach SMOTE as one tool, not magic.
- He, H., and Garcia, E. A. "Learning from Imbalanced Data." *IEEE Transactions on Knowledge and Data Engineering*, 2009. — Broad survey grounding the settled/disputed claims on metrics, resampling, and algorithmic approaches.
- Davis, J., and Goadrich, M. "The Relationship Between Precision-Recall and ROC Curves." *ICML*, 2006. — Primary source for preferring PR curves over ROC under strong imbalance.
- Pedregosa et al. "Scikit-learn." *JMLR*, 2011; the `imbalanced-learn` documentation and the scikit-learn `Pipeline`/metrics docs (verify against installed versions). — Implementation references for resampling inside the fold and minority-class metrics.
