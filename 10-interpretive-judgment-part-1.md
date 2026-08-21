# Chapter 10 — Capacity 4: Interpretive Judgment (Part 1: The Three Legitimacy Types)

Play three notes — say, a C, an E, and a G sounded together. Now play the same three notes at the front of a nursery rhyme, and then at the head of a funeral march. The chord has not changed. Not a single frequency differs. Yet in one setting it is bright and in the other it tolls, and no analysis of the notes themselves will tell you which. The difference is not in the chord. It is supplied — by the context, and by the conductor who decides what the chord is doing here.

An accurate AI output is a chord. It can be note-for-note correct and mean something entirely different depending on the human context it enters. The same accurate analysis can be legitimate in one setting and illegitimate in another, and the difference is not in the output. It is supplied by an interpreter who knows the context. That act of supplying — deciding what an accurate output *means* and whether it should be acted on *here* — is interpretive judgment, the fourth capacity, and this chapter gives you the vocabulary to diagnose what an output is missing before you try to fill it.

The vocabulary comes from organizational theory, and it is more precise than the loose way we usually talk about "trust." The claim this chapter builds toward is sharp and slightly unsettling: AI does not merely fail to earn one kind of legitimacy. With one of the three kinds, it does something worse — it *counterfeits* it.

## Three Kinds of Legitimacy

The framework is Mark Suchman's. In his 1995 paper "Managing Legitimacy," one of the most-cited works in organizational theory, Suchman identifies "three primary forms of legitimacy: **pragmatic, based on audience self-interest; moral, based on normative approval; and cognitive, based on comprehensibility and taken-for-grantedness.**" [High] Hold onto his actual words, because the everyday glosses drift from them, and the drift matters.

Suchman was writing about *organizations* seeking acceptance from *audiences* — why a company, a profession, an institution comes to be regarded as legitimate. We are going to transpose his typology onto a different question: why should *this AI output* be accepted as a basis for action? That transposition is the author's move, not Suchman's — he never wrote about AI. [High] It is a defensible adaptation, and naming it as an adaptation is part of using it honestly. With that flagged, here are the three types, in Suchman's terms and then translated for the supervisor.

**Pragmatic legitimacy** rests on the *self-interest* of the audience — does this serve the interests of the people it is for? In Suchman's world, an organization earns pragmatic legitimacy by giving its constituents something they want. Translated to an AI output: does the output serve the immediate interest of the person using it — is it fast, useful, responsive to the question asked? An accurate, fluent answer to a real question earns pragmatic legitimacy almost automatically, because it plainly serves the asker's interest. [High] This is the legitimacy AI supplies readily.

**Moral legitimacy** rests on *normative approval* — not "does it serve my interest" but "is it the right thing to do" by socially constructed standards. Suchman subdivides it (consequential, procedural, structural, personal), but the core is a judgment about rightness, not usefulness. Translated: is acting on this output the right thing to do, in this specific human context, by the standards the situation answers to? This requires values someone can hold and be accountable for. A model can *describe* moral considerations fluently; it cannot *stand behind* a recommendation as the right thing, because it holds no values and bears no accountability. [Medium — a defensible argument, not an empirical finding] This connects straight to the solve-verify asymmetry: the model optimizes for the common and the likely, never for the *right.*

**Cognitive legitimacy** rests on *comprehensibility and taken-for-grantedness* — something is legitimate because it is understandable and "the way things are done," accepted beyond active evaluation. This is the subtle one, and it is where the counterfeiting happens. Translated naively, you might say an AI output should be trusted because it is transparent and verifiable. But here is the trap: fluent, confident AI output is *taken for granted too easily.* It reads as the way things are done. It slides past evaluation precisely because it is comprehensible and well-formed. So the claim "AI lacks cognitive legitimacy" is the wrong claim. **AI does not lack cognitive legitimacy — it counterfeits it.** [High] It supplies the *appearance* of taken-for-granted trustworthiness — an unearned cognitive-legitimacy surplus — while genuine cognitive legitimacy, being trustworthy because the reasoning is transparent, accountable, and verifiable, is exactly what the human must supply.

