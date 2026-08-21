# Chapter 12 — Final Check and Build: EPUB + PDF

*Where the book ships — and discovers what the pipeline could not check on your behalf.*

---

This is the opening of an email a designer-author received from KDP in April 2026:

> Dear [name],
> Thank you for your submission. Your title, *AI for Designers: A Practitioner's Guide*, has been temporarily blocked from publishing for the following reasons:
> – Required metadata fields are incomplete. (Keywords: only 3 of 7 slots used. BISAC category: missing.)
> – Cover image does not meet specifications. Submitted file is 1200 × 1920 pixels; minimum height is 2560 pixels.
> – EPUB validation failed. Errors: 4 critical, 12 warnings. (Missing language metadata in OPF. Three images missing alt text. Navigation document structure violates EPUB 3.3 spec.)
> Please address the items above and resubmit.

The author did not write a bad book. The author wrote a book and skipped the final check sequence. Each of the three blockers takes a few minutes to fix and zero minutes to prevent. This chapter is the prevention.

Four things, in order. Run the Fact-Checking Assistant, triage, resolve the contradicted claims at minimum. Run `./build.sh` and produce the EPUB and the PDF. Read the EPUB on a device — not on a desktop, on an actual Kindle or the Kindle app on your phone. Submit to KDP. Then accept that you will rebuild. The rebuild loop is not a failure of the pipeline. It is the pipeline.

![Four step nodes — fact-check, build, device-read, submit — connected left to right by forward arrows, with a single curved return arc looping from the final node back to the build step to mark the intentional rebuild loop.](../images/12-final-check-and-build-fig-01.png)
*Figure 12.1 — The four-step ship sequence*

---

The Fact-Checking Assistant scans every chapter file and classifies every assertion along two dimensions: what kind of claim it is, and what the claim is about. The full prompt is reproduced in Appendix J — copy it from there, paste it into your project, and point it at your book directory.

The five claim types come from Sarah Harrison Smith's *The Fact Checker's Bible*, the procedure Smith built as head of research at the *New York Times Magazine*.[^smith] A **basic** claim is a plain factual assertion — "Pandoc converts Markdown to EPUB." An **emphatic** claim adds a strength qualifier — "Pandoc is the de facto Markdown-to-EPUB toolchain" — and the emphasis is what needs verifying. A **positive** claim is affirmative against an implied alternative — "Pandoc beats Calibre for reproducible builds" — and the comparison is the assertable thing. **I-language** claims are first-person assertions, hard to verify externally, usually flagged for caveat language. **Combination** claims carry two or more assertions in a single sentence; the checker decomposes them before verifying.

The six content categories are drawn from professional fact-checking practice — Peter Canby's department at *The New Yorker* is the gold standard.[^canby] **STAT** covers statistical claims, which must be verified against the primary source, not a derivative summary. **GUIDELINE** covers best-practice claims attributed to a standards body, verified against current published guidance. **APPROVAL** covers claims about authority decisions, verified against the authority's published policy as of a named date. **EVIDENCE** covers claims that evidence supports a conclusion, verified against the cited study with strength assessed. **SPECIALIST** covers claims attributed to a named expert, verified against published work. **CURRENT** covers claims true *now* — the most aging-prone category, requiring a verification date.

![A blank two-axis classification grid — five claim-type rows stacked down the left vertical axis, six content-category columns across the top horizontal axis, and the empty intersection matrix they define, with cell labels left for typography.](../images/12-final-check-and-build-fig-02.png)
*Figure 12.2 — Fact-check classification: claim type by content category*

Every assertion returns one of four statuses: VERIFIED, OUTDATED, CONTRADICTED, or UNVERIFIED. You triage in that exact order, because the order tracks both urgency and effort.

OUTDATED first. A claim that was true at writing time but is no longer true. *"KDP requires a 1600×2400 minimum cover"* — as of 2026 the minimum is higher. These are the fastest to fix: replace the number, re-verify, move on. They are also the most embarrassing if they ship.

CONTRADICTED second. A claim where the cited or implied source says something different from what the chapter claims. *"Pandoc supports EPUB 3.3 natively"* — Pandoc supports much of EPUB 3.3; some features require post-processing. These take longer because they require rewriting. They are the most important to catch — a contradicted claim is exactly the kind that gets quoted in a one-star review.

