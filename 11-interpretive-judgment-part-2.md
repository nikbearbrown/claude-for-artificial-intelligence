# Chapter 11 — Capacity 4: Interpretive Judgment (Part 2: Memo B)

A man rapidly contracts his right eyelid. That is the whole of what happened, described as a camera would describe it. Now: was it an involuntary twitch? A conspiratorial wink to a friend? A parody of someone else's wink, performed to mock him? Or a rehearsal of that parody, practiced alone in front of a mirror? The eyelid contraction is physically identical in all four. The meaning is not in the eyelid. It is supplied by an interpreter who knows the code — who knows that here, in this room, between these people, a contracting eyelid means *I am in on the secret* and not *something is in my eye.*

This is the example the philosopher Gilbert Ryle used to draw the distinction between *thin* description — "rapidly contracting his right eyelid" — and *thick* description, which fixes which of the four things is actually going on. Clifford Geertz borrowed the example and the terms and made them the method of interpretive ethnography. The previous chapter taught you to diagnose what an accurate AI output is missing. This chapter teaches you to supply it, and the structure of the task is exactly Ryle's and Geertz's: an AI output is a thin description — an accurate record of what is the case, the eyelid contracting, the numbers saying X. The professional's job is the thick description: what the accurate output *means* in this specific human context, whose interests it serves, what values it honors or violates, and whether it should be acted on.

We will call the AI's analysis Memo A and the professional's interpretation Memo B. The transformation from one to the other is where the moral and cognitive legitimacy diagnosed in Chapter 10 actually gets supplied, and where the recommendation acquires a signature. The discipline that makes it work — the chapter's signature move, and the author's own method — is *separation*: naming what the AI produced and what you add as distinct, labeled contributions, so that the line between the machine's work and your judgment cannot blur.

## The Memo A → Memo B Transformation

Memo A is the AI's output, whole and unedited: the differential diagnosis, the valuation, the market analysis, the risk score. It is thin in Ryle's sense — accurate, perhaps, but a record of what is the case, not an account of what it means here.

Memo B is not Memo A with your name added. That is the first and most seductive failure, and it is worth stating plainly: *Memo B equals Memo A plus a signature* is theater, not judgment. [High as a teaching claim] A signature without a genuine legitimacy account is a forgery of accountability. Memo B is the same underlying analysis rewritten so that three things are visible and separate: what the AI produced, what you add, and the recommendation you will sign. The separation is the discipline, and it is not arbitrary formatting. It is what makes accountability possible, because accountability requires knowing whose judgment is whose.

![Diagram showing Memo A as a single thin block transformed by separation into Memo B, a stack of five labeled bands — what the AI produced, what I add, the cognitive account, the moral account, and a red-outlined signed recommendation.](images/11-interpretive-judgment-part-2-fig-01.png)

*Figure 11.1 — Separation turns the AI's thin output into a thick, signed recommendation, with each contribution labeled so accountability can land on the signature.*

A useful way to enforce the discipline is to write Memo B in explicitly labeled sections:

- **What the AI produced.** A faithful statement of Memo A's contribution — the pattern it matched, the data it extracted, the trend it extrapolated. This is the pragmatic legitimacy, named honestly: the AI was useful, and here is exactly how.
- **What I add.** The situated judgment the AI could not make — what it omitted, what it could not weigh, what about *this* context changes the reading.
- **Why this should be trusted (cognitive).** The genuine account: which assumptions were checked, which retrieval was verified, which numbers were recomputed deterministically. Not "the model was confident." The reasons someone could stand on.
- **Why this is the right action here (moral).** Whose interests the recommendation serves, whose it decenters, and the statement that this is the right thing to do in this context — by standards you can name and answer for.
- **Recommendation (signed).** The action you will put your name to.

The labels are not decoration. They make the auditor's job possible in Chapter 15, and they make your own self-audit possible now. When the contributions are separated, a reader can see whether the "judgment" sections actually add anything or merely restate the machine.

