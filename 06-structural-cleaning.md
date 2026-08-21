# Structural Cleaning: Making the Schema Tell the Truth

You try to take the mean of the interest-rate column and pandas refuses:

```python
>>> df["int_rate"].mean()
TypeError: can only concatenate str (not "int") to str
```

The error is not a bug. It is the file telling you what it actually is. `int_rate` looks like a number when you scroll through it — `13.49`, `7.62`, `18.25` — but every value is the string `"13.49%"`, percent sign and all. pandas read the column as `object` dtype, which is to say: text. And text does not have a mean.

This is the most common defect in real-world data and the most quietly destructive, because it does not announce itself. The column *looks* numeric. The summary statistics are simply absent or wrong, and a downstream model either crashes or — worse — silently treats `"13.49%"` as a categorical token, learning a separate dummy variable for every distinct rate string. Structural defects do not corrupt your answer loudly. They corrupt it while everything appears to run.

![Four raw string cells — "13.49%", " 36 months", "$45,000", "10+ years" — mapping across arrows to clean typed numeric values, with the "10+ years" to 10 row flagged to show the censoring it silently discards.](images/06-structural-cleaning-fig-01.png)

*Figure 6.1 — Repairing numbers-stored-as-strings into tidy numeric cells is mostly mechanical, but each transform hides a judgment — and turning "10+ years" into 10 throws away the censored tail.*

This chapter is about repairing the *shape* of the data so that every column is the type it claims to be, every category is spelled one way, and the table matches the structure that every statistical tool silently assumes.

## The Target: Wickham's Tidy Data

Before fixing anything, name the goal. Hadley Wickham's *Tidy Data* (2014) gives the cleanest definition of the shape you are cleaning *toward*: each variable is a column, each observation is a row, each value is a cell. [High] It sounds obvious. It is not, because real files violate it constantly — and the violations in the LendingClub file are precisely the ones Wickham catalogued: values that encode units (`"36 months"`), columns that mix a measurement with its formatting (`"13.49%"`), and categories that should be one value but appear as several (`"Teacher"`, `"teacher"`, `"TEACHER"`).

Tidy data is not a stylistic preference. It is the contract every downstream step depends on. `IterativeImputer` from the last chapter, the encoders of the next, every scikit-learn estimator — all assume the table is already tidy. Structural cleaning is the work of honoring that contract.

## Defect One: Numbers Stored as Strings

The LendingClub file hides numbers inside text in at least four columns [verify against the actual LendingClub file]:

- `int_rate` — `"13.49%"` (trailing percent)
- `revol_util` — `"45.3%"` (trailing percent)
- `term` — `" 36 months"` (leading space, trailing unit)
- `emp_length` — `"10+ years"`, `"< 1 year"`, `"3 years"` (unit, and special tokens)

Each needs a different repair, and each repair encodes a small judgment.

```python
import pandas as pd
import numpy as np

# int_rate / revol_util: strip the percent sign, cast to float
for col in ["int_rate", "revol_util"]:
    df[col] = (df[col].astype(str)
                       .str.rstrip("%")
                       .str.strip()
                       .replace("nan", np.nan)
                       .astype(float))
```

A decision is buried in that one block: do you store `13.49%` as `13.49` or as `0.1349`? Both are defensible; what is *not* defensible is mixing them, or repairing `int_rate` to a percentage and `revol_util` to a proportion. Consistency is the rule, and it is a human's call, not the code's. Document which convention you chose, because the model coefficients will only be interpretable if you remember it.

```python
# term: " 36 months" -> 36 (an integer count of months)
df["term"] = (df["term"].astype(str)
                         .str.extract(r"(\d+)")[0]
                         .astype("Int64"))
```

`emp_length` is the genuinely interesting one, because `"< 1 year"` and `"10+ years"` are not clean numbers — they are *censored* values. Turning `"10+ years"` into `10` quietly throws away the information that the true value could be 10, 15, or 30. Turning `"< 1 year"` into `0` does the same at the bottom.

```python
def parse_emp_length(x):
    if pd.isna(x):
        return np.nan
    x = str(x)
    if "<" in x:
        return 0          # "< 1 year" -> 0; a modeling choice, not a fact
    if "10+" in x:
        return 10         # "10+ years" -> 10; censors everything above
    m = pd.Series(x).str.extract(r"(\d+)")[0].iloc[0]
    return float(m) if pd.notna(m) else np.nan

df["emp_length_num"] = df["emp_length"].apply(parse_emp_length)
```