UNVERIFIED third. A claim the checker could not verify in either direction. *"About 80% of indie ebook units in the US are sold through KDP"* — no single authoritative source confirms this number. Two resolutions: find a source and upgrade to VERIFIED, or rewrite to make the uncertainty visible. *"Probably the largest share of indie ebook units in the US, though no single authoritative source confirms a precise figure"* is honest in a way the original was not.

![Three actionable status nodes — OUTDATED, CONTRADICTED, UNVERIFIED — arranged left to right in triage priority order and joined by progression arrows, with the VERIFIED node set off the action track as the resolved no-action state.](../images/12-final-check-and-build-fig-03.png)
*Figure 12.3 — The four-status triage order*

The pipeline does not require you to resolve every UNVERIFIED claim. It requires you to make a deliberate decision on each one — keep with caveat language, find a source, or remove the claim. The Fact-Checking Assistant writes its output to `factchecks/MASTER_REPORT.md` and inserts inline `<!-- FACT-CHECK FLAG -->` comments at every claim that did not return VERIFIED. The flags travel with the chapter file until you resolve them.

Two disciplines from *The Fact Checker's Bible*, sharpened for AI-drafted manuscripts. First, the author and the fact-checker are separate roles even when the same person — when you wear the fact-checker hat, you read as a stranger looking for what could be wrong, and the hat-switching is the discipline. Second, read aloud against the source. Smith's *New Yorker* procedure catches paraphrase drift — assertions that summarize a source in a direction the source does not actually go. AI-drafted text drifts this way often. The fact-check is the fluency-trap's final defense. Chapter 1 named the trap. Chapter 8 introduced the Combined Test. Chapter 10 tightened the pedagogy standard. This is the close.

[^smith]: Smith, S. H. (2004). *The Fact Checker's Bible: A Guide to Getting It Right*. Anchor.
[^canby]: Canby, P. Profiled in *Columbia Journalism Review*, 2015. The *New Yorker* fact-checking procedure.

---

The build script runs one command. You will run it many times before the book is finished.

What `./build.sh` actually does, in plain language: it reads every chapter file from `chapters/` in numerical order, concatenates them with the front and back matter into `output/combined.md`, runs pandoc with flags that produce a valid EPUB 3 and a PDF, and logs the build with timestamps and file sizes. The `output/` directory is gitignored. The build artifacts are not the source of truth. The source of truth is the chapter files plus `metadata.yaml` plus the images. You do not edit `combined.md` directly. You edit chapter files and rebuild.

Pandoc, written and maintained by John MacFarlane, is the toolchain's spine — the de facto Markdown-to-everything converter.[^pandoc] Two things to know about its EPUB output. Pandoc reads pandoc-flavored Markdown, slightly extended from GitHub-Flavored: footnotes, block-quotes, tables, code fences, and inline HTML (including the `<!-- FACT-CHECK FLAG -->` comments) all work. Pandoc's EPUB output is *mostly* EPUB 3 valid. Three things break regularly: missing `<language>` metadata (fix in `metadata.yaml`), images without alt text (fix in chapter files), and navigation-document structure for chapters with no h1. EPUBCheck (github.com/w3c/epubcheck) catches all three.

The build fails in four recognizable ways, each with a specific fix. Pandoc command not found means pandoc is not installed or not on PATH — install with `brew install pandoc` (Mac), `winget install JohnMacFarlane.Pandoc` (Windows), or `sudo apt install pandoc` (Linux). [verify — package names current as of May 2026] EPUBCheck errors point to two or three specific chapter files; address missing metadata first, then image alt text, then navigation structure. PDF rendering errors are usually a font issue — pass `--pdf-engine=weasyprint` if the LaTeX engine complains about missing fonts. [verify — pdf-engine flag values can drift] A file that builds but is mostly empty usually means the chapter file prefixes don't sort the way the script expects — confirm all chapter files start with two-digit prefixes (`01-`, `02-`, ... `12-`).

The diagnosis pattern is always the same: read the error message, find which step failed, fix the input file, rerun. Do not rebuild blindly hoping the error resolves.

[^pandoc]: MacFarlane, J. (2006–present). *Pandoc User's Guide*. pandoc.org/MANUAL.html.

---

