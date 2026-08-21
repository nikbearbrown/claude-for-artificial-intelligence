# Chapter 7 — Chapter Writing: The Cowork Draft Run

*A `log.csv` of fourteen green rows looks like a finished book. The first page of any of those chapters tells the truth.*

---

Saturday afternoon. You ran the Chapter Writer at 11:00 a.m. and went for a walk. It is now 2:00 p.m. The terminal stopped scrolling long ago. You open `log.csv`. Fourteen rows. Every status field reads `OK`. Every chapter has a token count, a runtime, a timestamp. Nothing is `BLOCKED`. Nothing is in red.

```
chapter,status,tokens,runtime_sec,timestamp,verify_count
01-the-fluency-trap,OK,4823,182,2026-05-28T11:03:14,3
02-the-ai-plus-one-designer,OK,5104,201,2026-05-28T11:06:35,2
03-domain-research,OK,4982,194,2026-05-28T11:09:49,4
04-generating-your-tiktoc,OK,5331,221,2026-05-28T11:13:30,5
05-book-scaffold,OK,4567,176,2026-05-28T11:16:26,2
06-research-pass,OK,4891,189,2026-05-28T11:19:35,3
07-chapter-writing,OK,5012,198,2026-05-28T11:22:53,3
08-the-human-rewrite,OK,5247,209,2026-05-28T11:26:22,4
09-finishing-pass,OK,4733,182,2026-05-28T11:29:24,3
10-enrichment,OK,4956,191,2026-05-28T11:32:35,4
11-creating-figures,OK,4488,174,2026-05-28T11:35:09,3
12-final-check,OK,4612,178,2026-05-28T11:38:21,2
00-frontmatter,OK,1842,68,2026-05-28T11:36:41,0
99-back-matter,OK,2105,79,2026-05-28T11:38:00,1
```

A reasonable response to this is mild euphoria. Three hours of computation, two and a half hours of walking, and the book exists. You can almost see it on the Kindle.

You open `chapters/01-the-fluency-trap.md` and read.

The first paragraph is fine — actually quite good. The second contains the phrase "in today's rapidly evolving design landscape." The third cites "studies have shown" without naming the study. The fourth describes a hypothetical scenario involving a "small business owner" instead of a working freelance designer. The middle of the chapter is three pages of competent connective prose that could have been written about any creative profession. The bridge question at the end is *"What does this mean for the future of design?"*

The `log.csv` was honest. The Chapter Writer did exactly what it was asked to do. Every chapter got drafted, every section got filled, the structure was honored. What the log cannot show is what each of those green rows actually contains. This is the moment the book has been preparing you for since Chapter 1. The drafts are real. They are also exactly what the fluency trap looks like when it runs at chapter scale.

---

Before the five failure modes, a brief orientation on what the Chapter Writer actually is, because "Cowork" has been doing more work than it should in these chapters. The Chapter Writer prompt itself is reproduced in Appendix E.

Cowork is, as of 2026, a feature inside Claude's desktop application — launched as a research preview and since made generally available on paid plans, though some sub-features remain in preview.
It is not a separate product you install. It is a runtime that gives Claude access to a project folder on your machine, the ability to read and write files in that folder, and the ability to execute commands in an isolated shell. When the Chapter Writer "runs," Claude is reading your `TIKTOC.md`, `book.md`, `pantry/*.md`, and `chapters-spec.md`, then writing one chapter draft at a time into `chapters/`.

The pipeline this book teaches is built from three layers: Skills (bundled instructions Claude loads when invoked — the Chapter Research Gatherer, the Chapter Writer, the Fact-Checking Assistant); Plugins (configured connectors that extend Cowork — web search, image generation, file presentation); and the project folder `new_book.py` created in Chapter 5. You do not write the skills; you load them once into your Claude environment.

