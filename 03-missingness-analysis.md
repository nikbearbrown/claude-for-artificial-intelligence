# Chapter 3 — Missingness Analysis

## A blank that is not empty

Run one line on the LendingClub data and you meet the chapter's central problem head-on:

```python
loans["mths_since_last_delinq"].isna().mean()
```

It returns something like `0.51` — more than half the column is blank. [verify against the actual LendingClub file] A column that is mostly missing looks, at first glance, like a column to delete. Low information, high hassle, gone.

But stop and read the column *name*. `mths_since_last_delinq` — months since the borrower's last delinquency. Now ask the question this book keeps asking: *what does the blank mean in the world?* If a borrower has **never been delinquent**, there is no "last delinquency," and so there is no number of months since one. The field is not empty because data was lost. It is empty because **the event never happened.** [High — this is the documented intent of the field; verify the exact convention against the actual LendingClub file]

That changes everything. The blank is not noise to be filled — it is a *fact*, possibly one of the most predictive facts in the dataset, because borrowers who have never been delinquent are exactly the ones who tend to repay. If you delete the column, you throw away signal. If you fill the blank with the column mean — the reflexive default — you tell your model that a never-delinquent borrower was, on average, delinquent about three years ago. You have manufactured a lie and trained on it.

This is missingness, and it is the most error-prone topic in data cleaning precisely because the errors are silent. A bad imputation does not crash. It produces a clean-looking column and a quietly corrupted model. The discipline of this chapter is to slow down and ask, for every column with blanks, *why is this missing?* — before you decide what, if anything, to do about it.

## Rubin's three mechanisms

In 1976, the statistician Donald Rubin gave the field the vocabulary it still uses to reason about missing data (Rubin, 1976). He distinguished three *mechanisms* — three different reasons a value might be absent — and the distinction matters because each mechanism licenses different handling and threatens different biases. [High]

**MCAR — Missing Completely At Random.** The probability that a value is missing has nothing to do with anything — not with the value itself, not with any other variable. A clerk randomly skipped some entries; a sensor dropped readings at random. MCAR is the friendly case: the rows with missing values are a random sample of all rows, so dropping them loses precision but does not introduce bias. MCAR is also *rare* in real operational data, and assuming it when it is false is a classic GIGO mistake.

**MAR — Missing At Random.** This is the most misunderstood term in statistics, because "at random" is misleading. MAR means the probability of missingness depends on *other observed variables*, but not on the missing value itself once you condition on those variables. Example: `revol_util` (revolving-credit utilization) might be missing more often for borrowers with no revolving accounts — a fact recorded in *other* columns. The missingness is patterned, but the pattern is explainable by data you can see. MAR is the case where principled imputation (Chapter 5) can work, because the observed variables carry the information needed to fill the gap honestly.

**MNAR — Missing Not At Random.** The probability of missingness depends on the missing value itself, even after conditioning on everything observed. A borrower who chose not to report a very low income; a delinquency field blank precisely *because* the borrower's history is clean. MNAR is the dangerous case: the fact of missingness is informative, and no amount of imputation from observed variables can recover the truth, because the truth is *why the value is missing.* The only honest moves are to model the missingness explicitly (a "missing" indicator flag) or to be transparent that your conclusions rest on an untestable assumption.

![Three side-by-side panels of a data column with blanks: MCAR shows blanks scattered randomly, MAR shows blanks clustering against an observed neighbor column, and MNAR in red shows blanks concentrated at one end of the sorted values, where the blank itself means never delinquent.](images/03-missingness-analysis-fig-01.png)

*Figure 3.1 — The same blanks under three mechanisms: scattered (MCAR), explained by an observed neighbor (MAR), or — in red — driven by the missing value itself (MNAR), the informative blank no imputation can recover.*

> **The uncomfortable truth.** You usually **cannot prove the mechanism from the data alone.** [High] MCAR can be partly tested; distinguishing MAR from MNAR generally cannot, because it would require knowing the very values you do not have (Little & Rubin, 2019). Mechanism diagnosis is *underidentified*: the data narrows the possibilities, but the final call rests on reasoning about how the data was generated — which is judgment, not computation. This is the chapter's hardest lesson and its most important one.

## Mapping the missingness

Before reasoning about mechanisms, see the landscape. The AutoData move is to generate a missingness map — and then *you* read it.

