# Chapter 6 — Research Pass: Pantry Population

*The pantry is not a draft and it is not a citation list. It is the only thing standing between Cowork and an authoritative-sounding lie.*

---

Open `pantry/ch-03-domain-research.md`. The file looks substantial — nine sections, three pages, dozens of bullet points. Here is what four of those sections actually contain.

> **1. Primary Sources.**
> - According to a 2024 article, "AI is transforming graphic design" — most designers will need to adopt new tools or face displacement. *(source: a Medium post by an account with 3 followers; no further citation)*
> - "Studies show 78% of design firms are integrating AI." *(no study named; no year; no methodology)*
> - The McKinsey Global Institute has reported significant productivity gains from generative AI. *(no specific McKinsey report; no page; no figure)*

> **3. Application Domain Examples.**
> - Consider a marketing team using AI to write blog posts.
> - A small business owner could use ChatGPT to design a logo.
> - Educators are exploring how AI changes lesson planning.

> **9. Sourcing Notes.**
> Sources include articles from Forbes, Medium, LinkedIn, and a number of industry blogs. Primary sources were prioritized.

Read Section 9 again. *Primary sources were prioritized.* Section 1 has one primary source — a McKinsey reference too vague to find. The percentage in the second bullet has no study behind it. "Studies show" is not a citation; it is the grammatical form of a citation with the substance removed. Section 3 contains zero graphic designers. Section 9 claims to have prioritized primary sources while citing four aggregators.

This is the pantry file the Chapter Research Gatherer produced for a chapter about AI's impact on graphic design. In two days, Cowork will read this file and draft the chapter. It will produce something authoritative-sounding about AI and graphic design that cites no graphic designers, references a percentage no one can verify, and draws examples from marketing, small business, and education — every domain except the one the book is about.

Now read what the same chapter's pantry looks like after a forty-five-minute evaluation pass.

Section 1 names the Adobe Firefly 3 release notes from March 2024 with version-specific features sourced from Adobe's own release page, a peer-reviewed paper from *Journal of Design Research* on AI-augmented studio workflows, and the AIGA 2024 Design Census with methodology and sample size. Section 3 has five examples: a brand identity system for a regional law firm, an editorial layout for a quarterly magazine, a motion design project, a packaging redesign, a product lockup system — all graphic design, all specific. Section 9 names what was filtered out: Medium trend pieces, LinkedIn posts, listicles. The "Studies show" bullet is gone.

Same chapter. Same TIKTOC.md. Same Gatherer run. The difference is what happened after the script finished.

That difference is what this chapter is about.

---

## What the Gatherer does, and what it cannot do

The Chapter Research Gatherer is a Cowork prompt, not a separate piece of software. You give it the TIKTOC.md and a chapter spec file. For every chapter on the list, it does three things in order: reads the capability statement, learning outcomes, bridge question, and application domain; consults any shared library files in `pantry/` (files named with the `_lib_` prefix, covered below); then runs web research and writes a nine-section notes file. One file per chapter, saved as `pantry/research-ch-XX-<chapter-slug>.md`. Both research prompts — the Gatherer and the deeper Research Pass — are reproduced in Appendix D.

The nine sections are: Primary Sources, State of the Field, Application Domain Examples, Book's Thesis Connection, AI Wayback Machine Candidates, Pedagogical Delivery Research, Representation and Display Research, Open Questions and Research Gaps, Sourcing Notes.

This is a research synthesis task in Harris Cooper's sense. Cooper's 1982 framework for integrative research reviews named five stages: problem formulation, data collection, evaluation, analysis, presentation — and argued that compressing any stage was the move that hid the work.[^cooper] The Gatherer compresses Cooper's first three stages into one prompt. The two it cannot compress are evaluation and analysis. Those are yours. The four-questions pass described below is where Cooper's missing stages get re-added by hand.

[^cooper]: Cooper, Harris M. (1982). "Scientific Guidelines for Conducting Integrative Research Reviews." *Review of Educational Research*, 52(2), 291–302.