![A three-row comparison of pragmatic, moral, and cognitive legitimacy showing what AI supplies and what the human must supply; pragmatic is earned automatically, moral cannot be stood behind, and cognitive is marked in red as a counterfeit the supervisor must refuse.](images/10-interpretive-judgment-part-1-fig-01.png)

*Figure 10.1 — Of Suchman's three legitimacies, AI supplies pragmatic readily, cannot stand behind moral, and counterfeits cognitive — supplying the appearance of trust the supervisor must refuse and replace with the genuine article.*

| Type | Suchman's basis | What AI supplies | What the human must supply |
|---|---|---|---|
| Pragmatic | Audience self-interest | Readily — it is fast and useful | Confirmation it actually serves *this* interest |
| Moral | Normative approval | Description of considerations, not standing | The judgment that this is right *here*, and accountability for it |
| Cognitive | Comprehensibility, taken-for-grantedness | A *counterfeit* — fluency read as trustworthiness | Genuine trust grounded in verifiable, accountable reasoning |

## Why Pragmatic Is the Only One Statistics Can Supply

Statistical pattern matching is very good at producing outputs that serve an audience's immediate interest. Ask a useful question, get a useful-seeming answer fast: pragmatic legitimacy, earned. That is what the system optimizes for and what it is reliable at delivering.

Moral and cognitive legitimacy are different in kind, not degree. Moral legitimacy requires *standing behind* a judgment as right — an act of accountability that presupposes values held by an agent who can be answerable for them. A statistical model holds no values; it has no self to be accountable. It can generate a paragraph about fairness or harm, but generating a description of a value is not the same as holding one, any more than reciting a vow is the same as being married. Cognitive legitimacy, in its genuine form, requires that trust be *grounded* — that someone can account for why the reasoning holds. The model offers fluency in place of grounding, and fluency is not the same as warrant. The model can narrate a rationale, but recall from Chapter 8 that the stated reasoning chain is not guaranteed to be the actual computation — a model's self-narration is not an account anyone can stand behind. [High]

So the division is structural. The model supplies the legitimacy that comes from being useful. It cannot supply the legitimacy that comes from being right, or the legitimacy that comes from being genuinely accountable for the reasoning. Those are the supervisor's to supply, and this is precisely why interpretive judgment is irreducibly human: meaning and legitimacy are *supplied, not extracted.* You do not read the moral legitimacy off the output the way you read a number off a gauge. You add it, from a position the model cannot occupy.

That last phrase carries the weight, so dwell on it. To supply moral legitimacy you must occupy a position: you must be the one who is accountable, who can be asked "why did you act on this?" and who has to answer with something other than "the system recommended it." The model has no such position. It cannot be summoned to a review, cannot be answerable to a board or a patient or a court, cannot have its values examined because it has none to examine. When a recommendation goes wrong, the question "who is responsible" has no coherent answer that points at the model — and a recommendation for which no one is responsible has not earned moral legitimacy at all. The supervisor's signature, in the next chapter, is the act of taking that position. To supply cognitive legitimacy, similarly, you must be able to *account for* the reasoning to a skeptic — to say not "the model produced this" but "this holds because these specific facts were verified in these specific ways." The model can narrate; only a human can account. The difference between narrating and accounting is the difference between a story and a warrant.

This is why the chapter insists that meaning is supplied rather than extracted, and the phrasing is not loose. Extraction is what you do when the meaning is already in the object and you only have to read it out — a temperature off a thermometer, a balance off a ledger. Supply is what you do when the meaning is *not* in the object and must be added from outside it — when the same chord, the same accurate output, could mean different things and a human must decide which it means here. The interpretive move is an act of addition, not retrieval. The output is the raw material; the meaning is your contribution; and because it is yours, you are accountable for it.

## Diagnosing the Gap Without Filling It