Reading the EPUB on a device is the step every author resists and every author needs.

Pandoc's EPUB looks acceptable in Apple Books on a desktop, in any code-editor preview, in any browser-based reader. None of those are what your reader will use. Your reader will use a Kindle Paperwhite or Basic (e-ink, 6 inch, grayscale, slow refresh), a Kindle Colorsoft (e-ink with limited color), an iPad or iPhone Kindle app, or an Android Kindle app. E-ink Paperwhite is the cruel test. Gradients become bands. Subtle grays become indistinguishable. Custom fonts the reading system ignored fall back to a default weight that breaks the design. Color encoding becomes pure structural encoding — your blue-versus-red distinction becomes light-gray-versus-medium-gray, and if you relied on color to carry the difference, the chart now carries nothing.

Three things go wrong on every first-pass build. A figure is too small to read — the PNG was generated at 300 DPI but at small physical dimensions; on a 6-inch e-ink device it shrinks past legibility. Fix: redraw with larger type and fewer elements, or split into two figures. Not: upscale the PNG. A table is wider than the column — reflowable EPUBs cannot render wide tables on narrow screens; tables wider than roughly six viewport-widths break on phones. Fix: convert wide tables to bulleted lists or split. The W3C EPUB 3.3 spec does not require horizontal scrolling for wide content.[^epub33] A footnote rendered inline as parenthetical text — inline "(see footnote 1)" clutters small screens; EPUB has popup footnotes via `<aside epub:type="footnote">` that pandoc generates from Markdown footnote syntax (`[^1]`); convert inline parentheticals and rebuild.

You will find others specific to your book. Read every chapter on the device. Note three things to fix per chapter. Fix. Rebuild. Read again. The rebuild loop has started.

[^epub33]: W3C. (2023). *EPUB 3.3 Specification*. w3.org/TR/epub-33/.

---

Kindle Direct Publishing (kdp.amazon.com) accounts for the dominant share of indie ebook units in the US as of May 2026. [verify — share estimates from 2025 Authors Guild and industry analyst sources, subject to drift] The submission flow has five parts and takes about forty-five minutes the first time.
<!-- FACT-CHECK FLAG: UNVERIFIED — see factchecks/12-final-check-and-build-assertions.md -->

Before the details: every form field name, every dropdown option, every price-tier rule, and every program-eligibility requirement in this section is current-state as of May 2026 and carries the highest aging risk in this book (TIKTOC.md Part 11). The KDP dashboard changes meaningfully every six to twelve months. Re-check every detail against kdp.amazon.com before submitting. The *structural framework* of submission — account, metadata, cover, manuscript, pricing — is stable. The specific *fields* are not. [verify — all KDP submission details throughout this section]

**Account.** You need a KDP account (free) and a bank account Amazon's payment system supports. The first time, you complete a tax interview (W-9 for US residents, W-8BEN for others) and a banking form — about fifteen minutes, not repeated for future books.

**Metadata.** From the KDP dashboard: *Create New Title → Kindle eBook*. Title and subtitle (subtitles count toward search relevance). Series name (optional; links related books). Author name (the name you want in perpetuity; pen names accepted). Description (up to 4,000 characters — write it as carefully as Chapter 1). Keywords (seven slots; use all seven; each can be a phrase; Dave Chesson's Kindlepreneur is the practitioner reference [verify — slot count subject to change]). Categories (two from KDP's hierarchy, as specific as possible). And the AI-content disclosure introduced in September 2023: Amazon requires you to disclose *AI-generated* content but not merely *AI-assisted* content. AI+1 books use AI-assisted drafting — Cowork drafts, human rewrites — which falls under Amazon's *AI-assisted* category, so a disclosure is not strictly required; confirm the current boundary before you declare. [verify — disclosure boundaries have shifted multiple times since 2023 and remain unsettled]

**Cover.** JPEG or TIFF, RGB color space, ideally 2560 × 1600 pixels, minimum 1000 × 625. Ideal ratio at least 1.6:1. File under 50MB. [verify — cover spec is the single most aging-prone detail in this section] The designer-reader has a real advantage here. Design the cover at the recommended size, in a sans-serif typeface that survives thumbnail rendering, with the title legible at 200-pixel preview width. Amazon's discovery surfaces show 200-pixel thumbnails primarily. The cover that wins is the one that reads at that scale.