![A horizontal six-stage process flow along Cooper's review chain: problem formulation, data collection, and presentation grouped inside a machine band on the left, then a vertical dividing seam marking the machine-to-human hand-off, then evaluation and analysis inside a human band, ending in a draft-ready pantry-file terminal; machine stages tinted one color, human stages another.](../images/06-research-pass-fig-01.png)
*Figure 6.1 — The Gatherer pipeline and where the human re-enters*

The Gatherer runs on a long-context model with retrieval — what has been called a "Deep Research" agent since the generation of tools Anthropic, OpenAI, and Google shipped between 2024 and 2025. Retrieval-augmented generation has moved citation fabrication from roughly half the time toward something lower and harder to measure.[^goddard][^bhattacharyya] The improvement is real. The risk is not gone.

There is a structural reason fabrication persists even with retrieval: language models trained on aggregate text learn the *surface form* of citation — the author-year-title shape — without modeling the act of verifying the source.[^parrots] Citation-shaped text is cheap to generate. Verified citation is not. Someone must do the verification. The pantry evaluation pass is where that someone is you.

[^goddard]: Goddard, Joel et al. (2023). "Hallucination in ChatGPT: A Cross-Disciplinary Investigation of References and Bibliographies." Preprint.
[^bhattacharyya]: Bhattacharyya, Mehul et al. (2023). "High Rates of Fabricated and Inaccurate References in ChatGPT-Generated Medical Content." *Cureus*, 15(5).
[^parrots]: Bender, Emily M. et al. (2021). "On the Dangers of Stochastic Parrots: Can Language Models Be Too Big?" *FAccT '21*.

---

## Four questions before draft-ready

You will read each pantry file once. The goal is not an exhaustive audit — fifteen chapter files in one sitting would make exhaustive impractical. The goal is a sharp triage. Mike Caulfield's SIFT method gave undergraduates four moves: Stop, Investigate the source, Find better coverage, Trace claims.[^sift] The CRAAP test gave five criteria: Currency, Relevance, Authority, Accuracy, Purpose.[^craap] Both are too many to apply habitually across an entire pantry. The four below are adapted from SIFT, sharpened for AI-generated research notes, and designed to fit in five to seven minutes per file.

[^sift]: Caulfield, Mike (2017). *Web Literacy for Student Fact-Checkers*. CC-BY.
[^craap]: Blakeslee, Sarah (2004). CSU Chico Meriam Library. CRAAP Test.

**Question 1 — Is the strongest source primary or secondary?**

Open Section 1. Find the source the Gatherer is leaning on most. Is it a study, a release note, a dataset, a court ruling, an organization's own publication — or is it an article *about* a study, a blog post summarizing a report, a trend piece? If the strongest source in Section 1 is a Medium post or a Forbes article, the chapter is thin even if every other section looks full. A thin Section 1 means Cowork will draft on summaries of summaries. The derivatives compound. The chapter that results sounds authoritative and cites nothing anyone can find.

**Question 2 — Do the domain examples match your reader?**

Open Section 3. Count the examples. Count the ones in your actual domain. If the book is for graphic designers and Section 3 contains marketing, small business, and education examples, the Gatherer found related content but missed the target. This is the most common failure pattern and the easiest to miss, because the examples *sound* relevant — they involve creative work, or visual content, or working with clients. They are not about graphic design. The domain drift operates exactly like the fluency trap: the output has the right shape without the right substance, and the gap only becomes visible when a reader who knows the field opens the page.

**Question 3 — Is anything flagged `[verify]` or `[contested]`?**

Search the file. The Gatherer is instructed to flag any claim it could not source confidently. If the file contains zero flags, that is a yellow flag in itself. Either the chapter covers genuinely well-documented ground or the Gatherer is more confident than the evidence warrants. Sycophancy in long-context models is a measured phenomenon — one of its forms is producing fewer uncertainty markers than the topic deserves.[^sycophancy] A pantry file with no flags is not necessarily a clean pantry file. It may be a pantry file that did not notice what it did not know.

[^sycophancy]: Sharma, Mrinank et al. (2023). "Towards Understanding Sycophancy in Language Models." Anthropic preprint.

**Question 4 — Would a peer in your domain recognize these sources?**

This is the read-aloud test. If you texted Section 1 to your most demanding colleague, would they nod or wince? Practitioners have fast and accurate instincts about what counts as a source in their field. Designers can tell instantly whether a "designer source" was written by a designer. Clinicians can tell instantly whether a "medical source" was written by a clinician. This instinct is the thing the Gatherer does not have. It is the thing you have. Use it.

Four questions. Five to seven minutes per pantry file. Two hours for fifteen chapters, with attention left over.

If all four answers are good: draft-ready. Move on. If any answer fails: thin. The next section gives you the three responses.

<!-- → [TABLE: Four-question evaluation rubric — columns: Question, What to open, Pass condition, Fail signal, Common failure pattern — one row per question] -->

| Question | What to open | Pass condition | Fail signal | Common failure pattern |
|---|---|---|---|---|
| 1 — Is the strongest source primary or secondary? | Section 1, Primary Sources | The leading source is a study, dataset, release note, ruling, or an organization's own publication | The strongest source is a Medium post, Forbes article, or trend piece | Section drafts on summaries of summaries; derivatives compound |
| 2 — Do the domain examples match your reader? | Section 3, Application Domain Examples | Most examples sit squarely in the book's actual domain | Examples come from adjacent fields — marketing, small business, education | Domain drift: right-shaped output, wrong substance, only visible to a peer |
| 3 — Is anything flagged `[verify]` or `[contested]`? | Whole file (search) | Uncertainty is marked where confidence wavered | Zero flags across the file | Sycophantic over-confidence: fewer uncertainty markers than the topic deserves |
| 4 — Would a peer in your domain recognize these sources? | Section 1, read aloud | A demanding colleague would nod | A demanding colleague would wince | Sources sound field-adjacent but were not written by practitioners in the field |

---

## What thin means, and the three responses

Thin pantry has three causes. The cause determines the response, and picking the wrong response wastes either an hour of supplementation work on a problem that required a different fix, or weeks of Cowork drift on a problem that required supplementation.

**Cause A: the research was hard.** The topic is recent, niche, or contested. The Gatherer found two reasonable sources and flagged a third. Section 3 has three good domain examples and two stretches. This is a *supplementable* chapter. Open Google Scholar, your professional association's publications, the trade press in your domain. Forty-five minutes. Add two primary sources to Section 1 by hand. Replace the stretched examples in Section 3 with ones you have lived. The pantry becomes draft-ready before the hour is up.

**Cause B: the field evidence is genuinely thin.** This happens. The Gatherer cannot find what does not yet exist. AI's effect on a specific freelance niche may be reported only in trade newsletters. Case law on a contested claim may be too recent. Qualitative effects that practitioners know from experience may not yet be formalized in anything citable. This is an *accept-with-flag* chapter. Add a banner to the pantry file:

```
[contested — see pantry flag]
Field evidence on this topic is thin. The chapter will rely on
the author's domain experience and will be flagged in risks.md
as a contested claim.
```

Cowork will draft carefully. The author will know to be especially careful in the human rewrite. The chapter ships with eyes open rather than eyes closed.

**Cause C: the TIKTOC.md was vague.** The Gatherer could not fix what the spec did not ask for. Section 1 wanders. Section 3 is generic. Section 8 — Open Questions — is short because the Gatherer did not know what was missing. This is a *return-to-Tic-TOC* chapter. Open `/c1` again. Rewrite the capability statement until it names a specific, demonstrable action. Sharpen the application domain. Then rerun the Gatherer for that chapter alone. A hopeless pantry is a downstream signal of a broken spec. The fix is upstream.

The decision is short enough to memorize:

```
Pantry file thin?
   ├── Topic is hard       → Supplement by hand (45 min)
   ├── Field evidence thin → Accept with flag, mark in risks.md
   └── TIKTOC.md vague     → Return to /c1, sharpen spec, rerun Gatherer
```

![A left-to-right decision tree: one root node "pantry thin?" branching into three cause nodes — topic hard, field evidence thin, TIKTOC.md vague — each routing by a single arrow to one paired response on the right: supplement by hand, accept with flag into risks.md, and return to /c1; the return-to-/c1 response carries an upstream back-loop arc.](../images/06-research-pass-fig-02.png)
*Figure 6.2 — Thin-pantry triage: three causes, three responses*

Write the choice in `risks.md`. Future-you, four chapters deep in the human rewrite, will need to remember which chapters were accepted with flags and why.

---

## The shared markdown library

Some content recurs across chapters: the glossary, the recurring framework definitions, the book's house position on contested claims. Repeating this content in every pantry file wastes space and — worse — lets the content drift. Two chapters citing the same definition with one-word differences confuse the reader in ways that are hard to trace and hard to fix.

The Pragmatic Programmer's DRY principle applies: every piece of knowledge has a single authoritative home.[^pragprog] In the AI+1 scaffold, that home is any file in `pantry/` whose name starts with `_lib_`. The glossary lives in `_lib_glossary.md`. The AI+1 framework definition lives in `_lib_ai-plus-one-frame.md`. The house position on contested claims lives in `_lib_contested-claims.md`.

[^pragprog]: Hunt, Andrew and David Thomas (2019). *The Pragmatic Programmer*, 20th Anniversary Edition. Addison-Wesley.

The Chapter Research Gatherer reads `_lib_` files before generating chapter-specific notes. Anything in `_lib_` is shared context. The Gatherer does not duplicate it into chapter pantry files; it references the definition and moves on. When the Chapter Writer runs in the next chapter, it consults `_lib_` files the same way. When you update a definition once, every subsequent run sees the update.

What belongs in `_lib_`: terms used across more than two chapters, framework definitions, the book's position on contested claims, style notes that apply everywhere, author bio. What does not belong: chapter-specific examples, citations specific to one chapter's topic, per-chapter image briefs. The line is between what is shared and what is particular.

![A radial hub-and-spoke diagram: a central _lib_ hub node with four to five chapter pantry-file nodes arranged around it, each connected by a reference arrow pointing from the hub into the chapter file — the definition flowing outward from a single authoritative source, so one update at the hub propagates along every arrow.](../images/06-research-pass-fig-03.png)
*Figure 6.3 — The `_lib_` shared library: one authoritative home*

<!-- → [TABLE: `_lib_` file taxonomy — columns: File, Contents, When Gatherer reads it, Update trigger — rows for glossary, framework definitions, contested claims, style notes] -->

| File | Contents | When the Gatherer reads it | Update trigger |
|---|---|---|---|
| `_lib_glossary.md` | Terms used across more than two chapters, with one authoritative definition each | Before generating any chapter's notes | A term's meaning changes or a new cross-chapter term appears |
| `_lib_ai-plus-one-frame.md` | The AI+1 framework definition the whole book leans on | Before every chapter run | The framework's articulation is sharpened or revised |
| `_lib_contested-claims.md` | The book's house position on claims that are disputed in the field | Before every chapter run | New evidence shifts the house position on a contested claim |
| `_lib_style.md` | Style notes and author bio that apply everywhere | Before every chapter run | Voice or house-style guidance changes book-wide |

---

## Pantry is not citation

This is the section the chapter most wants to get right, because the distinction it draws is the one that collapses most easily under time pressure.

The pantry is reference, not citation. The distinction is the same one every designer already knows from moodboard practice. A moodboard is what you consult while working — competitive references, texture samples, typographic directions, visual precedents. You may have looked at two hundred references while developing a brand identity. You cite none of them in the deliverable. The references shaped your judgment; the deliverable carries your judgment, not the references.

The pantry plays the same role for chapter drafting. Cowork consults it while drafting. The chapter draft does not cite the pantry. Chapter drafts cite primary sources. If a chapter draft says "according to a 2024 article" without naming the article, that draft is citing the pantry — which means the claim was sourced from the Gatherer's notes rather than traced back to a primary source. The human rewrite must then trace the claim through the pantry to the original source and either cite it properly or remove it. This is the AI-laundered citation pattern. The pantry structure is the defense against it, but only if the defense is maintained in the rewrite.

Sönke Ahrens's *How to Take Smart Notes* describes the same distinction in a different vocabulary.[^ahrens] Niklas Luhmann's Zettelkasten — the 90,000-card archive that produced 70 books and 400 papers — had three layers: fleeting notes taken in the moment, literature notes recording what a source actually said, and permanent notes carrying the writer's own argued claim. Pantry files are Ahrens's literature notes. Chapter drafts are permanent notes. Treating literature notes as if they were already permanent — cutting from the Gatherer's prose into the chapter without tracing back to the primary source — is what produces academic embarrassment in human writers and hallucinated citations in language models. The fix is structural: keep the layers separate.

![A vertical three-tier stack — fleeting notes at the base, literature notes (the pantry) in the middle, permanent notes (the chapter draft) at the top — with a correct-path arrow routing from the literature layer through a primary-source waypoint up to the permanent layer, and a second arrow attempting to skip the waypoint terminated by a blockage glyph marking the forbidden AI-laundered citation shortcut.](../images/06-research-pass-fig-04.png)
*Figure 6.4 — Three note layers: literature notes vs. permanent notes*

Luhmann's system is worth knowing about for a second reason. It was boring. Index cards, a wooden cabinet, a numbering scheme he invented. No magic. The infrastructure was simple and the practice was relentless. The pantry is the same way. The technology is unimpressive. The discipline of evaluating each file before letting Cowork read it is the entire game.

[^ahrens]: Ahrens, Sönke (2017). *How to Take Smart Notes*. North Star Media.

---

## The annotated pantry — Chapter 3 of ai-for-designers

This is the pantry file for Chapter 3 of the running example after the Gatherer ran and after the forty-five-minute supplementation pass. Strong and weak entries are annotated so the evaluation logic is visible in operation.

```
# Research: Chapter 03 — Domain Research
# AI+1: AI Native Personalized Textbooks
Chapter one-line: Students write, run, and synthesize a structured
domain research prompt across three LLMs.
Research date: 2026-05-28

## 1. Primary Sources

[STRONG] Adobe Firefly 3 release notes, March 2024 — Adobe Inc.
Specific features named with version numbers; sourced from Adobe's
own release page. URL preserved.

[STRONG] Hoffmann, M. and Wallace, B. (2023). "Generative AI in
Studio Workflows: An Ethnography of Three Design Practices."
Journal of Design Research, 17(2). Peer-reviewed.

[WEAK — REPLACED] "According to a 2024 trend report, AI adoption
in design is growing." [no source named, percentage unattributed —
removed during supplementation pass]

[STRONG, ADDED MANUALLY] AIGA 2024 Design Census. URL, methodology,
and sample size named. Added by hand after Gatherer missed it.

## 2. State of the Field

[STRONG] What is settled: generative tools are now in every major
design software suite (Adobe, Figma, Canva). What is disputed:
whether AI augments or displaces senior designers. Cite Hoffmann
& Wallace 2023 (augmentation) and Davis 2024 op-ed (displacement).
[verify — Davis op-ed publication venue]

## 3. Application Domain Examples

[STRONG] Five examples, all from graphic design:
(1) Brand identity system for a regional law firm — designer used
Midjourney for moodboarding only, hand-drew the final mark.
(2) Editorial layout for a quarterly magazine — Adobe Firefly used
for stock image generation; layout decisions human.
(3) Motion design for a product launch — AI-assisted storyboarding,
hand-crafted final animation.
(4) Packaging redesign — Figma AI used for variation generation,
typography hand-set.
(5) Product lockup system — generative tools for exploration;
production all manual.

[REMOVED] Marketing teams using AI for blog posts. Small business
owners using ChatGPT for logos. Wrong domain — removed during
evaluation pass.

## 4. Book's Thesis Connection

The fluency trap is most visible in Section 3 examples. AI tools
produce design-shaped output without design judgment. The chapter's
domain research must surface this distinction by example, not claim.

## 5. AI Wayback Machine Candidates

[STRONG] Lead: Paula Scher (1948–). Pentagram partner. Known for
City Opera, MoMA identities. Substantive connection: Scher's career
is the case that design is judgment, not output.

Alternate: Massimo Vignelli (1931–2014). Italian-American designer.
The NYC Subway map. Quote: "If you can design one thing, you can
design everything." Counter-position to AI's generic competence.

## 6. Pedagogical Delivery Research

[STRONG] Three-LLM comparison as cognitive contrasting case
(Schwartz & Bransford 1998). Reading three drafts side by side
makes divergence visible.

## 7. Representation and Display Research

[STRONG] Three-column side-by-side of LLM outputs. Color-coded
agreement/divergence. Designers read color-coded tables natively.

## 8. Open Questions and Research Gaps

- Does Hoffmann & Wallace 2023 have a follow-up study? [verify]
- AIGA 2025 census not yet published; cite 2024 with date stamp.
- Davis op-ed venue uncertain. [verify before draft]

## 9. Sourcing Notes

Primary: Adobe release notes, Hoffmann & Wallace 2023, AIGA 2024.
Avoided: Medium trend pieces, LinkedIn posts, design-tool listicles.
The chapter's source list is the chapter's seriousness.
```

Notice what is missing that the bad version had: unverifiable percentages, the "Studies show" construction, examples from wrong domains. Notice what is present: specific titles, version numbers, peer-reviewed citations, explicit `[verify]` flags where confidence wavered. This is a literature-notes layer in Ahrens's sense. Cowork can draft from this without inventing. That is the only standard the pantry file needs to meet.

<!-- → [IMAGE: Side-by-side spread of the bad pantry Section 1 and the good pantry Section 1 — annotated to show exactly which elements changed and why, with the caption: "Same Gatherer run. Different evaluation pass. The annotation is the chapter's argument made visible."] -->

---

## What the pantry makes possible downstream

A pantry file is not interesting in itself. Its interest is entirely in what happens two chapters later, when Cowork opens it and drafts.

The Cowork output from the bad pantry produces a chapter that uses the "Studies show 78%" figure as if it were settled. It uses the McKinsey reference in a sentence that sounds specific and cites nothing findable. It includes a worked example about a small business owner using ChatGPT to design a logo — which is not the reader, not the domain, not the book's argument. The human rewrite in Chapter 8 must find these problems, trace each claim back through the pantry to its non-existent source, and either find a real source or remove the claim. This is expensive. It is the upstream defect propagating downstream, in the same pattern Curtis, Krasner, and Iscoe described in software projects: requirements defects cost ten to a hundred times more to fix at implementation than at specification.[^curtis]

The Cowork output from the good pantry opens with a specific scene drawn from one of the five domain examples in Section 3. It cites the Hoffmann and Wallace 2023 study when it makes a claim about studio workflows. It flags the contested question — augmentation versus displacement — without resolving it falsely. It puts a `[verify]` marker in the draft where the Davis op-ed venue is uncertain, which the human rewrite can resolve in five minutes. The rewrite is tightening and adding voice, not hunting ghosts.

[^curtis]: Curtis, B., Krasner, H., & Iscoe, N. (1988). "A Field Study of the Software Design Process for Large Systems." *Communications of the ACM*, 31(11), 1268–1287.

The difference is the pantry evaluation pass. Two hours of five-to-seven minutes per file. The cost at specification is a single afternoon. The cost at rewrite, without it, is a week.

Padmakumar and He's 2024 measurement of 10–20% lexical-diversity reduction in LLM-assisted writing is the empirical underpinning of this.[^padmakumar] When a model is given thin research infrastructure and asked to draft authoritatively, it converges on the cheap citation forms that make up most of its training data. A well-constructed pantry file is not a constraint on Cowork's output — it is the input that makes a specific, non-generic output possible. The model will converge on what it is given.

[^padmakumar]: Padmakumar, Vishakh and He He (2024). "Does Writing with Language Models Reduce Content Diversity?" *ICLR 2024*.

---

## AI Wayback Machine — Niklas Luhmann

> **Prompt to run in Claude or ChatGPT:**
>
> "Read the Wikipedia article on Niklas Luhmann and his Zettelkasten. Then argue whether the AI+1 pantry system is a Zettelkasten or only resembles one. Identify the strongest disanalogy between the two systems — the place where the analogy breaks down most seriously."

Luhmann (1927–1998) was a German sociologist who built, over thirty years, a personal note-taking system of roughly 90,000 paper slips, indexed by a numeric code he invented and cross-referenced by hand. From it he produced 70 books and 400 papers — an output that has never been credibly explained by anything other than the system itself.

His claim was that thinking happens in the notes, not in the head and not in the draft. The finished books are downstream of the Zettelkasten in the same way that chapter drafts are downstream of the pantry. A thin Zettelkasten produces thin books. A thin pantry produces thin chapters, no matter how hard the human rewrites later.

The Wikipedia article is substantive. The prompt asks you to read it once and find the strongest disanalogy — the place where the pantry is *not* a Zettelkasten. The disanalogy is the most informative result.

---

## LLM Exercises

**Exercise 1 — Evaluate two pantry files against the four questions**

Pick any two pantry files the Gatherer produced for your book. For each file, answer the four questions in writing:

1. What is the strongest primary source? Name it by title and explain why it is primary rather than secondary.
2. What is one claim that needs verification? Quote the claim. Name what evidence would settle it.
3. Do the Section 3 examples match your reader's domain? Count: how many of N examples are in your actual domain?
4. Would a respected peer in your field recognize the sources in Section 1? State yes or no, with one sentence of reason.

Then run the following prompt on one of the files:

> "Here is a pantry notes file from an AI-generated research pass. Apply the SIFT method (Stop, Investigate the source, Find better coverage, Trace claims) to Section 1 specifically. Identify the single weakest citation and describe what a stronger replacement would look like."

Compare the model's SIFT analysis to your own Question 1 evaluation. Where do they agree? Where does the model catch something you missed, or vice versa?

**Exercise 2 — Triage and produce the risks.md entry**

Read every pantry file in your `pantry/` directory. For each chapter, write one line in `risks.md` using this format:

```
ch-XX: DRAFT-READY
ch-XX: THIN — supplement (reason; what to add)
ch-XX: THIN — accept-with-flag (reason; what the flag is)
ch-XX: THIN — return-to-Tic-TOC (reason; which part of the spec is broken)
```

When you have all entries, run this prompt on the completed `risks.md`:

> "Here is a triage log for a set of chapter pantry files. Analyze the distribution of DRAFT-READY versus THIN entries. What does the distribution suggest about the quality of the TIKTOC.md specification — specifically, is the thinness concentrated in a particular phase (early chapters, late chapters, chapters with contested topics) or is it distributed? What does the pattern predict about the Cowork draft quality across the book?"

Read the model's analysis. Is the pattern it identifies the one you would have predicted?

**Exercise 3 — Stress-test the shared library**

Examine your `_lib_` files. Identify one term or framework definition that appears in more than two chapter pantry files. Run the following:

> "Here are three pantry file excerpts, each defining the same term: [paste the three excerpts]. Identify: (1) whether the definitions are consistent with each other, (2) what the strongest version would be, and (3) what downstream confusion a reader would experience if all three versions appeared in the final book."

Use the model's response to decide whether the term belongs in `_lib_` and, if so, what the canonical definition should be.

**Exercise 4 — Build a pantry file for a thin chapter**

Take the chapter you triaged as *return-to-Tic-TOC* (or, if none, the thinnest chapter in the set). Rewrite the capability statement in `/c1` until it names a specific, demonstrable action at Apply level or above. Then run the Gatherer again for that chapter alone.

Apply the four questions to the new pantry file. If the file is now draft-ready, document what changed in the capability statement that produced the better research output. If it is still thin, apply the correct triage response.

Run this prompt on the before-and-after capability statements:

> "Here are two capability statements for the same chapter — the original vague version and a revised version. Explain how the revision would change what a research assistant would look for when populating a pantry file for this chapter. What specifically would the revised statement cause the researcher to find that the original would cause them to miss?"

---

## Still puzzling

Whether there is a recommended maximum pantry size per chapter is genuinely open. Liu and colleagues' 2024 "Lost in the Middle" finding — that language models systematically under-attend to content in the middle of long contexts — suggests that very long pantry files may produce partially ignored research.[^lost] Empirically, three to five pages per chapter pantry file seems to hit the useful range. Longer files should probably be split into `_lib_` references plus a thinner chapter-specific file, but the exact context-window behavior of the current Chapter Writer prompt needs verification against actual runs [verify — current Chapter Writer context-window behavior].

Whether the Gatherer produces URLs or full bibliographic entries by default is a mix, and which is better depends on the author's publishing destination. Authors publishing to Substack alongside Kindle benefit from URLs; authors planning print citations benefit from full entries. The Gatherer can be instructed to prefer one. The current default is unspecified [verify — current Gatherer prompt default].

Whether the Gatherer infers the reader's domain from the TIKTOC.md or needs it stated explicitly is worth testing for niche subfields. Medical illustration, scientific publishing, and motion design authors sometimes get better Section 3 results by adding an explicit domain hint to the Gatherer prompt. This is a user-discovered workaround, not a documented feature.

[^lost]: Liu, Nelson F. et al. (2024). "Lost in the Middle: How Language Models Use Long Contexts." *Transactions of the Association for Computational Linguistics*.

---

## Prompts

### Figure 6.1 — The Gatherer pipeline and where the human re-enters
Build a horizontal left-to-right process flow of six stages along Cooper's review chain. Group the first three stages — problem formulation, data collection, presentation — inside a machine band tinted one accent. Draw a vertical dividing seam after stage three marking the machine-to-human hand-off. Place the next two stages — evaluation, analysis — inside a human band tinted a second accent. End in a sixth terminal node, draft-ready pantry file, in a third accent. Connect stages with solid arrows. The seam is a heavy vertical rule in ink. Encode machine versus human by band color only. Uniform 1pt strokes, white canvas, no text baked in beyond stage names. Deliverable: a single self-contained HTML file with inline CSS and D3 7.9.0 from the pinned CDN; SVG only; ResizeObserver redraw; tooltips per stage. Structural, not aesthetic.

### Figure 6.2 — Thin-pantry triage: three causes, three responses
Build a left-to-right decision tree with seven nodes: one root decision node on the left, three cause nodes fanning out in parallel, and three paired response nodes on the right. Connect the root to each cause with a branch edge, and each cause to its single response with one arrow. The third response (return to /c1) carries an additional upstream back-loop arc indicating the fix is upstream. Encode the root in ink, the cause nodes in a neutral fill, and the three responses in three distinct accents with the most severe response in the warning accent. Uniform 1pt strokes, white canvas, no cause or response text baked in beyond short labels. Deliverable: single self-contained HTML file, inline CSS, D3 7.9.0 from the pinned CDN, SVG only, ResizeObserver redraw, tooltips per node. Structural, not aesthetic.

### Figure 6.3 — The `_lib_` shared library: one authoritative home
Build a radial hub-and-spoke diagram: one central hub node and five chapter-file nodes arranged evenly around it. Draw an arrow from the hub outward into each chapter node, encoding the read-before-drafting direction so the definition flows from a single source. Encode the hub in one accent and the chapter nodes in a second; arrows in ink. Imply that one update at the hub propagates along all arrows. Uniform 1pt strokes, white canvas, no filenames baked in. Do not draw a competing duplicated-definition-drift diagram. Deliverable: single self-contained HTML file, inline CSS, D3 7.9.0 from the pinned CDN, SVG only, ResizeObserver redraw, hover highlights the hub and one spoke. Structural, not aesthetic.

### Figure 6.4 — Three note layers: literature notes vs. permanent notes
Build a vertical three-tier stack, bottom to top: fleeting notes at the base, literature notes (the pantry) in the middle, permanent notes (the chapter draft) at the top, each a horizontal band. Draw a correct-path arrow routing from the literature band through a small primary-source waypoint node up to the permanent band. Draw a second arrow attempting to skip the waypoint, terminated with a blockage glyph marking the forbidden direct cut (the AI-laundered citation shortcut). Encode each layer in a distinct accent; the blocked-shortcut arrow in the warning accent ending in a stop glyph. Uniform 1pt strokes, white canvas, no biographical figures baked in. Deliverable: single self-contained HTML file, inline CSS, D3 7.9.0 from the pinned CDN, SVG only, ResizeObserver redraw, tooltips per layer. Structural, not aesthetic.

---

## References

1. Cooper, H. M. (1982). Scientific Guidelines for Conducting Integrative Research Reviews. *Review of Educational Research*, 52(2), 291–302. https://journals.sagepub.com/doi/10.3102/00346543052002291
2. Bhattacharyya, M., et al. (2023). High Rates of Fabricated and Inaccurate References in ChatGPT-Generated Medical Content. *Cureus*, 15(5). https://www.ncbi.nlm.nih.gov/pmc/articles/PMC10277170/
3. Sharma, M., et al. (2023). Towards Understanding Sycophancy in Language Models. arXiv:2310.13548 (Anthropic). https://arxiv.org/abs/2310.13548
4. Liu, N. F., et al. (2024). Lost in the Middle: How Language Models Use Long Contexts. *Transactions of the Association for Computational Linguistics*, 12, 157–173. https://aclanthology.org/2024.tacl-1.9/
5. Padmakumar, V., & He, H. (2024). Does Writing with Language Models Reduce Content Diversity? *ICLR 2024*. arXiv:2309.05196. https://arxiv.org/abs/2309.05196