This chapter teaches diagnosis. The next chapter teaches the fill. The discipline of separating them matters, because the most common failure is to skip diagnosis and assume that an accurate output is a legitimate one. *Accurate equals legitimate* is the misconception the whole capacity corrects. [High as a teaching claim] An output can be fully accurate — pragmatically legitimate — and still be the wrong thing to act on, because it optimizes a good the situation does not actually want, or because it is being trusted for its fluency rather than for any reason anyone could defend.

Use a three-cell diagnostic on any output you are tempted to act on:

- **Pragmatic:** Is it useful — does it serve the immediate interest? (Usually yes; this is the easy one.)
- **Moral:** Who would I have to be accountable to for acting on this, and would the recommendation survive their standards? Whose interests does it serve, and whose does it quietly decenter?
- **Cognitive:** Am I trusting this because it is *verifiable* — because I or someone can account for the reasoning — or because it is *fluent*? Is the trust earned or counterfeit?

Two more misconceptions the diagnostic disarms. First, *fluent and confident equals trustworthy* — the counterfeit-cognitive-legitimacy trap, the same plausibility trap from Chapters 4 and 5, now named at the level of legitimacy. Second, *cognitive legitimacy means the model explained its reasoning.* It does not. A model's stated rationale can be unfaithful to its actual computation, so a narrated explanation is not an account. Genuine cognitive legitimacy is supplied by a human who can account for the output — not by the model narrating itself. A third worth flagging: *moral legitimacy is the ethics department's job.* In this book it is not a separate field of fairness or compliance; it is the supervisor's job at the point of recommendation, treated narrowly and operationally as one of the three legitimacies a recommendation must carry.

## Worked Example: One Output, Two Contexts

A hospital deploys an AI system that produces treatment-pathway analyses optimized to minimize cost while holding clinical outcomes within an accepted band. For a given condition, it outputs an accurate, well-reasoned recommendation: Pathway B, lower cost, outcomes statistically within range. The analysis is correct. Now read the same accurate output in two contexts.

**Context one: the hospital finance committee.** The committee's charge is stewardship of finite resources across the whole patient population. The output's optimization target — cost, subject to an outcome constraint — *is* the committee's value. Pragmatic legitimacy: present, it answers the question efficiently. Moral legitimacy: present, because the good it optimizes aligns with the good the committee is accountable for. Cognitive legitimacy: present *if* the committee can account for the assumptions — which retrieval was verified, which outcome band was used and why — rather than nodding at the recommendation because it is a confident number. The output can be legitimate here, on all three counts, provided the cognitive legitimacy is the genuine article and not the counterfeit.

**Context two: the bedside, for one patient.** A clinician reads the same accurate output to decide this patient's care. Pragmatic legitimacy: still present — it answers a question the clinician asked. But moral legitimacy *fails*, even though nothing about the output changed. At the bedside the governing value is this patient's welfare and informed choice, not population-level cost. The output optimizes the wrong good for this context. It is the same correct chord, now sounding in the wrong room. And the cognitive danger sharpens: a busy clinician may accept the recommendation *because it is a fluent, confident system output* — counterfeit cognitive legitimacy doing exactly the work it does best, sliding a cost-optimized recommendation past the evaluation it should receive at a bedside.

The output did not change. The legitimacy did. The accurate analysis is pragmatically legitimate in both contexts, morally legitimate in only one, and cognitively legitimate in neither without a human who refuses to mistake fluency for warrant. The conductor is the source of the difference: the notes are the model's, the meaning is supplied.

![The same accurate cost-optimized recommendation read in two contexts: at the finance committee all three legitimacies are present; at the bedside, pragmatic legitimacy holds but moral legitimacy fails in red, though nothing about the output changed.](images/10-interpretive-judgment-part-1-fig-02.png)

*Figure 10.2 — The identical accurate output is morally legitimate at the finance committee and morally illegitimate at the bedside: the notes are unchanged, the meaning is supplied by context.*

