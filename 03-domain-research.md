# Chapter 3 — Domain Research: The Chapter Before the Chapter

*One LLM gives you an answer. Three give you a map of what is settled, what is contested, and what nobody noticed.*

---

In May 2026 the same prompt was sent verbatim to three frontier large language models: Claude, GPT-4, and Gemini 1.5. The question was identical. The outputs were not.

The prompt asked each model to describe AI tool adoption in graphic design — the first of eight structured sections. Here is roughly the opening hundred words of each response, trimmed for the page.

**Claude** (with web research enabled):

> *Adoption of generative AI in graphic design has shifted from experimental to embedded over 2023–2026. Major design tools now ship AI features as defaults rather than add-ons: Adobe Firefly is integrated into Photoshop and Illustrator; Figma launched Figma AI at Config 2024; Canva's Magic Studio brought generative AI into the small-business design market. I should flag that headline adoption percentages vary considerably across reports depending on what counts as "use," and many of the most-cited figures come from vendor-published research with potential incentive bias.*

**GPT-4:**

> *AI tool adoption in graphic design has accelerated dramatically. Studies show that over 90% of graphic designers now use AI-powered tools weekly, with adoption highest among social media designers and lowest among high-end brand identity practitioners. The general pattern is that AI is most embedded in production workflows and least embedded in strategic and brand decisions.*

**Gemini 1.5:**

> *Graphic design has experienced one of the highest AI adoption rates in creative professions. Specific data from Figma's State of the Designer 2026 and the Adobe Creative Trends Report 2025: 93% of graphic designers use AI-powered tools at least once a week; 82% use them to overcome "blank canvas syndrome"; only 12% trust AI tools for high-stakes branding for Fortune 500 companies. The adoption story is not whether AI is used — it is — but for what.*

Three responses. Same question. Three signatures.

All three identify AI adoption as widespread and structurally embedded. All three name the same vendors. All three identify the same pattern — heavy adoption in production work, light adoption in strategic and brand work. This is settled territory.

On specificity they diverge. Claude qualifies and discloses vendor-bias risk without naming numbers. GPT enumerates confidently without sources — "over 90% weekly use," attributed to "studies." Gemini cites specific percentages from named reports — "93% at least once a week" from Figma 2026. The numbers in GPT and Gemini are close but not identical, which means they are either reporting different cuts of the same survey or different surveys entirely. Neither model flags the discrepancy.

And then there is the thing one model surfaced that the other two missed. Only Gemini named the 12% high-stakes-trust figure — the finding that while nearly every designer uses AI for production work, almost none trusts it for Fortune 500 branding. Claude and GPT both gestured at the same general pattern. Only Gemini retrieved the specific number that makes the pattern precise.

That is the entire argument for the three-LLM domain research prompt. One model gives you an answer. Three give you the map of confidence — what is settled, what is contested, what is conjecture, and what one model retrieved that the others missed. The rest of this chapter is how to draw that map for your own field.

![Three equal text-block panels side by side under one shared "same question" input node that splits into three arrows. The left panel (Claude) carries hollow hedge-ring markers in its margin for explicit uncertainty; the center panel (GPT) carries uniform solid enumerated bars with no source ticks for confident listing; the right panel (Gemini) carries solid bars with attached source-pin marks for retrieval-grounding. The three signatures are contrastable from the margin markers alone, without reading any text.](../images/03-domain-research-fig-01.png)
*Figure 3.1 — Three LLM signatures on the same question*
<!-- → [INFOGRAPHIC: three-column side-by-side of the three LLM opening paragraphs, annotated to show the uncertainty-explicit signature (Claude), the confident-enumeration signature (GPT), and the retrieval-grounded signature (Gemini) — arrows pointing to specific phrases that exemplify each] -->

---

Why three models and not one? Why not five?

