# Chapter 12 — The Cleaning Report: Documenting Data Decisions

Six months from now, someone will ask you a question you cannot answer.

It might be a regulator: *Why does this lending model reject more applicants from one ZIP code than another?* It might be a teammate who inherited your notebook: *Why is `emp_length` median-imputed but `dti` dropped when missing?* It might be a model that has started behaving strangely in production, and the only way to debug it is to reconstruct what the training data looked like — and you cannot, because the cleaning happened across forty cells in a notebook you have since rerun eleven times. Or it might be the worst version: it is you, and the question is *what did I do, and why did I think it was right?* — and you have no record but your own fading memory.

Every cleaning decision you made across the last eleven chapters was a judgment about the world. You decided that a loan with `annual_inc` of zero was an error and not a homemaker, that `recoveries` was leakage and not a feature, that "Full-time" and "full time" were the same category, that a 12% default rate was the real base rate worth resampling around. Each of those decisions could have gone the other way, and a reasonable analyst might have chosen differently. The cleaning report is the document that records which way you went and why — not as bureaucratic overhead, but as the accountability infrastructure that makes your data work auditable, reproducible, and defensible. It is where the irreducibly human layer of this book finally becomes a deliverable you can hand to another person.

## Why Documentation Is Part of the Analysis, Not After It

There is a persistent misconception that cleaning is clerical work — janitorial labor you do before the *real* analysis begins, the way you wash dishes before cooking. The research that grounds this chapter says the opposite, and says it sharply. Sambasivan and colleagues, studying high-stakes AI systems, named the phenomenon of **data cascades**: compounding downstream failures that originate in undervalued, undocumented data work, and that surface only late, in production, where they are most expensive to fix. [Medium] Their finding is blunt — practitioners want to do the model work, not the data work, and the model work cannot rescue weak data practice. This is the book's GIGO thesis stated as an organizational pathology. Garbage in is not only a property of the data; it is a property of the *process*, and an undocumented process is one nobody can inspect for garbage.

What follows is that documentation is not a write-up you produce after the analysis. It *is* part of the analysis, because the decisions it records are analytic decisions. When you chose median imputation for `emp_length`, you made a modeling assumption — that the missingness was ignorable and the median was a reasonable stand-in. That assumption will shape every prediction the model makes. A decision that consequential, left unrecorded, is not "done"; it is merely forgotten.

## What the Cleaning Report Borrows From Datasheets and Model Cards

The professional norm here has a recent and traceable history. In 2018, Gebru and colleagues proposed **Datasheets for Datasets**: the idea, borrowed from the electronics industry where every component ships with a datasheet specifying its operating characteristics, that every dataset should ship with a document answering standard questions. Why was the data collected? By whom? What does each instance represent? What preprocessing was done? What are the known limitations and biases? [Medium — verify Gebru et al. publication venue and year; the CACM version is 2021] The point of a datasheet is not to certify a dataset as clean. It is to make its provenance and its compromises *legible* to anyone deciding whether to use it.

A companion idea, Mitchell and colleagues' **Model Cards**, does the same for the trained model: intended use, evaluation conditions, performance disaggregated across groups, ethical considerations. [Medium] And Bender and Friedman's **Data Statements**, developed for natural-language data, push specifically on documenting the *populations* a dataset represents and the language varieties it covers — directly relevant when your LendingClub data contains a free-text field like a loan `desc` or `title` written by borrowers. [Medium]

The cleaning report sits between the datasheet and the model card. The datasheet describes the data as you received it. The model card describes the model you shipped. The cleaning report documents the transformation that connects them — the sequence of human judgments that turned the raw extract into model-ready features. It is the missing middle of the documentation chain, and for a practitioner it is often the most useful of the three, because it is the one that records what *you* did.

## The End State: Wickham's Tidy Data