**Manuscript.** Upload `output/[book-slug].epub`. KDP runs its own EPUB validation and previews in their Online Previewer — the minimum device check. You have already done the real check: the device read in the previous section. If the Online Previewer flags issues, fix in chapter files and rebuild.

**Pricing and KDP Select.** The AI+1 series ships at $0.99. The case is pedagogical, not commercial: the audience is freelance professionals and workshop participants who can sample, decide, and commit at low risk. A $20 textbook is friction. A $1 textbook is a one-click decision. The price is part of the pedagogy.

The KDP royalty structure: books priced between $2.99 and $9.99 earn 70%. Outside that range — including $0.99 — 35%. At $0.99 you keep about $0.35 per sale. The economic case is volume, not margin. This is a contested position. The Authors Guild argues low price points depress perceived value.[^authorsguild] Mike Shatzkin argues pricing is contextual and low points work for narrow professional handbooks. Joanna Penn frames pricing as one variable inside a multi-stream income model.[^penn] The $0.99 decision for this series is a defensible bet, not settled strategy.

KDP Select grants Amazon 90-day exclusivity — no distribution through Apple Books, Kobo, or your own site — in exchange for Kindle Unlimited inclusion, promotional pricing windows, and debated discoverability benefits. [verify — 90-day term, KU page-read economics, and Countdown Deal rules subject to Amazon policy change] Pro (Howey, Penn early-career): KU access dwarfs the cross-platform reach most new authors would build otherwise. Con (Penn more recent, authors with existing mailing lists): exclusivity locks you out of platforms where your audience already exists. For the AI+1 series the decision was to enroll: audience is on Amazon, workshop distribution is well-served by KU, cross-platform loss is acceptable at current series scale. Defensible, not the only defensible position.

![A step function of royalty rate against list price on a zero-based percentage axis — a low 35% band below $2.99, a raised 70% band between $2.99 and $9.99, a drop back to 35% above $9.99, with a single marker on the $0.99 series price sitting in the leftmost low band.](../images/12-final-check-and-build-fig-04.png)
*Figure 12.4 — KDP royalty tiers by price*

Click *Publish*. The book enters review. Approval typically arrives within 24–72 hours.

[^authorsguild]: Authors Guild. (2025). Survey of member pricing and perceived value. authorsguild.org.
[^penn]: Penn, J. (2021). *How to Make a Living with Your Writing* (3rd ed.). Curl Up Press.

---

The worked example is the complete KDP submission for *ai-for-designers* captured from the dashboard on May 14, 2026. Every field is current-state as of that date and subject to drift — re-verify against the live dashboard before submitting.

Title: *AI for Designers*. Subtitle: *A Practitioner's Guide*. Series: AI+1, volume 1. Author: Bear Brown. Description: *A working handbook for freelance graphic designers integrating AI into client practice. From brief intake to portfolio positioning, this book teaches AI+1 fluency — the AI literacy that makes you more valuable to your clients, not interchangeable with the model.* Keywords, all seven slots: AI for designers; graphic design workflow; Claude for creatives; freelance design business; AI tools for designers; Adobe Firefly Midjourney Figma; design practitioner handbook. Categories: Computers & Technology → AI & Semantics; Arts & Photography → Graphic Design → Commercial. AI-content disclosure: AI-assisted. Cover: 2560 × 1600 JPEG, RGB, flat fills in ink and ochre on cream, title legible at 200-pixel thumbnail. [verify — pixel specs subject to drift] Manuscript: `output/ai-for-designers.epub`. EPUBCheck result: 0 critical errors, 2 informational warnings. KDP Online Previewer: all 11 chapters rendered cleanly. Price: $0.99 USD, 35% royalty tier. KDP Select: enrolled, 90-day exclusivity from publish date. [verify — KDP Select term subject to Amazon policy change] Status: approved 27 hours after submission, May 15, 2026. Live on Amazon.com and every regional storefront.

<!-- → [TABLE: KDP submission checklist — two columns: field/step and verification note — covering all five submission stages with aging-risk flags on the fields most likely to drift] -->