The case for three is empirical, methodological, and practical. Each frontier model has a distinctive output signature shaped by its training data, its reinforcement conditioning, and its safety design. Claude is trained under Constitutional AI methodology and tends toward explicit uncertainty markers and nuanced qualification.[^anthropic] GPT-4 is optimized for instruction-following and structured enumeration, with less native tendency to surface its own doubt.[^openai]
<!-- FACT-CHECK FLAG: UNVERIFIED — see factchecks/03-domain-research-assertions.md -->
 Gemini is multimodal-first and tightly integrated with Google Search, producing outputs that are more retrieval-grounded and more likely to name specific sources with specific numbers.[^gemini]
<!-- FACT-CHECK FLAG: UNVERIFIED — see factchecks/03-domain-research-assertions.md -->


These signatures are temporally unstable [contested — practitioner observation; model behavior shifts across versions and within versions over months]. What is true of these three models in May 2026 will not be true two years from now. The *practice* of comparing across three models survives the signature shift, because the logic does not depend on any particular model's character — it depends on their independence.

That independence is the methodological anchor. Norman Denzin's *The Research Act* (1978) names the practice as investigator triangulation — using multiple independent investigators with different known biases to catch what any single one misses.[^denzin] Where independent investigators converge, the claim is more credible. Where they diverge, the contested territory becomes visible. The three frontier LLMs satisfy the independence condition weakly: they share enormous overlap in training data, share many of the same safety conditioning regimes, and are not fully independent in any rigorous statistical sense. But they satisfy the independence condition better than any single model does on its own. The convergence patterns that emerge are more legible across three than across one, and the divergent-as-gap pattern — one model retrieving something the others missed — only becomes visible when there are others to miss it.

James Surowiecki's argument in *The Wisdom of Crowds* (2004) applies here under qualification.[^surowiecki] Aggregation outperforms individual estimates when four conditions hold: diversity of opinion, independence, decentralization, aggregation. The three LLMs satisfy these conditions weakly — the training-data overlap undermines full independence — so the wisdom-of-crowds claim must be held lightly. This is approximate triangulation, not the statistical kind.

The practical case is the diminishing-returns curve. A fourth model (an open-source frontier model, a specialized domain model) doubles runtime cost and rarely doubles the signal — most of what the fourth model adds restates what one of the first three already said. Two models is almost enough but misses the third-perspective check that catches the divergent-as-gap finding. Three is the local optimum for the solo author-instructor working under time pressure.

This is not a peer-reviewed methodology [verify — no controlled study confirms three-LLM rotation produces better domain research than single-LLM use with rigorous verification]. Treat it as a defensible practitioner convention with strong analogical support from qualitative research methods. The claim is: it works better than one, not as a universal truth but as a repeatable practical result.

[^anthropic]: Anthropic. (2024–2025). *Claude prompting guide* and *Anthropic research blog posts on Constitutional AI*. Anthropic.
[^openai]: OpenAI. (2023–2025). *Model cards and system cards for GPT-4, GPT-4o, GPT-5*. OpenAI.
[^gemini]: Google DeepMind. (2024–2025). *Gemini technical reports and model cards*. Google DeepMind.
[^denzin]: Denzin, N. K. (1978). *The Research Act: A Theoretical Introduction to Sociological Methods* (2nd ed.). McGraw-Hill.
[^surowiecki]: Surowiecki, J. (2004). *The Wisdom of Crowds*. Doubleday.

---

The prompt that produced the three opening paragraphs above has eight sections. The structure is not arbitrary. Each section asks for a specific kind of evidence; together they produce what a Tic TOC /i1 session needs in order to start productive rather than stalling on basic context.

Here is the full prompt. The only substitution you make is the profession in brackets; every other word runs verbatim across all three models. Changing the sections per-model destroys the triangulation — you cannot tell whether a divergence reflects the model or the prompt.

> *I am a [your profession] researching how AI is currently affecting my profession. Please produce a structured report with the following eight sections:*
>
> *1. AI tool adoption by role and workflow stage*
> *2. Documented failure modes when AI is used in this work*
> *3. Copyright, IP, and legal-exposure landscape*
> *4. The fluency trap pattern in this domain — output that looks professional but fails expert review*
> *5. Labor-market data: postings, rates, displacement, wage premium*
> *6. The irreducibly human taxonomy — what AI cannot do here*
> *7. Existing training and certification for AI literacy in this field*
> *8. The context-specific risks for solo or one-primary-client practitioners*
>
> *For each section: cite sources where you can; mark contested claims; distinguish current-state from settled territory. Length: roughly 1,500–2,500 words.*

