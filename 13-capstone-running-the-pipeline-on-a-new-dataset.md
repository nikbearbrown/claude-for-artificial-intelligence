# Chapter 13 — Capstone: Running the Pipeline on a New Dataset

Here is a CSV you have never opened. It is not about loans. Nobody in it is borrowing money or defaulting on anything. It is a telecommunications company's customer file — about seven thousand rows, twenty-one columns — and the column you are asked to predict is called `Churn`: whether each customer cancelled their service. `[verify against the actual file]` You have a phone-service provider's billing extract, and a single afternoon, and the question that decides whether the last twelve chapters were a method or a memory.

Will your pipeline run on it?

This is the test the whole book has been building toward. Everything until now lived on the LendingClub loans — a dataset you came to know so intimately that you could name its skewed columns from memory, recite which fields leaked, recall that defaults ran around 12%. That intimacy was the point of the threading, and it is now exactly the thing that has to be taken away. A cleaning method you can only execute on data you already understand is not a transferable skill. It is recognition. The capstone replaces recognition with transfer: a genuinely unseen dataset, a different domain, defects you have not catalogued, and the discipline to find out how much of your machinery runs unmodified — and, more importantly, to find the few places where it must not.

## Why Transfer Is the Only Real Test

A pipeline, Sculley and colleagues argued in their study of the hidden technical debt in machine-learning systems, is not a finished object the day it first runs clean. [Medium] It is the beginning of a maintenance obligation: every cleaning decision becomes a standing assumption that the next dataset, the next quarter's data, the next deployment will either honor or quietly violate. A pipeline that has only ever seen one dataset has been *tested* against nothing. It has merely been *fit* to a single example, in the same sense an overfit model has been fit to its training set.

So the field's settled position, and this chapter's premise, is plain: a pipeline is not learned until it transfers to a new dataset with new defects. [High] What is *disputed* — and worth stating honestly to a reader about to run a capstone — is whether a single transfer can ever *prove* generalization, or only demonstrate readiness for further review. The honest answer is the second. One successful run on Telco churn does not certify your method for all tabular data everywhere. It demonstrates that the method is portable, that its structure survives a domain change, and that you know where to look when it strains. That is the realistic claim, and overclaiming it would itself be a GIGO failure — confident output from insufficient evidence.

## What Runs Unmodified

Start by reading the new dataset the way Chapter 2 taught you, before touching a single transformer. The Telco churn data has the same structural skeleton as the loan data: a binary target, a mix of numeric and categorical columns, some text-like fields, and some missingness. `[verify against the actual file]` That shared skeleton is exactly why the architecture from Chapter 11 transfers.

The leakage-proof structure carries over with no change to its logic. You still split first, still fit on train only, still route columns by type through a `ColumnTransformer`, still resample inside the fold, still seal the test set. The capstone prompt you give AutoData is essentially the Chapter 11 pipeline with the column names changed:

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

df = pd.read_csv("telco_churn.csv")

# --- column groups for the NEW domain (verify against the file) ---
numeric_features = ["tenure", "MonthlyCharges", "TotalCharges"]                    # [verify against the actual file]
categorical_features = ["gender", "Contract", "InternetService",
                        "PaymentMethod", "PaperlessBilling"]                       # [verify against the actual file]

y = (df["Churn"] == "Yes").astype(int)                                            # [verify against the actual file]
X = df.drop(columns=["Churn", "customerID"])   # drop the identifier, as in Ch.12  # [verify]

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, stratify=y, random_state=42
)

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
full_pipeline = ImbPipeline(steps=[
    ("preprocess", preprocess),
    ("smote", SMOTE(random_state=42)),
    ("model", LogisticRegression(max_iter=1000)),
])