> **AI Wayback Machine — Suchman and the typology of legitimacy**
>
> The three-part scheme this chapter runs on comes from **Mark C. Suchman, "Managing Legitimacy: Strategic and Institutional Approaches," *Academy of Management Review* 20(3):571–610 (1995)** — a foundational and uncontested paper in organizational theory, cited several thousand times. [High] Suchman's own one-sentence summary names the three types and their bases: *pragmatic, based on audience self-interest; moral, based on normative approval; and cognitive, based on comprehensibility and taken-for-grantedness.*
>
> Two honesty notes. First, Suchman wrote about organizations and their audiences, not about AI; applying his typology to the question "should this output be acted on" is the author's transposition, defensible but not Suchman's own. [High] Second, his definitions are sharper than the loose glosses — pragmatic is *self-interest*, not "efficiency"; cognitive is *comprehensibility and taken-for-grantedness*, not "transparency." Holding to his actual definitions is what yields the chapter's real payoff: because cognitive legitimacy is about being taken for granted, fluent AI output achieves it *too easily and unearned.* The supervisor's job is not to grant AI cognitive legitimacy it lacks, but to refuse the counterfeit and supply the genuine article.

## Exercises

The Assessment Spine governs each deliverable: name the judgment call that required your values or domain knowledge — one no AI could make for you, because it could not occupy the position from which the call is made.

**Exercise 10.1 — Define the three types in your domain (Understand).** Translate pragmatic, moral, and cognitive legitimacy into the working language of your field, using Suchman's actual bases (self-interest; normative approval; comprehensibility/taken-for-grantedness), not the loose glosses. For each, give a one-sentence test a practitioner in your domain could apply. *Deliverable:* three definitions, each with a domain-specific test. *Assessment Spine:* identify which of the three is hardest to judge in your domain and why — the judgment that requires situated knowledge. *(Supervision Lab Exercise #8, 25 points.)*

**Exercise 10.2 — Mark the present and missing legitimacies (Analyze).** For a provided AI output, mark which legitimacy types are present and which are missing, with evidence for each verdict. Pay particular attention to whether any apparent cognitive legitimacy is genuine or counterfeit. *Deliverable:* a three-cell diagnostic with evidence. *Assessment Spine:* state the single legitimacy verdict that depended on knowing the context the output enters — the one a reader without that knowledge would have gotten wrong.

**Exercise 10.3 — Specify what filling the gap would require (Evaluate).** For an output in your own domain that is accurate but not yet legitimate to act on, specify concretely what *supplying* the missing moral and cognitive legitimacy would require of you — not that it is missing, but what work fills it. *Deliverable:* a specification of the fill, per missing type. *Assessment Spine:* name what you would have to be accountable for, and to whom, to supply the moral legitimacy — the standing the model cannot hold.

## Closing and Bridge

You can now diagnose the gap. Given an accurate output, you can say which legitimacies it carries, which it lacks, and — crucially — where it counterfeits one. You can tell the chord from its meaning, and you can name what the meaning would have to include to be legitimate here.

Diagnosis is not yet supply. Knowing that an output lacks moral legitimacy does not produce the recommendation you would sign; knowing its cognitive legitimacy is counterfeit does not produce the genuine account. Chapter 11 asks you to *fill* the gap in writing — to take the AI's analysis, call it Memo A, and rewrite it as Memo B: the same analysis with the AI's contribution and your own named separately, the moral and cognitive legitimacy supplied explicitly, and a recommendation you put your name to. Diagnosis becomes authorship, and authorship is where accountability finally lands.

## Sources

- Suchman, M. C. "Managing Legitimacy: Strategic and Institutional Approaches." *Academy of Management Review* 20(3):571–610 (July 1995). DOI 10.5465/amr.1995.9508080331. [The pragmatic/moral/cognitive typology; definitions quoted from the source.]
- Deephouse, D. L., et al. "Organizational Legitimacy: Six Key Questions." In *The SAGE Handbook of Organizational Institutionalism* (2017). [Treats Suchman's typology as foundational; corroborating.]
- The application of Suchman's typology to AI-output trust, and the "counterfeit cognitive legitimacy" framing, are the author's contributions — no external source. [Flagged as the book's framing.]

## Tags

#conducting #ai #interpretive-judgment #legitimacy #Suchman #pragmatic #moral #cognitive #counterfeit #judgment