## Naming the AI Contribution Is Not Self-Diminishment

A reflexive objection arises here: naming what the AI did diminishes my work — it makes me look like a clerk who pressed a button. The reflex is exactly backward. *Naming the AI's contribution diminishes my contribution* is a misconception. [High] Conflating the two contributions is what makes accountability impossible; *isolating* the AI's contribution is what makes your judgment defensible. If you cannot say where the machine's work ends and yours begins, you cannot defend yours — and you cannot, in the end, sign it honestly, because you do not know what you are signing for.

Separation protects you. When the AI's contribution is named — *the model ran the comparables and extrapolated the trend* — your contribution becomes legible as something else entirely: *and I determined that the trend omits a regulatory change the client must be told about, which is why I do not recommend acting on the projection as stated.* The first is pattern-matching the model did well. The second is situated judgment the model could not perform, because it did not know what this client needs to hear or what you are accountable to disclose. Isolated, your judgment is visible, defensible, and yours. Conflated, it disappears into a fluent memo that no one can be held to.

## The Counterfeit That Looks Like Judgment

Now the hardest part, and the failure the chapter most needs you to recognize in your own writing. The most common way Memo B goes wrong is not that the writer forgets to add judgment. It is that they add *fake* judgment — they restate the AI's own pragmatic case in more impressive language and present the restatement as their interpretation. The TIKTOC names it precisely: *a restatement of the AI's pragmatic case dressed up as judgment.*

This is the laundering failure from Chapter 9, reappearing as fake interpretation. There, an unverified number acquired false authority by passing through clean downstream steps. Here, an unverified meaning acquires false authority by passing through impressive prose. Both are polish standing in for substance. And it maps exactly onto the most common misreading of Geertz: that *thick description means longer, more detailed description.* It does not. [High] Thick is not a word count. A thousand words restating the AI's output is still thin — it is the eyelid described at great length, with no claim about whether it was a wink. Thick description is the *interpretive* layer that fixes meaning, and it can be a single sentence. *He winked to signal that the alibi was a sham* is thick; three paragraphs cataloguing the precise velocity and duration of the eyelid's movement are thin.

So the test for any sentence in your Memo B is the **thin/thick audit**: *is this restating what the AI produced (thin), or interpreting what it means here (thick)?* Highlight every thin sentence. They are not wrong — Memo B needs a faithful statement of what the AI did — but they belong in the "What the AI produced" section and they are not your contribution. The thick sentences are. If the "What I add" and "Why this is right here" sections are full of thin sentences in fancy clothes, you have laundered, not interpreted. Two more tells worth naming: *supplying moral legitimacy means adding an ethics paragraph* — no, it means stating whose interests the recommendation serves and standing behind it as right *here*, which is a claim, not a paragraph of throat-clearing. And the cognitive account must give reasons someone could verify, not the assertion that the model was confident.

Be honest about the difficulty: the line between interpretation and elaborate restatement is itself a judgment call, and there is no mechanical test that settles it for you. This is not a defect of the method; it is the method. A course about supervisory judgment cannot reduce its central act to a checklist, because if it could, the act would be delegable and the whole premise of the book would collapse. What the thin/thick audit gives you is not an algorithm but a set of concrete tells — a sentence is probably thin if you could write it *without knowing anything the model did not already state*; a sentence is probably thick if writing it required a fact about this context, this client, this patient, this situation that the model neither had nor could have. "The valuation is robust and well-supported" is thin no matter how confident it sounds — it restates the model's pragmatic case. "The valuation omits a regulatory change taking effect next quarter that will compress this sector's multiples" is thick — it required knowing something the model did not. The tell is not the prose; it is whether the sentence could only have come from a situated human.