```python
import pandas as pd

# Per-column missingness, as a percentage.
miss = (loans.isna().mean() * 100).round(1)
miss = miss[miss > 0].sort_values(ascending=False)
print(miss)
```

You expect a profile roughly like this — verify every number against the real file:

```
mths_since_last_delinq    51.2     [verify]
desc                       86.0     [verify]
emp_title                   6.1     [verify]
emp_length                  5.8     [verify]
revol_util                  0.1     [verify]
```

That already satisfies the book's requirement — at least three columns above 5% missing, with mechanisms that will turn out to differ. But a per-column count hides the question that matters most: *is missingness in one column related to values in another?* That relationship is the empirical fingerprint of MAR.

```python
# Does emp_title missingness relate to employment length?
# (A MAR probe: missingness in one column vs. an observed column.)
loans["emp_title_missing"] = loans["emp_title"].isna()
print(
    loans.groupby("emp_title_missing")["emp_length"]
         .apply(lambda s: s.isna().mean())
)
```

If `emp_title` is missing far more often when `emp_length` is also missing — say, both blank for borrowers who are unemployed or retired — that co-pattern is evidence pointing toward MAR (or MNAR), and *against* MCAR. The test does not prove the mechanism. It rules MCAR less likely and tells you where to point your domain reasoning.

A compact, reusable diagnostic is the correlation of *missingness indicators* across columns:

```python
indicators = loans.isna().astype(int)
# Which columns tend to be missing together?
print(indicators.corr().round(2))
```

Blocks of co-missing columns betray a shared cause — often a whole section of the application that some borrowers skipped, or a data-source merge that left a group of fields null together. Each block is a hypothesis about the world for you to investigate.

### What you can and cannot test

It is worth being precise about how far the data can carry you, because the difference between evidence and assumption is the whole discipline of this chapter.