What each section is *for*, briefly stated:

Section 1 inventories what tools are actually being used, by whom, at what step. This becomes the state-of-the-field anchor for everything the book claims about AI's current penetration into your domain. Section 2 is the fluency trap inventory — the documented failure modes specific to your work. This is the spine of the book's first chapter. Section 3 is the legal and IP landscape; it looks completely different for a designer (copyright doctrine, *nemo dat*) than for a nurse practitioner (FDA disclosure, scope of practice) or a litigator (model rules of professional conduct). Section 4 asks the models to name the specific local instances of fluency-trap failure that an expert would catch and a non-expert would not. This is the hardest section to get right and the most valuable to triangulate. Section 5 is labor-market arithmetic — the evidence base for any claim that AI creates both threat and opportunity for your readers right now. Section 6 is the protect column — what AI cannot do in your domain, stated as specifically as the models can manage. Section 7 is the market gap — what training and certification already exists, which tells you what your book is not and what space it fills. Section 8 is the deployment-specific risk layer — what specifically is at stake for the kind of practitioner your book is written for.

The closing instruction — *cite sources where you can; mark contested claims* — changes the register of what comes back. Without it, the models produce summary text at blog-post confidence. With it, you get something closer to a research memo with hedges. The hedges are the signal.

![A left-to-right crosswalk schematic mapping the eight research-prompt sections to the Tic TOC intake targets. Eight uniform section blocks are stacked on the left; five intake-target nodes (/i2, /i3, /i4, /l1, /m1) are stacked on the right; thin connector lines link each section to the intake question it feeds, drawn only for the mappings the chapter states.](../images/03-domain-research-fig-02.png)
*Figure 3.2 — Eight-section prompt mapped to Tic TOC intake*

<!-- → [TABLE: eight-section prompt schema — three columns: section number, what it asks for, what Tic TOC intake question it feeds — showing how each research section maps to /i2, /i3, /i4, /l1, /m1] -->

| Section | What it asks for | Tic TOC intake question it feeds |
|---|---|---|
| 1. AI tool adoption | What tools are used, by whom, at what workflow step | /i2 — state of the field |
| 2. Documented failure modes | The fluency-trap inventory specific to this work | /l1 — first-chapter spine |
| 3. Copyright, IP, legal exposure | The legal and IP landscape for this domain | /m1 — domain-specific risk intake |
| 4. The fluency trap pattern | Local instances an expert catches and a non-expert misses | /l1 — first-chapter spine |
| 5. Labor-market data | Postings, rates, displacement, wage premium | /i2 — state of the field |
| 6. Irreducibly human taxonomy | What AI cannot do here, stated specifically | /i4 — thesis |
| 7. Training and certification | What already exists, and the gap it leaves | /i2 / /m1 — positioning and market gap |
| 8. Solo-practitioner risk | What is at stake for this reader's deployment | /i3 — specific reader profile |

---

You now have three documents. Each runs 1,500 to 3,200 words. The synthesis is the load-bearing skill.

Read all three outputs in one sitting, without yet writing anything. Read for the pattern of overlap. You are looking for four categories of claim:

**ALL THREE AGREE** means the claim appears in all three responses with consistent framing. Treat it as settled territory. Quote one model's clearest formulation and move on.

**TWO AGREE** means two of three produce the claim; one omits or contradicts. Flag as probably-settled, note the dissenter.

**DIVERGENT** means the models disagree on substance, magnitude, or interpretation. State all positions. Do not synthesize prematurely — the divergence is the finding.

**ONE ONLY** means one model raises a claim the other two did not. Investigate whether the omission is a gap (the other two missed something real) or a correction (the other two are right to exclude it). Verify before including.