A cleaning report needs a description of where the data ended up, and for that the discipline has a crisp standard. Hadley Wickham's **Tidy Data** gives three rules for a well-structured table: each variable is a column, each observation is a row, each value is a cell. [Medium — Wickham 2014, Journal of Statistical Software] "Tidy" is not a synonym for "clean" — a tidy table can still be full of errors — but it is the structural end state your cleaning should reach, and it gives the report a precise way to state the target shape. When your report says "the cleaned dataset is tidy," it is making a checkable claim: one row per loan, one column per attribute, no values smuggled into column headers, no multiple variables crammed into one field like the `"36 months"` string you parsed in Chapter 6.

## The Anatomy of a Cleaning Report

A cleaning report has a stable structure. It does not have to be long — for a small project a single Markdown file is plenty — but it must be complete in a specific sense: every consequential decision must be traceable to the evidence that prompted it and the assumption it introduced.

A working template, which you can carry across projects as a recurring artifact:

```markdown
# Cleaning Report: LendingClub Loan Data
Author: [you] · Date: 2026-05-31 · Source extract: [filename, date, row count]
Target shape (tidy): one row per loan; target = loan_status -> {Charged Off=1, Fully Paid=0}

## 1. Provenance
- Source, license, download date, original row/column counts.
- Known collection biases (e.g., only funded loans appear; rejected
  applications are absent -> survivorship caveat).  [verify against the actual file]

## 2. Columns dropped (and why)
| Column            | Reason dropped                          | World-question answered                  |
|-------------------|------------------------------------------|------------------------------------------|
| recoveries        | measured after default (leakage)         | "Could I know this at application time?" |
| total_rec_prncp   | post-outcome cash flow (leakage)         | same                                     |
| member_id         | identifier, no predictive content        | "Is this a property of the world?"       |

## 3. Decisions per retained column
(One block per nontrivial column. Five fields each — see below.)

## 4. Rows removed
- Count and rule. E.g., dropped 14 rows with annual_inc = 0 as
  data-entry errors, NOT low-income borrowers.  [verify against the actual file]

## 5. Residual risk
- What remains uncertain. Where the model should not be trusted.
- Imputed columns the model leans on; categories seen only at train time.

## 6. AI Use Disclosure
- Which steps used an AI assistant, for what, and how output was verified.
```

The heart of the report is Section 3, and its shape is the five-column decision record you have been building since the early chapters. For each retained column that required a judgment, record: the **raw state**, the **diagnostic evidence**, the **action taken**, the **assumption introduced**, and the **validation check**.

A filled row for the LendingClub data:

| Field | Diagnostic evidence | Action | Assumption introduced | Validation check |
|---|---|---|---|---|
| `emp_length` (e.g. `"10+ years"`, missing ~6%) `[verify]` | missingness shows no strong correlation with `loan_status`; looks MCAR/MAR | map to ordinal integers; impute missing with training median inside the pipeline | "missing employment length is ignorable; a typical tenure is a fair stand-in" | re-run model with missingness indicator added; AUC change negligible |

Read what that single row carries. The action — median imputation — is the syntax. The assumption — "missing employment length is ignorable" — is the world-claim, and it is the part an automated tool cannot supply. A profiler can tell you the column is 6% missing. It cannot tell you whether that 6% is *ignorable*, because ignorability is a fact about why the value is missing, which lives in the data-generating process, not in the data. The validation check is your honesty mechanism: you committed in advance to a test that could have proven the assumption wrong, and you recorded its result. That is the difference between a decision and a guess.

![A decision-record table with rows for emp_length, recoveries, and annual_inc==0, with columns for diagnostic evidence, action, and assumption. A dashed vertical seam divides the table: the diagnostic and action columns are labelled as ones AutoData can draft, while the assumption column — the world-claim — is highlighted and labelled as the column only a human can fill and that no profiler writes.](images/12-the-cleaning-report-documenting-data-decisions-fig-01.png)

*Figure 12.1 — The cleaning report's AI/human seam: AutoData can draft the diagnostic and action columns, but only a human can supply the assumption — the claim about the world that the profiler cannot see.*

## The AI Use Disclosure as a Deliverable