The comments are not decoration; they are the audit trail. Mapping `"10+ years"` to `10` is a *decision to treat a censored category as its lower bound.* For most models that is fine. For a model where long tenure is the whole point, you might keep `emp_length` as an ordinal category instead and let Chapter 7 encode it. The AI can write either version in seconds. Which one is right depends on what you are modeling — and that is the part that does not delegate.

## Defect Two: Capitalization and Whitespace in Categories

`emp_title` is a free-form text field a borrower typed, and humans are inconsistent. The same job appears as `"Teacher"`, `"teacher"`, `"TEACHER"`, `" Teacher "`, and `"Teacher  "`. To a computer these are five different categories. To a hiring manager they are one. [High] [verify against the actual LendingClub file]

```python
before = df["emp_title"].nunique()

df["emp_title"] = (df["emp_title"].astype(str)
                                   .str.strip()           # kill leading/trailing space
                                   .str.replace(r"\s+", " ", regex=True)  # collapse internal
                                   .str.lower()            # normalize case
                                   .replace("nan", np.nan))

after = df["emp_title"].nunique()
print(f"emp_title distinct values: {before} -> {after}")
```

The collapse is usually dramatic — tens of thousands of "distinct" titles fold into far fewer once case and whitespace stop being treated as meaning. [Medium] [verify against the actual LendingClub file]

But notice the warning the research literature flags: *how much normalization is safe before it erases meaningful variation?* Lowercasing `"Teacher"` and `"teacher"` together is obviously right. But should `"RN"` and `"Registered Nurse"` collapse? `"Sr. Engineer"` and `"Senior Engineer"`? Those require domain knowledge, and aggressive normalization can merge categories that a careful analyst would keep apart. The whitespace-and-case fix is mechanical and safe. The semantic merge is a judgment, and it belongs to you — over-normalizing is its own GIGO failure, erasing signal in the name of tidiness.

Whitespace is worth a separate pass because it hides in columns you would not expect — including the supposedly clean categoricals like `home_ownership` and `purpose`.

```python
obj_cols = df.select_dtypes(include="object").columns
for c in obj_cols:
    df[c] = df[c].str.strip() if df[c].dtype == "object" else df[c]
```

A `" RENT"` with a leading space is a different category from `"RENT"`, and it will produce a phantom dummy variable in Chapter 7 that no one notices until the model behaves oddly on new data.

### Silent Coercion Is the Quietest Failure of All

There is a failure mode hiding inside the repairs above that deserves naming, because it produces *no error and no warning* yet corrupts the data. When you call `.astype(float)` on a string column and one value will not parse — a stray `"N/A"`, a `"none"`, a number with a thousands comma like `"1,200"` — the operation can either raise or, with `pd.to_numeric(..., errors="coerce")`, silently turn the unparseable value into `NaN`. Coercion is the right tool, but it must be *audited*, because a column that quietly gained two hundred new `NaN`s during type repair has just had two hundred real values deleted under the banner of cleaning.

```python
raw = df["revol_util"].copy()
parsed = pd.to_numeric(raw.astype(str).str.rstrip("%"), errors="coerce")
lost = parsed.isna() & raw.notna()          # was present, became NaN
print(f"{lost.sum()} values failed to parse and became NaN")
print(raw[lost].value_counts().head())       # SEE what they were
```

Always count what coercion destroyed and *look at the values it could not parse.* Sometimes they are genuine junk (`"N/A"`), and conversion to `NaN` is correct — they flow into Chapter 5's imputation. Sometimes they reveal a pattern you did not expect — a different decimal convention, a unit you missed, a whole sub-population entered by a different system. The count is mechanical; deciding whether the lost values were garbage or signal is the judgment, and it is the judgment that separates cleaning from quiet data loss.

### Validate After You Repair

Structural cleaning is reversible only if you check it. After every type repair, assert the column now satisfies the constraint you believe it should. These assertions are cheap, they document your assumptions in executable form, and they fail loudly the day an upstream change breaks them — which is exactly when you want to know.