![Three overlapping circles, one per source LLM, drawn as outlines so the overlap regions read. Leader dots call out the four marker regions: the central triple-overlap is ALL THREE AGREE, a pairwise-overlap lens is TWO AGREE, and a single-circle crescent is ONE ONLY. A separate forked-arrow marker beside the cluster denotes DIVERGENT — all positions stated, not merged — since divergence is disagreement rather than absence of overlap. The key is source-agnostic and carries no model names.](../images/03-domain-research-fig-03.png)
*Figure 3.3 — The four synthesis markers*
<!-- → [TABLE: synthesis marker table — four rows, three columns: marker, meaning, what to do — as described in the paragraph above] -->

| Marker | Meaning | What to do |
|---|---|---|
| ALL THREE AGREE | The claim appears in all three responses with consistent framing | Treat as settled territory; quote the clearest formulation and move on |
| TWO AGREE | Two of three produce the claim; one omits or contradicts | Flag as probably-settled; note the dissenter |
| DIVERGENT | The models disagree on substance, magnitude, or interpretation | State all positions; do not synthesize prematurely — the divergence is the finding |
| ONE ONLY | One model raises a claim the other two did not | Decide whether it is a gap or a correction; verify before including, then attribute |

Here is what those four categories look like in practice, drawn from the running example:

*ALL THREE AGREE on the fluency trap definition.* All three models, asked to describe the fluency trap pattern in graphic design, produce variants of "AI generates output that looks professional but lacks the craft judgment, brand knowledge, or strategic rationale to survive expert review." The wording differs; the substance is identical. Quote the clearest formulation and move on.

*TWO AGREE on the wage premium magnitude, but the dissenter is reporting a different cut of the same dataset.* Claude and Gemini both cite PwC 2025's 56% wage premium figure with the U.S./advanced-skills qualifier. GPT-4 cites "approximately 25% wage premium" without source or qualifier — likely the global average from the same report rather than the U.S. cut. The 56% number is probably right for the context this book uses it; the 25% is probably right for a different context. Flag both, attribute both, let the reader see the variance.

*DIVERGENT on whether AI is displacing junior designers.* Claude: "junior production tasks are being automated, with mixed evidence on entry-level hiring." GPT: "AI is creating new junior roles in AI-assisted production." Gemini: "the junior pipeline gap is an underreported design crisis — agencies are hiring fewer juniors because AI handles their tasks." Three positions ranging from cautious through optimistic through alarmed. The divergence is the finding. State all three. Do not resolve.

*ONE ONLY on the IP doctrine name.* Gemini surfaced *nemo dat quod non habet* — "you cannot give what you do not have" — as the foundational legal principle for designers assigning AI-generated work to clients. Claude and GPT both discussed copyright issues for AI-generated work without naming the doctrine. This is the divergent-as-gap pattern. The claim checks out against U.S. Copyright Office guidance and the current case law [verify — Thaler v. Perlmutter, D.C. Circuit, 2025]. Include it in the synthesis, attribute it to Gemini, note that the other two omitted it rather than contradicted it.

The synthesis is **not averaging**. Averaging loses the expert-judgment move that is the whole point of the exercise. You are reading three differently-biased reports and applying domain expertise to triage. Where you know the field, you choose. Where you do not, you flag.

The output is a single document organized by the eight original sections — roughly 600 to 800 words total. Every claim carries one of the four markers. Contested claims are stated as contested. ONE ONLY claims are attributed. This document is what Chapter 4 takes in.

---

Before you call the synthesis done, run a five-minute fluency trap check on your own research output. The trap that Chapter 1 describes at the deliverable level runs identically at the research level, at lower stakes. This is the rehearsal.

Three patterns to watch for:

*The invented citation.* A model says "according to a 2024 Stanford study" with no further metadata, and the study does not exist. This is rarer in 2026 than it was in 2023 but still occurs, especially in lower-traffic subfields. When a claim is anchored to a specific named study without enough metadata to verify, search for the study before quoting it. If it does not exist, the underlying claim may still be true — but the study cannot be cited, and the model's confidence cannot carry into your brief.