This is where the book's running thread about AI assistance comes to rest. Throughout these chapters you have used Claude Code — AutoData — to profile columns, draft pipeline scaffolding, suggest imputation strategies, and write the very `ColumnTransformer` you assembled in Chapter 11. The AI Use Disclosure is the section of the cleaning report that records that collaboration honestly. It is not a confession and it is not a disclaimer; it is documentation, held to the same standard as everything else in the report.

A disclosure does three things. First, it states **what the assistant did**: "AutoData generated the initial `ColumnTransformer` scaffold and proposed median imputation for skewed numeric columns." Second, it states **what the human decided**: "The author chose which columns to treat as leaky, set the target definition, and rejected the assistant's suggestion to mean-impute `annual_inc` because the column is right-skewed." Third, and most important, it states **how the output was verified**: "Every assistant-generated transformation was checked against the column profile; the leakage audit (Ch. 11) was performed by the author, not the assistant."

The reason the disclosure matters is the reason the whole book matters. An AI assistant can generate code, summarize a column, and propose a strategy. It cannot know whether a missing value is ignorable, whether an extreme income is a real executive or a typo, whether two spellings are the same category, or whether the resulting model is safe to deploy — because every one of those is a question about the world that requires a standard, and the standard is set by a human who can be held responsible for it. The disclosure names where the human stood. A report that hides the AI's contribution is dishonest; a report that hides the *human's* contribution is worse, because it implies a judgment was made when none was.

## A Worked Example: Generating the Report With AutoData, Then Owning It

The mechanical labor of a cleaning report — listing every column, recording every imputation strategy, transcribing every threshold — is exactly the kind of work an AI assistant does well and a human does grudgingly. The trap is to let that fluency stand in for judgment. Watch the seam.

You point AutoData at the cleaned pipeline and ask it to draft the report. It can do an enormous amount correctly. It can read the `ColumnTransformer` and enumerate which columns went to the numeric branch and which to the categorical branch. It can read the `SimpleImputer` and report `strategy="median"`. It can count the rows dropped and the columns removed. It can produce a clean, well-formatted Section 3 with one block per column. Accept all of it. This is execution, and the assistant is good at execution.

Now read what it produced, and notice what it could not have known. For `emp_length`, AutoData will faithfully record *the action*: "imputed with median." It cannot fill the **assumption** column, because "missing employment length is ignorable" is not in the code — it is in your head, the conclusion of a missingness analysis (Chapter 3) about *why* those values are blank. For the rows you dropped where `annual_inc == 0`, the assistant can report that fourteen rows were removed; it cannot certify that those zeros were data-entry errors *rather than* genuinely no-income borrowers, because that distinction is a claim about the world that only a domain-informed human can stand behind. And the assistant will happily transcribe that `recoveries` was dropped, but the *reason* — "measured after the default event, therefore leakage" — is a judgment about the loan timeline that the column profile does not contain.

So the workflow is: let AutoData draft the skeleton and fill the mechanical columns, then go through the report line by line and supply the two columns no profiler can write — the **assumption** and the **world-question it answers**. The before-and-after of that single pass is the whole chapter in miniature:

```text
AutoData draft (action only):
  emp_length | imputed with median | — | —

Human completion (assumption + check supplied):
  emp_length | imputed with median (inside pipeline)
             | "missing tenure is ignorable; median is a fair stand-in"
             | re-ran with a missingness indicator; AUC change negligible
```

The disclosure then writes itself honestly, because the seam is now visible: AutoData drafted the structure and the mechanical fields; the author supplied every assumption and ran every validation check. That sentence is true, and being able to write a true version of it is the entire point of doing the work this way.

### Before and After

| | Undocumented cleaning | The cleaning report |
|---|---|---|
| Six months later | "I think I dropped some columns?" | every dropped column listed with its reason |
| New teammate onboarding | reads 40 notebook cells, guesses intent | reads one report, sees every assumption |
| Regulator asks "why?" | reconstructs from memory, defensively | hands over the decision record |
| AI's role | invisible, unverifiable | disclosed, with verification noted |
| Reproducibility | rerun and hope | every rule and threshold recorded |
| Status of a decision | forgotten, therefore unmade | recorded, therefore accountable |