The TIKTOC.md flagged Cowork prompt syntax and tool names as HIGH aging risk. Treat the *architecture* (skills + plugins + project folder) as stable. Treat the exact menu paths and command names as current-state. [verify — confirm current Cowork access path before publication; check against the version of the Claude desktop application your reader will install]

---

The Chapter Writer does five things for every undrafted chapter, in order.

It reads `TIKTOC.md` in full — spec, voice section, chapter list, three-act arc, contested claims. This is the contract. It reads `book.md` for cross-chapter context, so it knows what came before and what is coming next. It audits `chapters/` and leaves any existing chapter alone; the idempotency contract means re-running the Writer does not overwrite finished work. It reads the chapter's pantry file — the nine-section notes populated in Chapter 6. Then it drafts, targeting the house style the TIKTOC.md calls "Attenborough × Feynman."

![A left-to-right flow of five sequential nodes — read TIKTOC.md, read book.md, audit chapters/ and skip existing work, read the pantry file, draft — with a downward branch at the audit step marking the idempotency skip that leaves finished chapters untouched.](../images/07-chapter-writing-fig-02.png)
*Figure 7.2 — The Chapter Writer's five-step read-then-draft sequence*

Long-context models in 2026 (context windows in the 100k–1M token range) make full-chapter generation viable in a way it was not five years ago.[^liu] The constraint is no longer context length. The constraint is what the model attends to *inside* the context — which is the root cause of most of what goes wrong.

[^liu]: Liu, Nelson F., et al. (2024). "Lost in the Middle: How Language Models Use Long Contexts." *Transactions of the Association for Computational Linguistics*, 12, 157–173.

---

The voice the Writer is trying to produce is worth understanding before reading what it produces instead. Four moves define Attenborough × Feynman.

**Scene first.** Open inside a specific moment — a designer at her desk, a terminal after a script finishes, a brief the client rejected. Not "this chapter is about X." Attenborough never opens a *Planet Earth* episode with "this episode is about the ocean." He opens with a single creature doing one specific thing, and the reader is inside the scene before the chapter names what the scene is for.[^attenborough]

**First principles.** Explain the mechanism before naming the term. Why does this happen? What is happening at the layer beneath what you can see? Feynman opens his *Lectures on Physics* by asking what single sentence he would preserve if all scientific knowledge were lost — not the word "atom," but the mechanism the word names.[^feynman]

**Named trade-offs.** Where is the cost? What is the alternative that would also have worked? What does the choice rule out? Pinker's "classic style" — the writer points, the reader looks — only works if the writer is honest about what they are pointing at.[^pinker]

**Scale oscillation.** Move between scales: the individual designer's desk, the studio, the profession, the historical arc. Zoom in to a single moss, zoom out to the continent, return to the moss with the continent visible behind it. This is what makes a chapter feel large without being long.

These four moves are testable. A paragraph either opens in a scene or it doesn't. A mechanism is either explained before its term or after. A trade-off is either named or smoothed over. A scale shift either happens or doesn't. The Chapter Writer is instructed to honor all four. It succeeds roughly 70% of the time and fails in characteristic ways. The five failure modes below are what happens when the voice slips.

[^attenborough]: Attenborough, D. (presenter). *Life on Earth* (1979); *Planet Earth* (2006); *Blue Planet II* (2017). BBC Natural History Unit.
[^feynman]: Feynman, R. P., Leighton, R. B., & Sands, M. (1963–1965). *The Feynman Lectures on Physics*, Vol. I, Ch. 1. Caltech online edition: feynmanlectures.caltech.edu.
[^pinker]: Pinker, S. (2014). *The Sense of Style*. Viking. Chapters 2–3.

---

**Failure mode 1 — Voice drift.**

The chapter opens in scene, hits the first content block in voice, and then somewhere around the middle it flattens. Sentences become smoother. Hedges appear: "it is important to note that," "in today's landscape," "as we have seen." The author's specificity is replaced by generality. By the end the prose reads like a competent magazine article about the topic.