*The conflated finding.* A model reports "PwC found a 56% wage premium for AI skills" without naming the geography or skill-level cut. The 56% figure is real; it is the U.S./advanced-AI-skills cut of the PwC 2025 AI Jobs Barometer. Quoting it without the qualifier turns a defensible regional finding into an indefensible global claim. Find the original source, add the qualifier, or drop the number.

*The precision illusion.* Gemini reported "93% of graphic designers use AI weekly" — a precise-feeling number that comes from a specific named report (Figma's State of the Designer 2026). GPT reported "over 90%." Claude reported "a substantial majority." All three are probably describing the same underlying survey, but only Gemini names the source. The 93% is defensible; verify the methodology before treating it as canonical.

The fluency trap check is a five-minute pass: for each numeric claim and each named study, ask *can I verify this in five minutes?* If yes, do. If no, downgrade the claim — replace "X%" with "a majority" or with `[verify]`. You will run this same move in Chapter 6 when evaluating pantry research output, in Chapter 8 when rewriting Cowork drafts, and in Chapter 12 with the Fact-Checking Assistant. The habit starts here.

---

The synthesis produces 600 to 800 words with four-marker provenance on every claim. That document then gets distilled one further step into a four-section brief — the format Tic TOC's /i1 session actually reads.

The four sections collapse the eight-section synthesis into the structure that maps onto Tic TOC's intake questions. Section A is the state of the field — what is settled, what is contested, what is current-state — drawing from LLM sections 1, 5, and 7. Section B is the fluency trap and irreducibly human taxonomy — the failure modes specific to your domain and the corresponding human-retained competencies — drawing from sections 2, 4, and 6. Section C is the reader's specific risk context — the risks and opportunities for the particular kind of practitioner your book is written for — drawing from section 8. Section D is the market gap and book positioning — what training exists, what does not, what the book's specific contribution is — drawing from section 7.

Total brief length: 700 to 1,400 words. No longer. The brief is a working document, not a publication. If it runs longer, the /i1 session loses focus on actionable items. If it cannot answer four questions — *who is your specific reader; what is the central professional risk your book argues against; what is the current state of AI that makes the book necessary now; what existing materials does the book sit beside and what gap does it fill* — the session stalls, and you spend the first thirty minutes of your timebox drafting answers in real time. Forty minutes on the brief saves an hour of stalling.

![A left-to-right proportional funnel in four stages. Three stacked input slabs, each sized to roughly 3,000-plus words, narrow into a single synthesis block sized to 600–800 words (a sharp reduction), which narrows again into a four-section /i1 brief block sized to 700–1,400 words, before fanning out to four small endpoint nodes representing the four Tic TOC intake questions. Stage areas are scaled honestly to the word counts so the compression is visually truthful.](../images/03-domain-research-fig-04.png)
*Figure 3.4 — Compression funnel: 3 outputs to synthesis to /i1 brief*
<!-- → [INFOGRAPHIC: funnel diagram showing the three-LLM outputs (3,000+ words each) compressing into the 600–800 word synthesis, then into the 700–1,400 word four-section /i1 brief — with the four Tic TOC questions annotated alongside the sections they map to] -->

---

The synthesized brief for the running example — *AI for Designers: A Practitioner's Guide* — is reproduced here in its /i1-ready form. The full source brief lives at `pantry/ai-for-designers-final-brief.md` and runs to roughly 9,000 words; that version is longer than the /i1 minimum because it doubles as the source document for every chapter of the book, not just the intake session. What follows is the four-section distillation, with provenance markers preserved.

**Section A — The state of the field.** Generative AI is structurally embedded in graphic design as of 2026. 93% of designers use AI tools at least once a week (Figma State of the Designer 2026) [ALL THREE AGREE; specific number from Gemini]. Adobe Firefly shows 41% business adoption; Figma AI, Canva Magic Studio, Midjourney, and DALL-E are embedded as defaults in the major tools [ALL THREE AGREE on tool list].
<!-- FACT-CHECK FLAG: UNVERIFIED — see factchecks/03-domain-research-assertions.md (Adobe Firefly 41% figure not confirmed; reproduced-brief content) -->
 Adoption is uneven: heaviest in social-media production work, lightest in high-end brand identity, where only 12% trust AI for Fortune 500 branding [ONE ONLY — Gemini, Figma 2026 source]. PwC 2025 reports a 56% wage premium for workers with advanced AI skills (U.S. cut) [TWO AGREE — Claude and Gemini]. WEF 2025 ranks graphic design as the 11th fastest-declining job category, citing AI as primary cause [DIVERGENT — Claude flags the source; GPT does not raise it]; simultaneously 59% of freelance designers report raising rates via AI-enhanced prototyping [ONE ONLY — Gemini]. Both signals are present.

**Section B — The fluency trap and irreducibly human taxonomy.** Five fluency-trap patterns recur across all three outputs: brand-correct surface with brand-wrong meaning [ALL THREE AGREE, primary pattern]; accountability collapse — designer can produce the asset but not defend the decision [ALL THREE AGREE]; client-relationship misread — AI blind to unspoken brief context [ALL THREE AGREE]; revision-cycle breakdown from non-localized generative control [ONE ONLY — Gemini]; variation overload without selection principle [TWO AGREE — Claude and GPT]. The irreducibly human taxonomy: client intuition, subtractive judgment, creative accountability, brief interpretation, constraint navigation, presentation under questioning, cultural reading, brand stewardship [ALL THREE AGREE on category list, varying formulations]. Empirical anchor: arXiv 2024 expert evaluation found GenAI-supported designs rated more creative and unconventional but not significantly better in visual appeal, brand alignment, or usefulness [TWO AGREE — Claude and GPT; Gemini does not raise it].

**Section C — The reader's specific risk context.** The target reader is a freelance graphic or brand designer, five to fifteen years of practice, one primary anchor client, at least one consumer-grade AI tool in active use. Specific risks: confidentiality and NDA exposure from feeding proprietary client data into consumer-grade AI tools [ONE ONLY — Gemini, most complete]; legal exposure void — no in-house legal department to backstop a copyright claim from AI-assisted work [TWO AGREE — Claude and Gemini]; rate compression from clients who assume AI makes everything faster and cheaper [ALL THREE AGREE]; scope creep from clients asking for "a few more variations" [ONE ONLY — GPT framing]. Specific opportunity: retainer expansion via embedded creative partner positioning [ONE ONLY — GPT framing]; rate-raise via AI-enhanced rapid prototyping (59% of freelancers reporting this) [ONE ONLY — Gemini]. The reader holds tacit knowledge — client history, internal politics, brand memory — that is the long-term relationship's primary value and cannot be replicated by AI [ALL THREE AGREE].

**Section D — The market gap and book positioning.** No current training program teaches the full AI+1 framework for graphic designers specifically. Adobe, Figma, and Canva publish product-focused tutorials driving user adoption [ALL THREE AGREE]. AIGA's business and law certificates cover legal and business fundamentals but are slow to adapt to generative AI law changes [ONE ONLY — Gemini, specific institutional claim]. Independent design educators (The Futur, Flux Academy) teach business scaling and visual fundamentals but lack comprehensive AI+legal+strategy curriculum [TWO AGREE — Claude and Gemini]. The book's position: a practitioner handbook for the freelance designer with deep domain expertise and one anchor client, teaching AI fluency as a layer on top of preserved professional identity — with the IP, disclosure, brand stewardship, and accountability moves the existing training market does not cover [SYNTHESIS, derived from gap analysis ALL THREE AGREE].

Notice three things about that brief. Every claim has provenance — either a four-marker flag or a source attribution. Contested claims are stated as contested rather than resolved. And the length is bounded: four sections, roughly 900 words. That is the document a productive /i1 session can work from. It is not the 9,000-word source; it is the input.

---

What this chapter actually established, underneath the method:

The three-LLM domain research prompt is not a redundancy check. It is a map-drawing exercise. When you run the same question across three differently-trained systems, what you get back is not three answers but a topology — the territory where confidence is high, the edges where it frays, and the occasional point where one system retrieved something the others missed. The synthesis move is reading that topology with professional judgment, marking each claim's confidence level honestly, and compressing the result into a brief that holds up under scrutiny.

The fluency trap check at the end is not optional. It is the same move you are teaching your readers to make on their own AI outputs. Practicing it on your own research brief is how you understand it well enough to teach it.

The brief that comes out of this process is roughly 700 to 1,400 words long. That is not much to show for two to three hours of work. But what the brief contains — every claim flagged by confidence level, contested territory named as contested, the gap in the market stated specifically enough that a Tic TOC session can work from it without stalling — is harder to produce than it looks. The compression is the work.

---

## LLM Exercises

### Exercise 1 (Apply) — Adapt the template to your field; run on three LLMs

Take the eight-section prompt from this chapter. Substitute your specific profession for `[graphic designer]`. Do not modify any other word in the prompt. Run it verbatim in Claude (with web research enabled), GPT-4 or later, and Gemini. Save each response as a separate markdown file: `claude-output.md`, `gpt-output.md`, `gemini-output.md`. Do not synthesize yet.

**Time required:** 30–60 minutes including waiting for outputs.

**Deliverable:** Three markdown files, each between 1,500 and 3,500 words.

### Exercise 2 (Analyze) — Produce a 600–800 word synthesis with provenance flags

Read all three outputs from Exercise 1 in one sitting. Produce a synthesis document organized by the eight original sections. For every claim, mark with one of: ALL THREE AGREE / TWO AGREE / DIVERGENT / ONE ONLY. For ONE ONLY claims, attribute the source LLM. For DIVERGENT claims, state all positions without resolving prematurely.

Length: 600–800 words. Run the five-minute fluency trap check before you call it done: every numeric claim, every named study — can you verify it in five minutes? Downgrade what you cannot.

**Deliverable:** One markdown file, 600–800 words, every claim flagged.

### Exercise 3 (Create) — Produce a four-section brief ready for /i1

Distill the synthesis from Exercise 2 into a four-section brief: state of the field; fluency trap and irreducibly human taxonomy; reader's specific risk context; market gap and book positioning. Total length: 700–1,400 words. This is the document you will paste into the Project Knowledge of your Claude Project before running Tic TOC. The full multi-LLM research prompt is reproduced in Appendix B.

**Deliverable:** One markdown file, 700–1,400 words, four sections.

---

## AI Wayback Machine — Paula Scher

> **Prompt to run in Claude or ChatGPT:**
>
> "Read the Wikipedia article on Paula Scher. Identify one project where her research into a domain — a city, a publisher, a museum — shaped the visual identity in a way no quick brief could have produced. Explain how this maps onto the argument that domain research must precede design."

Scher is a Pentagram partner whose fifty-year career is an extended argument for graphic design as cultural research before it is visual production. Her work on the NYC Public Theater identity, the Citi logo, and Microsoft's corporate identity all begin with extended immersion in the client's domain. The Wikipedia article is accessible; the prompt asks you to read it once and write the comparison memo.[^scher]

[^scher]: Pentagram. (n.d.). "Paula Scher — Partner Biography." Pentagram. Cross-reference with Scher, P. (2002). *Make It Bigger*. Princeton Architectural Press.

---

## Bridge — Chapter 4

The brief exists. Four sections, 700 to 1,400 words, every claim flagged. It sits in a markdown file.

You are now ready for the hardest chapter in the book.

Chapter 4 walks you through the full Tic TOC session — /i1 through /g2 — with the brief you just produced as the primary input. The session takes two hours. The chapter is long because the moves are not transferable from reading; they have to be done.

Chapter 4 is also where the central thesis of this book becomes visible as a single image: two TIKTOC.md chapter specs, side by side, one from a rushed session and one from a session where the pushback was honored. The Cowork outputs below them differ in ways that matter.

The difference is the argument.

---

## Prompts

### Figure 3.1 — Three LLM signatures on the same question
Build a three-panel comparison diagram as one standalone HTML file with inline CSS and D3 7.9.0 from the CDN. Data shape: one shared input node feeding three side-by-side panels (Claude, GPT, Gemini), each panel a stack of text-block bars carrying a distinct signature-marker type. Marks: stacked rectangles for each panel's text blocks; hollow ring markers in the Claude panel margin (hedges), plain enumerated bars with no source ticks in the GPT panel (confident lists), solid bars with source-pin glyphs in the Gemini panel (retrieval-grounded); arrows from the input node to each panel. Channels: column = model; marker type = output signature; color encodes model identity. No quantitative axis, no zero baseline. Annotate the three model labels and the shared "same question" node. Do not reproduce the quoted paragraph prose or the adoption percentages. Deliverable: one self-contained HTML file, inline CSS, D3 7.9.0 CDN, responsive via ResizeObserver, accessible SVG with title/desc.

### Figure 3.2 — Eight-section prompt mapped to Tic TOC intake
Build a left-to-right bipartite crosswalk diagram as one standalone HTML file with inline CSS and D3 7.9.0 from the CDN. Data shape: eight source nodes (the prompt sections) on the left, five target nodes (/i2, /i3, /i4, /l1, /m1) on the right, and a set of section-to-target links (a many-to-some mapping; draw only stated links). Marks: small uniform rectangles for both columns, thin connector lines between them. Channels: left/right column = source versus intake target; y position = order within each column; line presence = a stated mapping. No quantitative axis. Annotate the eight section numbers and the five gate codes. If the crosswalk reads cluttered, split into two stacked sub-panels (sections 1–4 and 5–8) sharing the right-hand target column. Deliverable: one self-contained HTML file, inline CSS, D3 7.9.0 CDN, responsive via ResizeObserver, accessible SVG with title/desc.

### Figure 3.3 — The four synthesis markers
Build a three-circle overlap key as one standalone HTML file with inline CSS and D3 7.9.0 from the CDN. Data shape: three source circles drawn as low-fill outlines so overlaps read, plus four called-out marker regions and one forked divergence marker. Marks: three overlapping circles; leader dots pointing to the central triple-overlap (ALL THREE AGREE), a pairwise lens (TWO AGREE), and a single-circle crescent (ONE ONLY); a separate forked-arrow glyph beside the cluster for DIVERGENT. Channels: overlap geometry encodes the four categories; circle color encodes source identity but stays source-agnostic in labeling. No quantitative axis, no zero baseline. Annotate the four marker names; do not reproduce the running-example claims. Deliverable: one self-contained HTML file, inline CSS, D3 7.9.0 CDN, responsive via ResizeObserver, accessible SVG with title/desc.

### Figure 3.4 — Compression funnel: 3 outputs to synthesis to /i1 brief
Build a horizontal proportional funnel as one standalone HTML file with inline CSS and D3 7.9.0 from the CDN. Data shape: four sequential stages sized by word count — three input slabs at roughly 3,000 words each (aggregate ~9,000), a synthesis block at 600–800, a four-section /i1 brief block at 700–1,400, and four endpoint nodes for the Tic TOC intake questions. Marks: area-scaled blocks connected left to right by flow lines, fanning to four endpoints. Channels: block area = word count (honestly proportional); x position = pipeline stage; color encodes stage. Use a linear area scale anchored at zero so the compression is truthful. Annotate each stage's word-count range and the four endpoint questions. Do not include the 9,000-word source brief as a stage. Deliverable: one self-contained HTML file, inline CSS, D3 7.9.0 CDN, responsive via ResizeObserver, accessible SVG with title/desc.

---

## References

The following sources were verified during fact-checking and support confirmed factual claims in this chapter. See `factchecks/03-domain-research-assertions.md` for the full report.

1. Denzin, N. K. (1978). *The Research Act: A Theoretical Introduction to Sociological Methods* (2nd ed.). McGraw-Hill.
2. Surowiecki, J. (2004). *The Wisdom of Crowds.* Doubleday.
3. Anthropic. (2026). "Claude's New Constitution." Anthropic. https://www.anthropic.com/news/claude-new-constitution
4. World Economic Forum. (2025). *Future of Jobs Report 2025.* WEF. https://www.weforum.org/publications/the-future-of-jobs-report-2025/
5. Pentagram. "Paula Scher — Partner." Pentagram. https://www.pentagram.com/about/paula-scher