This is also where Chapter 10's diagnosis becomes Chapter 11's authorship. In the prior chapter you learned to *diagnose* the legitimacy gap — to mark that an output has pragmatic legitimacy but lacks the moral and counterfeits the cognitive. Memo B is where you *fill* what you diagnosed. The "Why this is the right action here" section supplies the moral legitimacy the diagnosis found missing. The "Why this should be trusted" section supplies the genuine cognitive legitimacy in place of the counterfeit the diagnosis flagged. Diagnosis without supply is a complaint; supply without diagnosis is guesswork. The two chapters are one capacity in two motions: see the gap, then author the fill, and sign what the fill supports.

## The Signature

Geertz's interpreter stakes a reading — commits to *this* is what the wink meant, and can be wrong, and owns the error. The professional stakes a recommendation. Signing is the act no model performs. The model produces no sound; the conductor signs the score. The signature is not a flourish at the end of Memo B; it is the mechanism by which accountability finally lands on a human who can be answerable for the action. Everything above the signature line exists to make the signature honest: the separated contributions so you know what you are signing for, the genuine cognitive account so the trust is earned, the moral account so you can stand behind the action as right. Sign only what those sections actually support.

## Worked Example: Memo A Becomes Memo B

A financial analyst receives an AI analysis of a growth-stage company the firm is considering. Memo A, the thin description:

> *The model projects 18% annual revenue growth over three years, based on comparable-company multiples and an extrapolation of the last eight quarters. Recommended valuation range: $210–240M.*

Accurate, useful, pragmatically legitimate. Now Memo B, with the contributions separated and the thin/thick discipline enforced:

**What the AI produced.** The model assembled comparable-company multiples, extrapolated eight quarters of revenue, and produced an 18% growth projection and a $210–240M valuation range. This is competent pattern-matching and arithmetic; the comparables are real and the extrapolation is correctly computed (I recomputed the growth figure in a spreadsheet — it ties out). *[Thin, and labeled thin. Pragmatic legitimacy, named.]*

**What I add.** The eight-quarter window the model extrapolated *begins* the quarter after the company's largest customer signed a two-year contract that expires next year and is not assured of renewal. The model treated that period as a clean trend. It is not a clean trend; it is a contract-inflated bump, and the projection silently assumes renewal the company itself describes as uncertain. *[Thick — this is interpretation the model could not supply, because it did not know what the trend's shape conceals.]*

**Why this should be trusted (cognitive).** The growth arithmetic is verified by independent recomputation; the comparables are verified against the source database; the contract-expiry fact is verified against the company's own filings. The conclusion rests on those verified facts, not on the model's confidence. *[Genuine cognitive legitimacy — reasons, not fluency.]*

**Why this is the right action here (moral).** Our recommendation serves the firm's limited partners, to whom we owe a complete picture, not the deal team's interest in closing. A valuation that omits the renewal risk serves the deal and decenters the people we are accountable to. Disclosing it is the right thing to do here. *[Moral legitimacy — interests named, standing taken.]*

**Recommendation (signed).** I recommend the firm treat the $210–240M range as a *ceiling conditional on contract renewal*, and commission a renewal-risk assessment before proceeding. — *[signed]*

The thin number — 18% growth, $210–240M — has become a thick, accountable recommendation. Notice what happened: the AI's contribution was named and honored, not erased; the analyst's contribution was isolated and made defensible; the legitimacy the model could not supply was supplied; and the signature rests on sections that actually support it. A reader can see exactly where the machine's work ended and the analyst's judgment began — which is the only condition under which the signature means anything.

> **AI Wayback Machine — Thick description, from Ryle to Geertz**
>
> The terms *thin* and *thick description* are **Gilbert Ryle's**, from two 1968 essays — "The Thinking of Thoughts: What Is 'Le Penseur' Doing?" and "Thinking and Reflecting." [High] The wink/twitch/parody/rehearsal example is Ryle's too. **Clifford Geertz** borrowed both for *The Interpretation of Cultures* (1973), in the opening essay "Thick Description: Toward an Interpretive Theory of Culture," and made them the method of interpretive anthropology — *and he credited Ryle by name.* [High] So the honest lineage is: Ryle coined the distinction; Geertz operationalized it as ethnographic method. Presenting "thick description" as Geertz's invention is a citation error a knowledgeable reader will catch.
>
> The engine for this chapter is the same in both thinkers: *the meaning is not in the behavior; it is supplied by an interpreter who knows the context.* Memo B is thick description for an AI output — the author's analogy, and a strong one, but an analogy, not a claim from Geertz. The eyelid is the model's accurate output. Which of the four things it means — and whether to act on it — is the thick description only a situated human can write.