The structural cause is what Bender and colleagues named in the "Stochastic Parrots" paper: models trained on aggregate corpora regress toward corpus-average voice in long generations.[^bender] Lee and colleagues at CHI 2022 measured the same effect in collaborative writing — writers using LLM suggestions converged on shared phrasings over time.[^lee] The middle of a long generation is where drift is strongest, partly because instruction-following weakens with token distance and partly because the surrounding training corpus contains far more competent-magazine-article prose than it contains any specific author's voice.

Voice drift is audible. Read the chapter aloud. The middle does not sound like the opening. The upstream signal is a thin or absent voice section in TIKTOC.md — Cowork has no anchor to return to.

[^bender]: Bender, E. M., Gebru, T., McMillan-Major, A., & Mitchell, M. (2021). "On the Dangers of Stochastic Parrots: Can Language Models Be Too Big?" *FAccT '21*, 610–623.
[^lee]: Lee, M., et al. (2022). "CoAuthor: Designing a Human-AI Collaborative Writing Dataset for Exploring Language Model Capabilities." *CHI 2022*.

**Failure mode 2 — Fabricated specificity.**

"Studies show 78% of design firms..." with no study named. "A 2023 report found..." with no report cited. Numbers appear without provenance. Names of companies appear in contexts that sound plausible but cannot be verified. The citation is present as a surface feature; no retrieval event occurred.

Ji and colleagues' survey of hallucination in natural language generation calls this *extrinsic hallucination* — content that cannot be verified against any source the model had access to.[^ji] TruthfulQA established that the failure is measurable and persistent across model sizes.[^lin] The model generates citation-shaped text because citation-shaped text is high-probability in scholarly contexts.

The diagnostic is a search pass: find every percentage, every "studies show," every "research suggests." For each, can the source be named from the pantry? If no, fabricated specificity. The upstream signal is a thin Section 1 (Primary Sources) in the pantry — Cowork invented because the pantry did not anchor it.

[^ji]: Ji, Z., et al. (2023). "Survey of Hallucination in Natural Language Generation." *ACM Computing Surveys*, 55(12), Article 248.
[^lin]: Lin, S., Hilton, J., & Evans, O. (2022). "TruthfulQA: Measuring How Models Mimic Human Falsehoods." *ACL 2022*.

**Failure mode 3 — Missing domain judgment.**

The chapter is technically correct. It explains the principles, names the frameworks, walks through the structure. What it does not do is reveal that anyone inside the actual domain wrote it. A design critique chapter names hierarchy and contrast without making the specific judgment that a particular brand needed a lowercase wordmark because the founder's accent softens the company name beyond what the spelling suggests. A medical chapter names differential diagnosis without the case-specific judgment a clinician makes at the bedside. The text passes a textbook test and fails a peer test.

The model has not lived the domain. Domain judgment is what Baldwin called the "test-tube" of the artist — the medium in which the self has been formed through specific experience.[^baldwin] It is what cannot be inferred from a TIKTOC.md or a pantry. The model produces what a careful, well-read outsider to the field would produce.

The diagnostic is a single question: would a respected peer in your domain recognize this as coming from inside the profession? If you cannot point to a single sentence that could only have been written by a practitioner, the failure is here. The upstream signal is capability statements in TIKTOC.md that described topics rather than specified outcomes — "students learn about" rather than "students learn to do."

[^baldwin]: Baldwin, J. (1962). "The Creative Process." Reprinted in *The Price of the Ticket: Collected Nonfiction, 1948–1985* (1985). St. Martin's Press.

**Failure mode 4 — Padded middle.**

The chapter opens strongly, hits the first content block well, and then expands. The middle three pages contain transitions, summaries of what was just said, restatements of what is about to be said, and connective tissue without load. The chapter runs 5,000 words. The argument fits in 3,500. The other 1,500 words are middle.