```python
assert df["int_rate"].between(0, 100).all(), "int_rate out of plausible % range"
assert df["term"].isin([36, 60]).all(), "unexpected loan term"   # LendingClub uses 36/60
assert df["emp_length_num"].between(0, 10).all(skipna=True), "emp_length parse error"
```

The `term` assertion is the instructive one: LendingClub issues 36- and 60-month loans. [verify against the actual LendingClub file] If your parse produced a `48` or a `0`, the assertion catches a regex that matched the wrong digits before that error silently becomes a feature. An assertion is a hypothesis about the data written so the computer can check it — the same discipline as a missing-indicator or an outlier decision log, applied to structure.

## Defect Three: Encoding Corruption (Mojibake)

Free-text fields like `emp_title`, `title`, and `desc` are where character-encoding errors surface. A name typed with an accent — `José`, `Müller` — that was saved as UTF-8 and re-read as Latin-1 turns into mojibake: `JosÃ©`, `MÃ¼ller`. The garbled string is now its own category, and a substring search for `"jose"` will silently miss it. [Medium] [verify against the actual LendingClub file]

The first defense is to read the file with the right encoding in the first place:

```python
df = pd.read_csv("loans.csv", encoding="utf-8", low_memory=False)
# If you see mojibake, the source may be latin-1 / cp1252; try:
# df = pd.read_csv("loans.csv", encoding="latin-1")
```

When corruption is already baked in, a repair library can sometimes reverse it, but verify the result by eye — automated fixers occasionally "correct" text that was never broken. This is a place to be conservative: a wrong fix is harder to detect than no fix. [Medium]

The reason to care, beyond tidiness, is that mojibake fragments a category. A borrower named with an accented character appears under the garbled spelling, which means a group-by, a frequency count, or a join on that field silently splits one real entity into two. The corruption does not announce itself as a data-quality problem; it presents as a slightly noisier distribution, a few extra rare categories, a join that drops a handful of rows. You will not see it unless you look for non-ASCII characters on purpose.

```python
# Surface candidate mojibake: rows with the tell-tale Ã/Â sequences
suspicious = df["emp_title"].astype(str).str.contains(r"[ÃÂ][\x80-\xBF]", na=False)
print(f"{suspicious.sum()} emp_title values look like mojibake")
print(df.loc[suspicious, "emp_title"].head())
```

The decision of whether a flagged string is genuine corruption or a legitimately unusual character is, again, a human's. The scan narrows the field; you confirm.

## Defect Four: Numeric-Looking Categoricals

One quiet trap: a column that *is* numeric in dtype but *categorical* in meaning. A zip-code prefix, an account ID, or a sub-grade encoded as a number should never be summed or averaged. If the LendingClub file carries any such column, casting it to string (or `category`) is the structural fix that prevents a model from learning that "zip 940 is twice zip 470." [Medium] The repair is trivial; recognizing the need for it is the judgment, and it is exactly the kind of thing an automated profiler reports as "numeric" while being substantively wrong.

```python
# A numeric-looking ID is a label, not a quantity:
# df["some_id"] = df["some_id"].astype("string")
```

## The Dirty Schema Repair Log

The artifact this chapter produces is a log that persists across the book: every structural repair, the evidence that motivated it, the action taken, and what remains uncertain. It is what makes the cleaning *reproducible* and *auditable* — a reviewer can see not just what you did but why, and what you deliberately left alone.

| Column | Raw form | Defect | Repair | Judgment / risk |
|---|---|---|---|---|
| `int_rate` | `"13.49%"` | Number as string | strip `%`, → float | Chose percent (13.49) not proportion (0.1349) |
| `revol_util` | `"45.3%"` | Number as string | strip `%`, → float | Same convention as `int_rate` |
| `term` | `" 36 months"` | Number as string + unit + space | extract digits → Int64 | Discards the word "months" (kept in column name) |
| `emp_length` | `"10+ years"` | Censored, unit | parse → numeric (10) | `10+` mapped to lower bound; censoring lost |
| `emp_title` | `"TEACHER"`, `" teacher "` | Case + whitespace | strip, collapse, lower | Did NOT merge synonyms (RN vs Registered Nurse) |
| `home_ownership` | `" RENT"` | Whitespace | strip | Low risk |
| `desc` / `title` | `"JosÃ©"` | Mojibake | re-read encoding / repair | Verified by eye; conservative |

The log's value is the rightmost column. Anyone can strip a percent sign. The discipline is recording the *choice* you made and the information you knowingly let go.