cv = StratifiedKFold(n_splits=5, shuffle=True, random_state=42)
scores = cross_val_score(full_pipeline, X_train, y_train, cv=cv, scoring="roc_auc")
print(f"CV AUC: {scores.mean():.3f} (+/- {scores.std():.3f})")
```

It runs. The `ColumnTransformer` does not care that `tenure` measures months-as-a-customer rather than years-of-employment; it scales it identically. `OneHotEncoder` does not care that `Contract` has the values `"Month-to-month"`, `"One year"`, `"Two year"` instead of LendingClub's `home_ownership` categories; it expands them the same way. SMOTE does not care that the minority class is churners rather than defaulters; it interpolates the same. The split-then-fit discipline is domain-blind by design — that is the entire payoff of having built the structure correctly in Chapter 11. Roughly 80% of the pipeline transfers untouched, because roughly 80% of preprocessing is mechanical once the human decisions are made.

The danger is that this success is seductive. The code runs clean and returns a respectable AUC, and every instinct says *ship it*. But the 20% that did not transfer is where the model's validity actually lives.

![A transfer diagram. A continuous mechanical spine — split, route by type, fit-on-train, resample-in-fold, model — runs unmodified across the new Telco churn domain. Four dashed callouts branch down from it to the places where judgment must re-engage: tenure==0 is not an outlier but the key churn segment, TotalCharges blanks are MNAR and should be filled with 0 not the median, Contract is ordinal not nominal, and the leakage audit must be redone from scratch for this domain's timeline.](images/13-capstone-running-the-pipeline-on-a-new-dataset-fig-01.png)

*Figure 13.1 — The mechanical spine transfers unmodified to the new domain, but the four re-engagement points — where a defect's meaning changed — demand fresh human judgment the running code lets you skip.*

## Where Human Judgment Must Re-engage

A different domain means a different meaning for every defect. The same word — outlier, missing, category — points at a different thing in churn data than it did in loan data, and only a human who has thought about the new domain can do the re-pointing. Walk through the four places the pipeline runs but your judgment must not coast.

**The outlier is a different animal.** On the loan data you reasoned that a very high `annual_inc` might be a real executive, while `annual_inc = 0` was probably a data-entry error. On the Telco data, the numeric columns are `tenure`, `MonthlyCharges`, and `TotalCharges`. `[verify]` A `tenure` of 0 is not an error here — it is a brand-new customer in their first month, which is precisely the most churn-prone segment you have, the opposite of a row to drop. An extreme `MonthlyCharges` is not a typo; it is a customer with every premium add-on. The outlier-handling judgment you made on loans would be actively harmful here. Same code path, opposite domain meaning.

**The missing value tells a different story.** This is the sharpest place the pipeline misleads. The Telco `TotalCharges` column is famous for a specific defect: it is stored as text, and a small number of rows are blank — and those blanks correspond exactly to the brand-new customers whose `tenure` is 0, because a customer who has been billed zero times has no total charges yet. `[verify against the actual file]` Your median imputer will run on it without complaint and fill those blanks with the median total charge of established customers — which is not ignorable missingness at all. It is MNAR: the value is missing *because* of what it represents (no billing has occurred), and the "right" fill is arguably 0, not the median. A human who knows the domain catches this. The imputer does not. Worse, before any of that, `TotalCharges` is a number stored as a string — exactly the Chapter 6 structural defect — so `pd.to_numeric(df["TotalCharges"], errors="coerce")` has to run first, or the column lands in the wrong type group and the median imputer never even sees it. `[verify against the actual file]`

**The category boundary is drawn differently.** On loans, you had to decide whether `grade` was ordinal (it is — A through G is an ordered risk scale) while `home_ownership` was nominal. The Telco data has its own ordinal-versus-nominal calls: `Contract` has a natural order from month-to-month to two-year, and that order carries churn signal, so treating it as unordered one-hot throws information away. `[verify]` There are also columns like `OnlineSecurity` or `TechSupport` whose values include `"No internet service"` — a third category that is not a missing value and not a plain "No," but a structural consequence of the customer having no internet at all. Collapse it into "No" and you have erased a real distinction. The encoder will run either way; only a human reads the category list and asks what each value *means*.

**The target itself must be redefined.** This is the most important re-engagement and the easiest to skip. On loans, the target was `loan_status` mapped so that `"Charged Off"` was the positive class. On churn, it is `Churn == "Yes"`. But the *leakage audit* — the Chapter 11 discipline that quietly justified your whole evaluation — has to be redone from scratch, because leakage is a fact about *this* domain's timeline. Are there columns in the Telco data measured after the churn decision? A field that only exists for retained customers? A flag set by the retention team during a cancellation call? The loan data's leaky columns (`recoveries`, `total_rec_prncp`) tell you *nothing* about which Telco columns leak. You have to walk every column and ask, again, the one question no profiler can answer: *could I have known this at prediction time?* `[verify against the actual file]`

## The New Dataset Challenge, as the Five-Column Artifact

The same decision record from Chapters 11 and 12 carries over — and filling it for the new domain *is* the capstone. Each row forces the re-engagement the running code lets you skip.

| Pipeline state (Telco) | Diagnostic evidence | Action | Assumption introduced | Validation check |
|---|---|---|---|---|
| `TotalCharges` stored as string, ~11 blanks `[verify]` | blanks align with `tenure == 0` | coerce to numeric; impute blanks with 0, not median | "no billing history means zero total charges, not a typical charge" | confirm imputed rows all have `tenure == 0` |
| `tenure == 0` rows | new customers, highest churn risk | keep; do **not** treat as outliers | "a zero here is a real, important state" | churn rate among `tenure==0` is high, as expected |
| `Contract` | three ordered levels | ordinal encode, preserving order | "contract length is an ordered risk scale" | model with ordinal vs. one-hot; compare AUC |
| every column | which are post-churn? | redo leakage audit from scratch | "this domain's timeline differs from loans" | each retained column knowable at prediction time |

## When the Pipeline Strains and What That Teaches

Run it honestly and you will likely find the AUC is *good but not great* — better than guessing, worse than the loan model, and exactly the kind of result that should make you reach for the cleaning report rather than the deploy button. That gap is information. It is the pipeline telling you that the unmodified 80% got you a working model and the un-revisited 20% — the MNAR `TotalCharges`, the ordinal `Contract`, the unrun leakage audit — is leaving signal on the table or letting a quiet leak in.

This is the book's thesis in its final form. The pipeline generalizes; the *judgment* does not. The mechanical structure — split, route, fit-on-train, resample-in-fold, document — is portable across domains and is exactly the part you should automate, hand to AutoData, and trust the object to enforce. The interpretive layer — what an outlier means, whether a blank is ignorable, where this domain's timeline puts the outcome, whether the model is safe to act on — is irreducibly human, has to be re-supplied for every new dataset, and is exactly the part no assistant can do for you, because every one of those calls is a question about the world rather than a question about syntax. Garbage in, garbage out is not finally a statement about data. It is a statement about who is responsible for deciding what counts as garbage — and that responsibility does not transfer with the code.

### Before and After

| | Treating transfer as a rerun | Treating transfer as a test |
|---|---|---|
| `TotalCharges` blanks | median-imputed silently | recognized as MNAR, filled with 0 |
| `tenure == 0` | clipped as an outlier | kept as the key churn segment |
| Leakage audit | reused from the loan data | redone for the churn timeline |
| The good-not-great AUC | shipped | read as a signal to revisit the 20% |
| What you proved | that the code runs | that you can run the code *and judge it* |

## Exercises: The Capstone Run

**1. Run it (Apply).** Point the Chapter 11 pipeline at the Telco churn CSV, changing only column names and the target definition. Report the cross-validated AUC. Note every place the code ran without error but where you suspect a domain-specific judgment was skipped.

**2. The four re-engagements (Analyze).** For each of `TotalCharges`, `tenure`, `Contract`, and the leakage audit, write one sentence stating what the loan-data judgment was and why the churn-data judgment must differ.

**3. Write the new datasheet (Create).** Produce the cleaning report (Chapter 12 template) for the Telco churn dataset, including the AI Use Disclosure for the parts AutoData generated and the parts you decided. The residual-risk section must name at least one churn-specific assumption the loan model never had to make.

**4. The overclaim test (Evaluate).** Your manager says, "The pipeline ran on a totally new dataset, so our method is proven." Write the two-paragraph reply that accepts what the capstone *did* show (portability, readiness for review) and corrects what it did *not* (proof of general validity), citing one concrete judgment that had to be re-made by hand.

## The Book Lands Here

You began with a polished artifact that ran without errors and a quiet question about whether it could be trusted. You end with a method that runs across domains and a sharpened version of the same question — now answerable, because you know exactly which parts of the work the machine can carry and which parts you cannot put down. The pipeline is automatable. The judgment is not. That is not a limitation of today's tools that tomorrow's will erase; it is the structure of the problem. Every cleaning action answers a question about the world, and the world does not come with the answers attached. Someone has to decide. In the AI era, that someone is still, and irreducibly, you.

## AI Wayback Machine: D. Sculley

In 2015, **D. Sculley** and a group of Google colleagues published a paper with a deliberately unglamorous title: *Hidden Technical Debt in Machine Learning Systems.* Its argument was that the running model is the smallest part of a real ML system, and that the largest, least-visible part is the accreted mass of data dependencies, glue code, and preprocessing assumptions — the stuff that does not show up in the accuracy metric and shows up instead, months later, as a system nobody can safely change. [Medium — verify NeurIPS 2015 venue]

The connection to a capstone is exact. The moment your pipeline runs clean on the Telco data is the moment Sculley's warning becomes operative: every assumption you carried over from the loan data is now a hidden dependency on a domain it was never validated against. The unrun leakage audit, the median imputer quietly mishandling MNAR `TotalCharges`, the ordinal column flattened to nominal — these are technical debt being booked in real time, invisible because the code did not complain. Sculley's contribution to a working data scientist is the habit of distrusting the clean run: of treating "it executed" as the start of the inspection, never the end of it. That is the discipline this entire book has tried to install, and it is the right note to end on, because it is the discipline that does not transfer with the code. You have to bring it yourself, every time, to every new dataset.

Ask an AI assistant the Wayback prompt: *"Explain how D. Sculley's work on hidden technical debt helps a modern data scientist avoid a GIGO failure in pipeline transfer and generalization."* Then do the thing the assistant cannot: name the specific hidden dependency in *your* capstone run.

## Sources

- Sculley, D., et al. (2015). *Hidden Technical Debt in Machine Learning Systems.* NeurIPS. [Medium — verify venue]
- Sambasivan, N., et al. (2021). *"Everyone wants to do the model work, not the data work": Data Cascades in High-Stakes AI.* CHI. [Medium]
- Pedregosa, F., et al. (2011). *Scikit-learn: Machine Learning in Python.* Journal of Machine Learning Research, 12, 2825–2830.
- Gebru, T., et al. *Datasheets for Datasets.* Communications of the ACM, 2021 (orig. 2018). [Medium]
- Chawla, N. V., et al. (2002). *SMOTE: Synthetic Minority Over-sampling Technique.* JAIR, 16, 321–357. DOI 10.1613/jair.953.
- IBM Sample Data Sets. *Telco Customer Churn.* (Capstone dataset; verify column names, row count, and the `TotalCharges` blank-rows behavior against the actual file.) `[verify against the actual file]`
- imbalanced-learn and scikit-learn developers. *Pipeline / ColumnTransformer* (current documentation; verify API against the installed version).