## Exercises

The Assessment Spine governs each deliverable: name the judgment call that required your values or domain knowledge — the one no AI could make, because it could not occupy your position or be accountable for the action.

**Exercise 11.1 — Produce Memo B (Create).** Take an accurate AI output in your capstone domain (Memo A) and write Memo B using the five labeled sections: what the AI produced, what you add, the cognitive account, the moral account, and the signed recommendation. *Deliverable:* a complete Memo B. *Assessment Spine:* in the "What I add" section, name the single piece of situated knowledge that changed the reading — the thing you knew about this context that the model could not, and could not have. *(Supervision Lab Exercise #9, 25 points.)*

**Exercise 11.2 — Audit a Memo B for laundered judgment (Evaluate).** Apply the thin/thick audit to a provided Memo B. Highlight every sentence that restates the AI's output (thin) and every sentence that genuinely interprets meaning or supplies legitimacy (thick). Render a verdict: does the "judgment" content add interpretation, or does it launder the AI's pragmatic case in impressive language? *Deliverable:* the annotated memo and a verdict with the strongest tell cited. *Assessment Spine:* identify the one sentence that was hardest to classify, and explain the judgment you used to call it — the line between interpretation and elaborate restatement is itself a judgment call.

**Exercise 11.3 — Write the Assessment Spine statement (Create).** For your Memo B, produce the Assessment Spine statement for the interpretation: the judgment that required your values, and the specific reason it could not be delegated to the model. *Deliverable:* a short written statement. *Assessment Spine:* this *is* the spine — make it name a judgment, not a task, and make the "why not delegable" reason structural, not incidental.

## Closing and Bridge

Four capacities now exist as separate skills. You can audit a plausible output before verifying it, reframe a problem before engaging a tool, orchestrate tools with every handoff and trust decision explicit, and supply the legitimacy an accurate output lacks — diagnosing the gap and then filling it in a Memo B you would sign. Each is a real competence, practiced and assessable on its own.

But a supervisor does not exercise them one at a time, in tidy sequence. Real work braids them together, and the hardest capacity is not a fifth skill added to the four — it is holding all four at once, and noticing when exercising one forces another to re-engage. The plausibility audit that surfaces an anomaly may reopen the problem formulation; the legitimacy gap you find in interpretation may send you back to re-orchestrate. Chapter 12 takes up executive integration: not sequencing the four, but holding them simultaneously toward a recommendation someone signs — the weave of head, hand, heart, and spirit that no single capacity, and no algorithm, can perform on its own.

## Sources

- Geertz, C. *The Interpretation of Cultures: Selected Essays*, opening essay "Thick Description: Toward an Interpretive Theory of Culture." Basic Books, 1973. [Thick description as ethnographic method; credits Ryle.]
- Ryle, G. "The Thinking of Thoughts: What Is 'Le Penseur' Doing?" and "Thinking and Reflecting" (1968), in *Collected Papers*, Vol. 2. [The thin/thick distinction and the wink/twitch example; the term's origin.]
- Secondary on the lineage: Kaploun, "From Geertz to Ryle"; *HAU* 7(2) (2017), "How to distinguish a wink from a twitch." [Corroborates Geertz's borrowing from Ryle.]
- The Memo A → Memo B method, the separation-of-contributions discipline, and the "Memo B is thick description for an AI output" analogy are the author's contributions — no external source. [Flagged as the book's framing.]

## Tags

#conducting #ai #interpretive-judgment #memo-b #thick-description #Geertz #Ryle #legitimacy #accountability #judgment