Liu and colleagues' "lost in the middle" finding documents that long-context models attend disproportionately to context beginnings and ends — the middle context is under-attended, and the middle output is under-conditioned.[^liu] Without strong conditioning from context, the model fills with high-probability connective prose. Strunk and White's "omit needless words" is the human-edited cure; Cowork systematically violates it because the model's training data is dominated by writing that did not omit needless words.[^strunk]

The diagnostic is a pencil pass: read pages two through four and cross out any sentence that does not advance a claim, deliver an example, or name a trade-off. If more than 25% of sentences get crossed out, padded middle. The upstream signal is over-broad chapter scope in TIKTOC.md — a 5,000-word target for a 3,500-word argument.

[^strunk]: Strunk, W., & White, E. B. (2000). *The Elements of Style* (4th ed.). Allyn and Bacon.

**Failure mode 5 — Bridge questions that don't bridge.**

The chapter ends with a question that sounds like a bridge but is actually a topic heading. "What does this mean for designers?" "How will AI change creative work?" These are not questions in the sense of having answers the next chapter delivers. They are gestures toward continuation. Zinsser's chapter on transitions names exactly this failure — transitions that pretend to connect but actually wave.[^zinsser]

The cause is structural. A bridge question is a commitment: it claims the next chapter answers it. If the TIKTOC.md did not specify a clear answer in the next chapter's spec, the Writer cannot generate a real bridge. It produces something bridge-shaped. The diagnostic is simple: read the bridge question, then open the next chapter's spec. Does the next chapter answer this question? If no, broken bridge. The upstream signal is inter-chapter logic that was assumed in TIKTOC.md rather than specified.

A sixth failure mode worth naming, though not on the official list: sycophancy. Cowork-drafted chapters tend to agree too easily with the TIKTOC.md's framings and never genuinely push back. The "What would change my mind" sections of this book are partly designed to externalize the disagreement Cowork will not generate on its own.[^sharma]

[^zinsser]: Zinsser, W. (2006). *On Writing Well* (7th ed.). HarperCollins. "Bits and Pieces."
[^sharma]: Sharma, M., et al. (2023). "Towards Understanding Sycophancy in Language Models." Anthropic technical report.

<!-- → [TABLE: five failure modes summary — three columns: mode name, diagnostic test, upstream signal in TIKTOC.md or pantry — one row per failure mode plus the sycophancy note] -->

| Failure mode | Diagnostic test | Upstream signal in TIKTOC.md or pantry |
|---|---|---|
| Voice drift | Read aloud; does the middle sound like the opening? | Thin or absent voice section in TIKTOC.md — no anchor to return to |
| Fabricated specificity | Search every percentage and "studies show"; can the source be named from the pantry? | Thin Section 1 (Primary Sources) in the pantry |
| Missing domain judgment | Would a respected peer recognize a sentence only a practitioner could write? | Capability statements that describe topics ("learn about") rather than specify outcomes ("learn to do") |
| Padded middle | Pencil pass on pages two to four; do more than 25% of sentences fail to advance a claim, example, or trade-off? | Over-broad chapter scope — a 5,000-word target for a 3,500-word argument |
| Bridge questions that don't bridge | Read the closing question, then open the next chapter's spec; does it answer it? | Inter-chapter logic assumed in TIKTOC.md rather than specified |
| Sycophancy (off the official list) | Does the draft ever genuinely push back on a TIKTOC.md framing? | No declared "What would change my mind" position to externalize disagreement |

![A vertical taxonomy of the five Cowork failure modes, each row carrying three cells — mode name, diagnostic test, and upstream signal — with the upstream-signal column tinted to set it apart.](../images/07-chapter-writing-fig-01.png)
*Figure 7.1 — The five Cowork failure modes*

---

The `[verify]` flag is the Chapter Writer's form of intellectual honesty, and it deserves a section of its own because the temptation to treat it as a bug is strong and wrong.

The flag looks like this in a draft:

> ...the average freelance design contract is six months long `[verify — figure not in pantry, model estimate based on industry norms]`...

Bansal and colleagues at CHI 2021 found that uncertainty annotation improves downstream human accuracy — when humans actually engage with the annotations.[^bansal] The flag is the model saying: *I am about to do the thing the chapter warns against — fabricate specificity — and I am marking it so you catch me.* This is intellectual honesty in the strongest form a language model currently produces. Treat it as such.

A draft with zero `[verify]` flags is more suspect than a draft with many. Zero flags either means the topic is extremely well-documented in the pantry, or the model is being more confident than the evidence warrants. Their absence is not reassuring; it is uninformative or worrying.

When you find a `[verify]` flag, you do one of three things: verify and replace (the claim is true; find the source; replace the flag with the citation); verify and remove (the claim is wrong or unfindable; cut the sentence); or leave for later with a note (convert the inline flag to a comment in your tracking file and address it before publication). What you do not do is delete the flag and keep the sentence. That is laundering the model's uncertainty into your authorial voice.

![A branch decision from a single source node — a verify flag found — fanning into three valid output branches (replace with a citation, remove the sentence, convert to a tracked note) and one forbidden branch (delete the flag, keep the sentence) terminated with a blockage glyph.](../images/07-chapter-writing-fig-03.png)
*Figure 7.3 — The three responses to a verify flag*

[^bansal]: Bansal, G., et al. (2021). "Does the Whole Exceed its Parts? The Effect of AI Explanations on Complementary Team Performance." *CHI 2021*.

---

Sometimes a chapter does not draft. The `log.csv` row reads `BLOCKED`. The chapter file contains a stub explaining why.

Three causes are common. The pantry is missing or empty: the Gatherer failed for that chapter, or the file was deleted, or the slug doesn't match. The Writer refuses rather than fabricate a pantry; fix by rerunning the Gatherer for that chapter. The capability statement is uninterpretable: the TIKTOC.md spec is too vague for the Writer to know what success looks like; fix by returning to `/c1` in Tic TOC, sharpening the spec, and rerunning. A contested-claim flag appears in the pantry but `_lib_contested-claims.md` does not declare the book's position; the Writer refuses to take a position the author has not declared; fix by declaring the position and rerunning.

A BLOCKED chapter in Act Two becomes an incomplete chapter in Act Three becomes a hole in the EPUB in Chapter 12. The default is to resolve before continuing. Proceeding manually over a BLOCKED chapter is sometimes the right call; it is never the easy one.

---

The worked example is the opening of `ai-for-designers/chapters/03-domain-research.md` as Cowork drafted it, annotated for all five failure modes.

> # Chapter 3 — Domain Research: The Chapter Before the Chapter
>
> *The structured prompt that turns three LLMs into one usable brief.*
>
> Domain research is one of the most important steps in any textbook
> writing project. Without good research, your book cannot succeed.
> In today's rapidly evolving design landscape, understanding what AI
> is doing to your profession is essential.
>
> Studies have shown that 78% of design firms are integrating AI tools
> into their workflows. This means designers must adapt quickly. Many
> designers are finding that AI can help with brainstorming,
> mood-boarding, and initial concept development.
>
> A small business owner using ChatGPT to create marketing materials
> is a good example of how AI is becoming accessible to non-experts.
> The same principles apply to graphic designers as they explore
> new tools.
>
> In this chapter, we will discuss the three-LLM research prompt and
> how to use it. We will explore how to combine outputs and what makes
> a brief ready for the next step. By the end, you will have a strong
> foundation.
>
> **What does this mean for the future of design?**