You *can* gather evidence against MCAR. If missingness in a column is statistically associated with observed values in other columns — as the `groupby` and correlation probes above reveal — then missingness is not completely at random, and MCAR is implausible. Formal versions of this exist (Little's MCAR test is the classic), but you rarely need the formal test; a few well-chosen cross-tabs usually settle whether missingness is patterned. [Medium]

You *cannot*, in general, distinguish MAR from MNAR from the observed data alone. [High] The reason is exact and unavoidable: telling them apart requires knowing whether missingness depends on the *missing values themselves*, and the missing values are, by definition, the thing you do not have. Suppose `emp_title` is blank more often for borrowers who rent. That is consistent with MAR (missingness depends on the observed `home_ownership`) — but it is *equally* consistent with MNAR, where renters with embarrassing or no job titles are the ones who leave it blank, so missingness depends on the unobserved title itself. The same observed pattern fits both stories. No statistic resolves it. Only a claim about borrower behavior does, and that claim is yours to make and to own.

This is why the chapter insists on the worksheet's separation between *evidence* and *likely mechanism*. The evidence column is what the data proved. The mechanism column is what you inferred, and inference here is irreducibly an act of judgment about how the world generated the blanks.

## The mechanism worksheet

Mapping produces evidence; it does not produce decisions. The recurring artifact for this chapter is the **missingness map and mechanism worksheet**, a five-column table you fill in for every column with meaningful missingness. It forces you to separate what the data *shows* from what you *assume*, and to commit to a check.

| Column | Diagnostic evidence | Likely mechanism | Assumption introduced | Validation check |
|---|---|---|---|---|
| `mths_since_last_delinq` | ~51% blank; blank rows have fewer delinquencies in other fields [verify] | MNAR-style: blank ≈ "never delinquent" | Treating blank as an informative category, not a number | Add a `never_delinquent` flag; check it predicts `loan_status` |
| `revol_util` | <1% blank; blanks cluster with zero revolving accounts [verify] | MAR (depends on observed account columns) | Imputable from related credit fields | Compare model with/without imputation on a holdout |
| `emp_title` | ~6% blank; co-missing with `emp_length` [verify] | MAR or MNAR (unemployed/retired self-omit) | Blank may mean "not employed," not "unknown" | Cross-tab blank-rate against `home_ownership`, `purpose` |
| `desc` | ~86% blank; blank dominates newer loans [verify] | Structural/MCAR-by-era (field deprecated) | Blank ≈ "feature not collected for this vintage" | Check blank-rate by `issue_d` year |

Notice what the worksheet does. The "diagnostic evidence" column holds only what the data shows. The "likely mechanism" column holds your *inference* — and it is explicitly *likely*, not proven. The "assumption introduced" column is the GIGO honesty: it names the claim about the world you are about to bet on. The "validation check" column commits you to finding out, downstream, whether the bet paid off. An AI assistant can fill the evidence column from the data. It cannot fill the mechanism, assumption, or — especially — decide whether your assumption is *safe*. Those are yours.

## The cost of getting it wrong

Make the stakes concrete. Suppose you take the reflexive path on `mths_since_last_delinq`: fill the blanks with the column mean and move on. Here is what you have done, in the language of mechanisms.

The blanks are MNAR — they mean "never delinquent." Mean imputation replaces "never delinquent" with "delinquent ~36 months ago." Because never-delinquent borrowers are disproportionately good credit risks, you have just blurred the single sharpest line between repayers and defaulters. Your model's most useful feature has been smeared into mush. The model will still train; its accuracy will look fine; and on the borrowers you most need to classify correctly, it will be worse than it should be. That is a data cascade (Sambasivan et al., 2021) born from one unexamined `fillna`.

![A before-and-after pair of distributions for months-since-last-delinquency: before, a distinct brown spike for the never-delinquent group sits apart from the body of real gap values; after mean imputation, that spike is dragged in red onto the column mean near thirty-six months, erasing the predictive split.](images/03-missingness-analysis-fig-02.png)

*Figure 3.2 — Mean-imputing the MNAR blank relocates the sharp "never delinquent" group onto the column mean (~36 months), smearing the most predictive line between repayers and defaulters.*

Now the right move, which is almost as little code:

```python
# Honor the MNAR reading: missingness is information.
loans["never_delinquent"] = loans["mths_since_last_delinq"].isna().astype(int)

# Fill the numeric column ONLY for those who have a delinquency,
# leaving the flag to carry the "never" meaning. (One option among several;
# the choice is a modeling decision, revisited in Chapter 5.)
median_gap = loans.loc[loans["never_delinquent"] == 0,
                       "mths_since_last_delinq"].median()
loans["mths_since_last_delinq"] = loans["mths_since_last_delinq"].fillna(median_gap)
```

**Before:** one column, 51% blank, about to be lied into uniformity.
**After:** two columns — a clean numeric one *and* a binary flag that preserves the informative fact. You have respected the mechanism. Whether this exact split is optimal is a Chapter 5 question; what matters now is that the decision was *made on purpose*, with the mechanism named and the assumption written down.

> ⚠ **Disclosure.** Every missingness pattern discussed in this chapter is real to the LendingClub data; none was injected. Per the book's policy, core missingness patterns are never artificially manufactured. The exact percentages are flagged for verification against the actual file.

### Seeing the pattern, not just counting it

Numbers in a table are easy to skim past; a picture of where the blanks fall is harder to ignore, and it often surfaces a cause a count cannot. A missingness matrix — rows as observations, columns as fields, a mark wherever a value is absent — turns the abstract "51% missing" into a visible texture. If the blanks in `desc` form a solid block at one end of the file sorted by `issue_d`, you are looking at a field that was switched off on a date, not at random borrower behavior.

```python
import matplotlib.pyplot as plt

# Sort by issue date so any time-based pattern becomes visible.
ordered = loans.sort_values("issue_d")
plt.figure(figsize=(10, 5))
plt.imshow(ordered[["desc", "mths_since_last_delinq", "emp_title",
                    "revol_util"]].isna(),
           aspect="auto", cmap="gray_r", interpolation="nearest")
plt.xticks(range(4), ["desc", "mths_delinq", "emp_title", "revol_util"])
plt.ylabel("loans, ordered by issue date")
plt.title("Missingness matrix (dark = missing)")
plt.tight_layout()
```

Read the image as evidence about process. A clean horizontal split in `desc` — all missing after some row — is the signature of a deprecated field, which points to a structural/MCAR-by-era reading. A salt-and-pepper scatter with no structure is the closest thing to genuine MCAR you will ever see. A column whose blanks line up with another column's blanks is a co-missing block worth a cross-tab. The plot does not decide the mechanism; it tells you which hypothesis to test and which question about the world to ask. As ever, the assistant draws the picture in one call; you read the meaning into it.

## When you genuinely cannot tell

Sometimes the worksheet's "likely mechanism" column will, honestly, read *unknown*. The data is consistent with MAR and with MNAR, and no test settles it. This is not a failure of analysis; it is the normal underidentified state (van Buuren, 2018). The professional response is not to pretend certainty. It is to:

1. **State the assumption explicitly** in the worksheet and the datasheet.
2. **Pick the more conservative handling** — usually a missingness flag, which is robust whether the truth is MAR or MNAR.
3. **Run a sensitivity check**: impute two different ways, train both, and see whether your conclusions change. If they do not, the ambiguity does not matter for your purpose. If they do, you have found a place where the data cannot bear the weight of the decision, and that itself is a finding worth escalating.

This is the human-judgment layer in its purest form. The mechanism is not in the data; it is in your account of how the data came to be. The assistant computes; you adjudicate; and when you cannot adjudicate, you disclose.

## Exercises

**1. Build the worksheet.** For the real LendingClub data, fill in the five-column missingness worksheet for every column above 5% missing. Replace each `[verify]` with a real number, and write your *likely mechanism* as an explicit inference, not a fact.

**2. Probe for MAR.** Choose a column with moderate missingness (e.g., `emp_title`). Cross-tabulate its missingness against two observed columns. Does missingness depend on observed values? Write one sentence stating what your test does and does not prove about the mechanism.

**3. Quantify the cost.** Train two simple models predicting `charged_off`: one that mean-imputes `mths_since_last_delinq` with no flag, and one that uses the `never_delinquent` flag plus a conditional fill. Compare their performance *on the minority class*. Report the difference and explain it in terms of mechanism.

**4. The honest disclosure.** Pick one column where you genuinely cannot distinguish MAR from MNAR. Write the two-sentence disclosure you would put in the dataset's datasheet, stating the assumption your handling rests on and the sensitivity check you ran.

## The AI Wayback Machine: Donald Rubin

> The entire vocabulary of this chapter — MCAR, MAR, MNAR — comes from one paper: **Donald Rubin**'s *Inference and Missing Data*, published in *Biometrika* in 1976 (Rubin, 1976). Before Rubin, missing data was treated as a nuisance to be deleted or filled by whatever was convenient. Rubin's insight was that **the process that causes data to be missing is itself a statistical object you must reason about** — that the *mechanism* of missingness determines whether your analysis is valid, and that ignoring it can silently bias every conclusion you draw. [High]
>
> What makes Rubin's framework so useful to a modern data scientist is exactly what makes this chapter hard: it tells you that the right handling cannot be read off the data alone. The difference between MAR and MNAR lives in *why* a value is absent, and "why" is a claim about the world. Rubin gave the field the discipline of asking that question before reaching for `fillna`. When you look at a blank in `mths_since_last_delinq` and force yourself to ask whether it means "lost" or "never happened," you are doing precisely what Rubin insisted statisticians must do: refusing to treat absence as self-explanatory. Half a century on, the tools have changed beyond recognition and Rubin's question has not aged a day. It is the question that separates an imputation from a fabrication.

## Bridge to Chapter 4

Missingness asks whether a value is *there.* The next question is whether a value, present and plausible-looking, is *real.* In Chapter 4 we turn to the `annual_inc` and `revol_bal` columns and confront their extreme values — the $9.5 million incomes, the enormous balances. Some are genuine high earners; some are data-entry errors; and the data alone will not tell you which is which. As with missingness, the diagnostic is mechanical and the decision is human. We will learn to detect outliers statistically and, more importantly, to decide — with domain judgment — whether an extreme value is an error to remove or a real business event to protect.

## Sources

- Little, R. J. A., & Rubin, D. B. (2019). *Statistical Analysis with Missing Data* (3rd ed.). Wiley.
- Rubin, D. B. (1976). Inference and Missing Data. *Biometrika*, 63(3), 581–592. DOI: 10.1093/biomet/63.3.581
- Sambasivan, N., Kapania, S., Highfill, H., Akrong, D., Paritosh, P., & Aroyo, L. M. (2021). "Everyone wants to do the model work, not the data work": Data Cascades in High-Stakes AI. *Proceedings of the 2021 CHI Conference on Human Factors in Computing Systems (CHI '21)*.
- van Buuren, S. (2018). *Flexible Imputation of Missing Data* (2nd ed.). CRC Press.
- Wickham, H. (2014). Tidy Data. *Journal of Statistical Software*, 59(10), 1–23.

## Tags

#gigo #missing-data #MCAR #MAR #MNAR #imputation #LendingClub #Rubin