| Field / step | Verification note |
|---|---|
| Account — KDP account + supported bank account | One-time tax interview (W-9 US, W-8BEN non-US) and banking form, about fifteen minutes; not repeated for future books. |
| Metadata — title and subtitle | Subtitles count toward search relevance; write them deliberately. |
| Metadata — series name | Optional; links related volumes (AI+1, volume 1). |
| Metadata — description | Up to 4,000 characters. [verify — character limit subject to drift] |
| Metadata — keywords | Seven slots; use all seven; each can be a phrase. [verify — slot count subject to change] |
| Metadata — categories | Two from KDP's hierarchy, as specific as possible. |
| Metadata — AI-content disclosure | AI-assisted (not AI-generated) for the AI+1 drafting model. [verify — disclosure boundaries unsettled since 2023] |
| Cover — file | JPEG or TIFF, RGB, ideally 2560 × 1600, minimum 1000 × 625, ratio at least 1.6:1, under 50MB. [verify — most aging-prone detail in this section] |
| Manuscript — upload | Upload `output/[book-slug].epub`; KDP runs its own validation and Online Previewer. |
| Pricing — list price | AI+1 series ships at $0.99 (35% royalty tier). [verify — royalty-tier boundaries subject to Amazon change] |
| Pricing — KDP Select | 90-day exclusivity for Kindle Unlimited inclusion. [verify — term and KU economics subject to policy change] |
| Publish — review | Approval typically within 24–72 hours. [verify — review window subject to drift] |

---

After the device read, the fact-check resolution, and the KDP submission, the book is live. The reader who picks it up tomorrow morning reads version 1.0.0.

You will rebuild. The rebuild is normal.

Tom Preston-Werner's Semantic Versioning — MAJOR.MINOR.PATCH — is the right mental model for a versioned book.[^semver] PATCH is a typo fix, an errata update, a current-state claim that aged — 1.0.0 becomes 1.0.1. MINOR is a new chapter or substantial revision — 1.0.0 becomes 1.1.0. MAJOR is a second edition: new chapters, restructured TOC, material rewrites — 1.x becomes 2.0.0. KDP supports updates through the dashboard. Existing readers may or may not receive the new version automatically; Amazon's auto-update logic is undocumented. Treat PATCH as routine; MINOR and MAJOR as occasions to consider whether the new content warrants a push request to KDP support.

The fast rebuild cycle takes about thirty minutes the first time and fifteen after the first half-dozen: open the chapter file, make the change, run `./build.sh`, run EPUBCheck if the change touched structure, open on device, upload to KDP (the form recognizes the existing book and treats the new EPUB as an update), bump the version in `metadata.yaml`, commit.

Before each MINOR or MAJOR version push, run a four-question audit against the AI+1 standard. First, do every LLM Exercise still pass the three-question audit from Chapter 10 — the test, the requires-domain-knowledge condition, the judgment-not-generation condition? Pull three at random and score them. Second, is the reader still being treated as a domain expert acquiring AI fluency, not a generic AI user acquiring domain content? Read the introduction and one mid-book chapter. Third, pick three exercises at random — if any one of them reads as "ask Claude to explain X," the pedagogical fluency trap is back. Fourth, read one chapter aloud: does it sound like you, or does it sound like a Cowork dump? Drift happens between revisions.

A book that passes all four is shippable. One that fails one is fixable. One that fails three is in trouble — the human rewrite from Chapter 8 was not held over enough revisions.

[^semver]: Preston-Werner, T. (2013). *Semantic Versioning 2.0.0*. semver.org.

---

## AI Wayback Machine — Aldus Manutius

Most readers who know the history of printing know Gutenberg. Fewer know Aldus Manutius — and what Manutius did is the more direct precedent for the AI+1 series' $1 Kindle decision.

Gutenberg invented movable type. Manutius invented the *portable book*. Working in Venice between 1494 and 1515, he produced octavo editions — small enough to carry in one hand — of Greek and Latin classics that previously existed only as heavy folios in institutional libraries. He called the format the *enchiridion*: handbook. He commissioned the first italic typeface, cut by Francesco Griffo around 1500, to fit more text on a smaller page without sacrificing legibility. He standardized punctuation, including a recognizable semicolon.

What Manutius understood, that the AI+1 series tries to inherit: the format of a book is a decision about who the book is for. A heavy folio is for an institution. A portable octavo is for a reader who wants the text close at hand, on the road, between client meetings. The format is the access strategy. The price follows from the access strategy. The $1 Kindle is the same move at a different turn of the wheel.