## Exercises: Writing the Record

**1. Reconstruct a decision (Apply).** Pick any one cleaning action you would take on the LendingClub data and write its full five-column decision record. The assumption column must contain a claim about the world, not a description of the code.

**2. Draft the disclosure (Create).** Write the AI Use Disclosure section for a cleaning workflow in which an assistant proposed the imputation strategy, you overrode one of its choices, and you performed the leakage audit yourself. Three sentences minimum: what it did, what you decided, how you verified.

**3. Audit a phantom report (Evaluate).** You are handed a cleaning report whose Section 3 records, for every column, only the action ("median imputed," "one-hot encoded") and nothing else. Identify what is missing and explain, with one concrete example, what failure this gap would cause six months later.

**4. Tidy or not (Analyze).** Take a column from a raw extract that violates one of Wickham's three tidy rules — for instance, a `term` field storing `"36 months"`, or a single column packing two variables — and write the report entry that documents reshaping it into tidy form, including the world-question the reshape answers.

## Bridge

You now hold two things: a pipeline that is honest (Chapter 11) and a record that makes its honesty inspectable (this chapter). Everything in the book so far has lived on one dataset — the LendingClub loans you have profiled, imputed, encoded, scaled, resampled, and documented until you know its every column. That intimacy is exactly what the final chapter must take away. A method you can only run on data you already know is not a method; it is a memory. Chapter 13 hands you a dataset you have never seen, in a domain you have not worked, and asks the only question that proves you learned anything: does the pipeline transfer? You will find that most of it runs unmodified — and that the few places where it does not are precisely the places where human judgment must re-engage.

## AI Wayback Machine: Timnit Gebru

When **Timnit Gebru** and her co-authors proposed *Datasheets for Datasets*, they were answering a question the machine-learning field had mostly declined to ask: not *how good is this model?* but *what is this data, and what should anyone using it be told?* The proposal drew an explicit analogy to the electronics industry, where no engineer would solder a component into a circuit without consulting its datasheet — its tolerances, its failure modes, the conditions under which its behavior is guaranteed. Gebru's argument was that datasets, which carry far higher social stakes than capacitors, shipped with nothing of the kind. [Medium — verify the analogy and original 2018 arXiv vs. 2021 CACM publication]

The connection to this chapter is direct. The cleaning report is a datasheet for the *transformation* — the same accountability instinct applied to the messy middle where raw data becomes model-ready features. Gebru's deeper contribution, visible across her work on documentation and on the social consequences of undocumented systems, is the insistence that data work is consequential work, that the choices buried in preprocessing shape who a model helps and who it harms, and that those choices must be made *legible* to the people they affect. That is the whole argument for the AI Use Disclosure: a system that cannot say what was done to its data, by whom, and why, is a system no one can be accountable for.

Ask an AI assistant the Wayback prompt: *"Explain how Timnit Gebru's work on Datasheets for Datasets helps a modern data scientist avoid a GIGO failure in data documentation and decision logs."* Then notice what you have to add to its answer — the specific assumptions in *your* report — that the assistant could not have known.

## Sources

- Gebru, T., Morgenstern, J., Vecchione, B., Vaughan, J. W., Wallach, H., Daumé III, H., & Crawford, K. *Datasheets for Datasets.* Communications of the ACM, 2021 (orig. arXiv 2018). [Medium — verify version]
- Mitchell, M., et al. (2019). *Model Cards for Model Reporting.* FAT*/FAccT. [Medium]
- Bender, E. M., & Friedman, B. (2018). *Data Statements for Natural Language Processing.* Transactions of the ACL. [Medium]
- Sambasivan, N., et al. (2021). *"Everyone wants to do the model work, not the data work": Data Cascades in High-Stakes AI.* CHI. [Medium]
- Wickham, H. (2014). *Tidy Data.* Journal of Statistical Software, 59(10). [Medium — verify volume/issue]