Line by line: "Domain research is one of the most important steps" — **voice drift**, opening sentence. Generic textbook prose that could appear in any field. The TIKTOC.md voice section asked for scene-first; this is summary-first. "In today's rapidly evolving design landscape" — **voice drift** compounding; this phrase is a Cowork tell. "Studies have shown that 78% of design firms" — **fabricated specificity**; the number is not in the pantry, no source named. "Many designers are finding that AI can help with brainstorming, mood-boarding" — **missing domain judgment**; technically true and reveals nothing a practitioner would specifically know. "A small business owner using ChatGPT" — **missing domain judgment** of a different kind; the pantry's Section 3 had five graphic design examples; the draft picked a weak entry that should have been pruned in Chapter 6. "In this chapter, we will discuss... By the end, you will have a strong foundation" — **padded middle** previewed; restates the structure before delivering it. "What does this mean for the future of design?" — **bridge question that doesn't bridge**; the next chapter is the Tic TOC walkthrough, which is not about the future of design.

Now the human rewrite of just the opening paragraph:

> Three LLMs answering the same question about your profession give you something no single LLM does: a map of agreement, divergence, and silence. Claude knows the published research. ChatGPT has read the trade press. Gemini has scraped the LinkedIn posts. Run the same prompt across all three on a Tuesday afternoon, and by Wednesday morning you have a domain research brief — the document Tic TOC will demand at `/i1`.