> **Prompt to run in Claude or ChatGPT:**
>
> "Visit the Wikipedia page for Aldus Manutius. Read about the octavo enchiridion format and the Aldine Press design choices. Identify three specific Manutius decisions — about format, typeface, or price — and pair each with an analogous decision in the AI+1 production pipeline. Then verify Claude's claims against the Wikipedia sources, and note any cases where Claude's account of a Manutius decision drifts from the Wikipedia account."

The verification instruction is deliberate. The Aldine Press catalog at UCLA is one canonical secondary source. The prompt asks you to catch the model doing the thing Chapter 1 warned against — claiming authority without grounding. The fact-check habit starts before the book is finished and runs through the next one.

---

## Exercises

**Exercise 12.1 (Apply) — Run the Fact-Checking Assistant and resolve one finding.** Run the Fact-Checking Assistant across your book. Open `factchecks/MASTER_REPORT.md`. Triage in the order OUTDATED → CONTRADICTED → UNVERIFIED. Identify at least one OUTDATED finding and resolve it by updating the chapter file, then rerun the checker against that chapter to confirm. If no OUTDATED findings exist, identify at least one CONTRADICTED finding and resolve it. Document the original claim, the contradicting source, and the rewrite.

**Deliverable:** The resolved finding, with original claim, source, and revised text shown side by side.

**Exercise 12.2 (Apply) — Build and read on a device.** Run `./build.sh`. Confirm `output/[book-slug].epub` and `output/[book-slug].pdf` are produced. Open the EPUB on a Kindle device or in the Kindle app on your phone — not on a desktop. Scroll through every chapter. Note three specific things to fix: at minimum one figure rendering issue, one table or list issue, and one footnote or sidebar issue. For each, record the chapter, the location, and the proposed fix.

**Deliverable:** A list of three issues with chapter, location, and proposed fix.

**Exercise 12.3 (Apply) — Fix, rebuild, confirm.** Apply the three fixes from Exercise 12.2 to the relevant chapter files. Run `./build.sh`. Open the EPUB on the device again. Confirm all three issues are resolved.

**Deliverable:** A one-paragraph note per fix confirming resolution, plus the rebuilt EPUB file.

**Exercise 12.4 (Evaluate) — AI+1 final assessment.** Run the four-question AI+1 assessment. Does every LLM Exercise pass the three-question audit from Chapter 10? Is the reader still being treated as a domain expert, not a generic AI user? Pick three exercises at random — are any in the form "ask Claude to explain X"? Read one chapter aloud — does it sound like you? Write a one-paragraph assessment per question with concrete evidence from the manuscript. Identify the strongest passing dimension and the weakest. State whether the book is shippable, fixable, or in trouble.

**Deliverable:** Four one-paragraph assessments with evidence.

---

## Closing

The book is live on KDP. A reader who just finished this chapter is an author-instructor with a Kindle-ready AI+1 textbook. The TIKTOC.md session that started everything was two hours, months ago. The Cowork drafts were rewritten chapter by chapter. The figures encode arguments. The LLM Exercises pass the standard. The fact-check ran. The build ran. The submission cleared.

The book sits on Amazon. Someone is about to download it.

And the rebuild loop is already starting. You will read your own book on a Kindle next week and find three things you missed. A reader will email about a fourth. A new client engagement will give you a worked example you wish you had included. KDP will change a form field and you will rebuild to keep current.

This is not failure. This is the pipeline at work. A book is not finished the way a building is finished. It is finished the way software is finished — versioned, patched, occasionally re-edited. Every course run produces new cases. Every workshop produces new failure modes. Every new model release produces new capabilities to integrate.

The TIKTOC.md is still on disk. The `chapters/` directory still exists. The build script still runs.

Monday morning, you will look at the next book you want to build. You will open Tic TOC. You will run `/i1`. The next pipeline is ready when you are.

---

## Prompts