### Before and After

```python
# BEFORE structural cleaning
>>> df.dtypes[["int_rate", "term", "emp_length", "revol_util"]]
int_rate      object
term          object
emp_length    object
revol_util    object

>>> df["int_rate"].mean()
TypeError: can only concatenate str (not "int") to str

# AFTER
>>> df.dtypes[["int_rate", "term", "emp_length_num", "revol_util"]]
int_rate         float64
term               Int64
emp_length_num   float64
revol_util       float64

>>> round(df["int_rate"].mean(), 2)
13.25          # [verify against the actual LendingClub file]
```

The mean now exists. That single fact — that a numeric column can be averaged — is the signal that the schema has started telling the truth.

## Exercises: Repairing the Shape

**1. The phantom categories.** Count distinct values of `emp_title` before and after stripping/lowercasing. Report the reduction. Then find one pair of values that the mechanical fix merged correctly and one pair it would *not* catch (a synonym, an abbreviation). State why the second pair needs a human.

**2. Censoring matters.** Parse `emp_length` two ways: as a number (`"10+ years"` → `10`) and as an ordered category that keeps `"10+"` distinct. Describe a modeling question for which each version is the right choice.

**3. Convention consistency.** Convert `int_rate` to a percentage and `revol_util` to a proportion (0–1) on purpose — the wrong, inconsistent choice. Fit any model that uses both and explain why the coefficients are now uninterpretable even though nothing errored.

**4. Make the AI find the defects.** Hand Claude Code the raw file and ask it to list every column whose dtype does not match its apparent meaning. Check its list against your own. Note any numeric-looking categorical it missed — that is the failure mode of automated profiling, and the reason you read the schema yourself.

## A Bridge to Categorical Encoding

The columns are now honestly typed: numbers are numbers, categories are spelled one way, whitespace is gone. But the categorical columns are still text, and no model accepts text. `home_ownership`, `purpose`, `emp_title`, and `grade` all have to become numbers before they can enter a model — and the next chapter shows that *how* you turn them into numbers is not one decision but three, because these columns are three different *kinds* of categorical. Apply the same encoder to all of them and you will get the wrong answer for at least two. The structural cleaning you just did is what makes that choice visible: now that `grade` is a clean ordinal A–G and `emp_title` is a clean high-cardinality field, their differences are no longer hidden behind dirty strings.

> ### The AI Wayback Machine: Hadley Wickham
>
> Most data scientists have spent more of their lives than they would like reshaping spreadsheets, and **Hadley Wickham** is the person who finally said *why*. His 2014 paper *Tidy Data* named the target: each variable a column, each observation a row, each value a cell. Before tidy data, "clean" was a vibe. After it, "clean" had a definition you could check a file against. [High]
>
> The LendingClub file is a catalogue of tidy-data violations: `"36 months"` smuggles a unit into a value, `"13.49%"` welds a measurement to its formatting, `"TEACHER"` and `"teacher"` split one category into two. Wickham's framework is what lets you see these as the *same kind* of problem — a mismatch between the structure the data has and the structure analysis requires.
>
> A useful prompt for an AI assistant: *"Using Hadley Wickham's tidy-data principles, audit these LendingClub columns and tell me which ones violate 'each value is a single cell of one variable' — and what the tidy version of each column looks like."* The assistant can reshape the columns. Wickham gave you the standard that tells you whether the reshaping is *done* — and the judgment of how far to normalize before you start erasing real variation remains yours. [High]

## Sources

- Wickham, H. (2014). "Tidy Data." *Journal of Statistical Software*, 59(10). — Each variable a column, each observation a row, each value a cell; the target shape of structural cleaning. [High]
- McKinney, W. (2010). "Data Structures for Statistical Computing in Python." *Proceedings of the 9th Python in Science Conference (SciPy).* — pandas dtypes, missing-value representation, text manipulation. [High]
- pandas development team (current). "Working with text data," "Categorical data," "Working with missing data." *pandas documentation.* — `str` methods, `category` dtype, `read_csv` encoding; version-sensitive, verify in your environment. [Medium]
- Sambasivan, N., et al. (2021). "Everyone wants to do the model work, not the data work: Data Cascades in High-Stakes AI." *CHI.* — Under-valued structural data work as a source of downstream failure. [High]