Scene implied (Tuesday afternoon, Wednesday morning). Mechanism (each LLM's training has a different bias; three sources triangulate). Specific (the three named; the timing real). Bridge set (Tic TOC at `/i1` is what the next chapter delivers).

One paragraph. This is what Chapter 8 asks of you for every chapter. The opening paragraph rewrite is the smallest possible demonstration of the work. The full chapter rewrite is harder and takes longer and is the only part of this pipeline no one else can do.

---

## AI Wayback Machine — Joan Didion

> **Prompt to run in Claude or ChatGPT:**
>
> "Read Joan Didion's essay 'Why I Write.' She says 'grammar is a piano I play by ear.' What does that mean about voice in writing — and how would Didion describe what an LLM is doing when it generates prose?"

Didion (1934–2021) is worth reading once before Chapter 8 and once a year after that. Her 1976 *New York Times Book Review* essay is the cleanest statement in English of why voice cannot be specified, only recognized. The five failure modes in this chapter are voice failures the writer can hear but the model cannot. Voice drift is audible. Fabricated specificity has a tinny quality. Padded middle drags. Missing domain judgment sounds like a competent outsider. Bridge questions that don't bridge feel like the music ended on the wrong note.

One thing to carry from Didion into Chapter 8: her argument that voice is recognized but not metricizable is what makes the Combined Test honest about its limits. The test catches the failures it can specify. It cannot guarantee voice. Only the author can do that.

---

## Exercises

**Exercise 7.1 (Apply).** Run the Chapter Writer against your TIKTOC.md, scaffold, and populated pantry. Confirm that `chapters/` contains exactly one `.md` file per chapter on your list. Open `log.csv` and verify that every row has a status, a token count, a runtime, and a `verify_count`. Note any BLOCKED chapters. Do not proceed until BLOCKED chapters are resolved.

**Exercise 7.2 (Analyze).** Pick two chapter drafts. For each, number every paragraph and annotate each occurrence of the five failure modes in the margin: voice drift (VD), fabricated specificity (FS), missing domain judgment (MDJ), padded middle (PM), broken bridge (BB). Count the `[verify]` flags and write the number at the top of the file. Two drafts, twenty minutes each. The exercise trains the eye; by the second chapter you will be reading faster and catching more.

**Exercise 7.3 (Evaluate).** For each chapter in `chapters/`, write one line in `risks.md`:

```
ch-01: SOLID FOUNDATION (3 verify flags, voice consistent, examples right domain)
ch-02: SOLID FOUNDATION (2 verify flags, minor padding in middle)
ch-03: NEEDS PANTRY WORK — Section 1 had no primary sources;
       fabricated specificity throughout. Return to Ch 6 evaluation.
ch-04: SOLID FOUNDATION (5 verify flags, all genuine; opening strong)
```

NEEDS PANTRY WORK is feedback to the pantry, not a verdict on the chapter. The list is what you carry into Chapter 8.

---

## Bridge — Chapter 8

The drafts exist. You have read two of them with a pencil. You have rated all of them in `risks.md`. The pipeline has done what the pipeline does.

Now the pipeline stops.

There is no command to run for Chapter 8. There is no script that turns a Cowork draft into the author's chapter. The seam — the place where the book becomes yours — is the next chapter. It is the only chapter in the book that asks you to spend more time than the rest. It is also the chapter the entire book has been building toward.

---

## Prompts

### Figure 7.1 — The five Cowork failure modes
Build a vertical taxonomy table as a single self-contained HTML file with inline CSS and D3 7.9.0 from the cdnjs CDN. Data shape: six objects, each with three string fields — mode, diagnostic, signal — for voice drift, fabricated specificity, missing domain judgment, padded middle, bridge questions that don't bridge, and a sixth sycophancy row marked off-list. Marks: five (then six) stacked rows of equal height; three text cells per row laid left to right under three column headers (mode / diagnostic test / upstream signal). Channels: position encodes reading order top to bottom; the third column carries a distinct fill tint to set the upstream-signal channel apart from structure. Sort: fixed authored order, sycophancy last. Thin horizontal rules between rows only; no vertical column chrome. Annotation: a one-line header row. No zero baseline (categorical). Deliverable: one HTML file, inline CSS, D3 7.9.0, responsive via ResizeObserver, role="img" with title and desc.

### Figure 7.2 — The Chapter Writer's five-step read-then-draft sequence
Build a horizontal process flowchart as a single self-contained HTML file with inline CSS and D3 7.9.0 from the cdnjs CDN. Data shape: an ordered array of five node objects (label, step index) plus one branch edge off node 3. Marks: five equal rectangular nodes left to right, single arrow links between consecutive nodes, one short downward branch arrow from the audit node representing the idempotency skip that returns out of the main flow. Channels: x-position encodes sequence; the branch arrow is visually differentiated as a secondary path. Sort: fixed step order 1 to 5. Annotation: node labels; a small tag on the branch reading "skip / leave alone." No zero baseline (process diagram). Deliverable: one HTML file, inline CSS, D3 7.9.0, responsive via ResizeObserver, role="img" with title and desc, keyboard-reachable nodes.

### Figure 7.3 — The three responses to a verify flag
Build a branch decision flowchart as a single self-contained HTML file with inline CSS and D3 7.9.0 from the cdnjs CDN. Data shape: one source node ("verify flag found") and four branch objects, three flagged valid (replace with citation, remove sentence, convert to tracked note) and one flagged forbidden (delete flag, keep sentence). Marks: one source node on the left; four links fanning right to four leaf nodes; the three valid links as plain arrows, the forbidden link terminated with a blockage glyph. Channels: vertical position separates branches; the primary valid path uses the lead series treatment, the forbidden branch is set apart by its blockage terminator. Sort: three valid branches first, forbidden last. Annotation: leaf labels and the blockage marker. No zero baseline (decision tree). Deliverable: one HTML file, inline CSS, D3 7.9.0, responsive via ResizeObserver, role="img" with title and desc.

---

## References

1. Liu, N. F., et al. (2024). Lost in the Middle: How Language Models Use Long Contexts. *Transactions of the Association for Computational Linguistics*, 12, 157–173. https://aclanthology.org/2024.tacl-1.9/
2. Sharma, M., et al. (2023). Towards Understanding Sycophancy in Language Models. arXiv:2310.13548 (Anthropic). https://arxiv.org/abs/2310.13548
3. Claude Cowork product page (general-availability status; Skills/Plugins/Connectors architecture; 2026). https://claude.com/product/cowork
4. Context-window range (100k–1M tokens) across 2026 frontier models, Context Length Comparison: Leading AI Models in 2026. https://www.elvex.com/blog/context-length-comparison-ai-models-2026