### Figure 12.1 — The four-step ship sequence
Build a horizontal process flowchart with a return loop as a single self-contained HTML file with inline CSS and D3 7.9.0 from the CDN. Data: four sequential step nodes (fact-check, build, device-read, submit) plus one return arc from the final node back to the build step. Marks: four rectangle nodes joined by left-to-right forward arrows, and one curved return arc drawn distinctly. Channels: x position encodes step order; the curved arc encodes the intentional rebuild loop. Keep steps in fixed order; do not sort. No quantitative scale. Annotate each node with its step name and label the arc as the rebuild loop. Use the red series color for the return arc only. Deliverable: one HTML file, role="img" SVG with title and desc, ResizeObserver redraw, dark-mode and reduced-motion media queries.

### Figure 12.2 — Fact-check classification: claim type by content category
Build a blank two-axis classification grid as a single self-contained HTML file with inline CSS and D3 7.9.0 from the CDN. Data: five claim-type rows (basic, emphatic, positive, I-language, combination) and six content-category columns (STAT, GUIDELINE, APPROVAL, EVIDENCE, SPECIALIST, CURRENT), defining an empty 5 by 6 intersection matrix. Marks: a ruled grid with a labeled left vertical axis band and a labeled top horizontal axis band; cells left empty. Channels: row position encodes claim type; column position encodes content category. Keep both axes in fixed order; do not sort. No quantitative scale. Annotate only the axis labels — leave all 30 cells blank. Use neutral palette colors for the axis bands; reserve the red series color for at most one emphasis element. Deliverable: one HTML file, role="img" SVG with title and desc, ResizeObserver redraw, dark-mode and reduced-motion media queries.

### Figure 12.3 — The four-status triage order
Build an ordered priority sequence as a single self-contained HTML file with inline CSS and D3 7.9.0 from the CDN. Data: three actionable statuses in triage order (OUTDATED, CONTRADICTED, UNVERIFIED) plus VERIFIED set aside as the no-action terminal. Marks: three nodes on a horizontal track joined by progression arrows, and one VERIFIED node placed off the track. Channels: x position encodes triage priority; off-track placement encodes the resolved state. Keep statuses in fixed triage order; do not sort. No quantitative scale. Annotate each node with its status name and mark VERIFIED as requiring no triage. Use the red series color for the OUTDATED node only (fastest, most embarrassing); render the others in neutral palette colors. Deliverable: one HTML file, role="img" SVG with title and desc, ResizeObserver redraw, dark-mode and reduced-motion media queries.

### Figure 12.4 — KDP royalty tiers by price
Build a step-function chart as a single self-contained HTML file with inline CSS and D3 7.9.0 from the CDN. Data: royalty rate as a function of list price — 35% below $2.99, 70% between $2.99 and $9.99, 35% above $9.99 — plus a single marker at the $0.99 series price in the low band. Marks: a stepped line or banded area profile and one point marker. Channels: x position encodes list price increasing rightward; y position encodes royalty percentage. Use a linear y-scale with a zero baseline; the royalty axis starts at zero. Do not sort; price runs naturally left to right. Annotate the three bands with their rates, the breakpoints at $2.99 and $9.99, and the $0.99 marker. Use the red series color for the $0.99 decision marker only; render the bands in neutral palette colors. Deliverable: one HTML file, role="img" SVG with title and desc, ResizeObserver redraw, dark-mode and reduced-motion media queries.

---

## References

1. KDP. "What criteria does my eBook's cover image need to meet?" https://kdp.amazon.com/en_US/help/topic/G200645690
2. KDP. "Digital Book Pricing Page" (royalty tiers). https://kdp.amazon.com/en_US/help/topic/G200634500
3. KDP. "KDP Select." https://kdp.amazon.com/en_US/help/topic/G200798990
4. Authors Guild (2023). "Amazon's New Disclosure Policy for AI-Generated Book Content" (policy announced September 2023). https://authorsguild.org/news/amazons-new-disclosure-policy-for-ai-generated-book-content-is-a-welcome-first-step/
5. MacFarlane, J. *Pandoc User's Guide* / "Creating an ebook with pandoc." https://pandoc.org/MANUAL.html
6. W3C (2023). *EPUB 3.3* (Recommendation, 25 May 2023). https://www.w3.org/TR/epub-33/
7. Preston-Werner, T. (2013). *Semantic Versioning 2.0.0*. https://semver.org/
8. Wikipedia. "Aldus Manutius." https://en.wikipedia.org/wiki/Aldus_Manutius
