# Chapter 14 — Case Studies

*A quiz asks what you know. A case asks what you would do.*

---

It is Thursday afternoon. Your client — a mid-sized marketing agency — has just emailed. They love the rebrand. The colors are right, the wordmark is clean, the system scales beautifully across digital and print. Then, one line near the bottom of the message: *"By the way, did you use AI to generate any of this?"*

You did. You used Midjourney to rough out six directions before picking three to refine by hand. You used Claude to draft the brand rationale document you then rewrote. Maybe forty percent of the final deck touched an AI tool at some point. The manual work is real — hours of iteration, judgment calls, client knowledge — but the AI was part of the process.

You have not answered the email. You are looking at the screen.

This is not a worked example. There is no solution to show you. The question is unresolved, the information is incomplete, and the answer depends on things you know that this book does not: your contract language, your relationship with this client, your jurisdiction's emerging norms around creative disclosure, what "generated" even means to this particular person. You are being asked to make a judgment call in the middle of professional ambiguity.

That email, turned into structured learning material with a debrief, is a teaching case.

---

## What a teaching case is not

Before the definition, the contrast matters, because the confusion between cases and worked examples is exactly where most AI-generated learning material goes wrong.

A **worked example** shows the solution. You see the problem stated, then you see the steps taken, then you see the answer arrived at. The reader's job is to follow the reasoning, abstract the pattern, and recognize similar problems when they appear. Worked examples are excellent for skill transfer in well-defined domains. Sweller's cognitive load theory explains why: the worked example reduces extraneous cognitive load so the learner can attend to the pattern rather than the problem-solving effort itself.[^sweller] You use worked examples when there is a right answer and the right answer generalizes.

A **teaching case** does something different. It places the reader inside an unresolved decision with real tension and incomplete information. The reader is not shown the answer. The reader is asked to form a judgment, defend it, and then — in the debrief — compare that judgment against a structured analysis of what was at stake. The case does not conclude with *the correct choice*. It concludes with *here is what this situation was actually asking of you, and here are the considerations a thoughtful person would weigh*.

The difference is not a stylistic one. It is a difference in what kind of learning the material produces.

Worked examples build pattern recognition: *I have seen this shape before. I know how to resolve it.* Cases build judgment under ambiguity: *I have not seen this exact situation. I need to reason about it, tolerate incomplete information, and decide anyway.* Cognitive scientists call this **transfer** — the ability to apply knowledge in novel contexts — and the research is consistent that transfer requires the learner to have practiced judgment, not just pattern matching.[^perkins]

The research goes further. Gentner and colleagues' work on analogical reasoning shows that transfer is enhanced when learners are forced to find structure in new problems rather than having structure handed to them.[^gentner] Mary Gentner and Kenneth Kotovsky's work on transfer and problem isomorphs is the foundational argument: what transfers is not content, but reasoning structure built through active problem engagement. A worked example hands the student the structure. A case makes them find it.

Harvard Business School's case pedagogy — which has trained case method for over a century — rests on this insight. The goal is not to teach the "right answer" to past business decisions; the goal is to build the habit of decision-making under uncertainty in a setting where the cost of the wrong answer is a grade, not a company.[^hbs] The case is a low-stakes rehearsal of high-stakes judgment.

This is why Part 2 of the AI+1 pipeline builds cases, not more worked examples. Chapter 10 already gave you the quiz infrastructure. Quizzes test recall and basic application. Cases test judgment. For a reader who is a working professional, judgment is what actually transfers to the desk on Monday morning.

[^sweller]: Sweller, J. (1988). Cognitive load during problem solving: Effects on learning. *Cognitive Science*, 12(2), 257–285.
[^perkins]: Perkins, D. N., & Salomon, G. (1992). Transfer of learning. In T. N. Postlethwaite & T. Husén (Eds.), *International Encyclopedia of Education* (2nd ed., pp. 6452–6457). Pergamon Press.
[^gentner]: Gentner, D., Loewenstein, J., & Thompson, L. (2003). Learning and transfer: A general role for analogical encoding. *Journal of Educational Psychology*, 95(2), 393–408.
[^hbs]: Christensen, C. R., Garvin, D. A., & Sweet, A. (Eds.). (1991). *Education for Judgment: The Artistry of Discussion Leadership*. Harvard Business School Press.

---

## The anatomy of a teaching case

A well-formed teaching case has five components. Name them now because the generator prompt in Appendix 91 is built around them, and recognizing the structure is how you vet the output.

**Situation and context.** The reader is placed inside a specific setting with enough concrete detail to feel real. Not "a designer faces an ethical question," but "a freelance graphic designer, eighteen months into a relationship with a marketing agency client, receives an email the Friday before a project deliver." The specificity is not decoration. It is what makes the case generalizable: the reader can only extract the transferable principle if they first understand the specifics from which it is being extracted. Vague cases produce vague learning.

**The tension or dilemma.** Something is genuinely in conflict. Two legitimate goods are competing, or a professional obligation conflicts with a practical necessity, or the right action in one frame looks wrong in another. The tension has to be real — if a thoughtful person reading the case would have no difficulty choosing, the case is not teaching judgment, it is testing compliance with an obvious rule. Disclosure cases work because disclosure norms in design are genuinely unsettled in an AI era. The designer has a real relationship to protect and a real uncertainty about how disclosure would be received.

**The decision point or points.** The case identifies the moment the reader is being asked to step into. Sometimes this is a single binary: answer now or buy time? Sometimes it is a branching sequence: first, do you disclose proactively or wait to be asked? If asked, how do you characterize the AI's role? If the client pushes back, where does your bottom line sit? The decision point is where the case hands control to the reader.

**The information the student has — and what they lack.** A real case tells you what you know and what you do not. You know the email. You know your relationship with this client. You do not know what triggered the question — did they read something, did a colleague raise it, did they see a news story? You do not know their position on AI use. You do not know your contract language precisely. The information the student lacks is load-bearing: it forces the student to make an explicit decision about how to reason under uncertainty rather than resolve the ambiguity before the judgment begins.

**The debrief.** The case without a debrief is a question with no answer. The debrief is not the solution — it is the structured unpacking of what was at stake. It names the competing considerations, the range of defensible positions, the considerations that change which position is more defensible, and the principle that generalizes beyond this specific situation. The debrief might conclude: "Designers who disclosed proactively generally reported better long-term client relationships even when the immediate response was mixed. The risk of non-disclosure is compounded in proportion to the depth of the AI's role." That is a generalizable claim with an empirical grounding. It does not tell you what to do. It tells you what you were actually deciding.

These five components are what separate a teaching case from a discussion prompt. A discussion prompt can generate interesting conversation. A teaching case generates judgment that transfers.

---

## How the AI+1 pipeline generates cases

The generator is a prompt you run inside Cowork or any long-context LLM session. You feed it domain material — pantry files, chapter drafts, a list of professional tensions you want the book to address — and it produces a structured case draft built around the five-component anatomy. The full prompt is in Appendix 91. Here is what the prompt does and why each piece exists.

**The domain brief.** The generator needs to know the field, the reader's career stage, and the professional tensions that are authentic to that domain. For *ai-for-designers*, the domain brief is the `TIKTOC.md` voice section plus the chapter spec for the nearest topically relevant chapter. The generator reads this to understand what "real tension" means in your domain — what a designer would actually face that an accountant would not.

**The situation seed.** You give the generator a single sentence or scenario — a real tension you have observed or a professional dilemma from the domain literature. For *ai-for-designers*, you might seed it with: "A freelance designer who used AI tools extensively on a project receives a client question about AI use." The seed does not specify the answer. It identifies the decision space.

**Component scaffolding.** The generator is instructed to produce all five components, in order, as distinct labeled sections. This is the structural discipline that makes vetting efficient. If the debrief is missing, it is missing visibly. If the information-gap section does not name what the student lacks, that section is clearly incomplete. The structure makes the human audit fast.

**The generalize instruction.** The generator is instructed to end the debrief with a one-sentence principle that survives transplanting: a claim that would be true for any professional in this domain facing this type of tension. This is the test of whether the case is doing its pedagogical job. If the principle only works for this exact scenario, the case has not extracted the transferable learning.

The key constraint: the generator produces a draft. You read it, verify the domain facts, check that the tension is real and not manufactured, confirm the debrief names real competing goods rather than a strawman alternative, and — crucially — check that the five components are all present and honest. This is the human vetting step. It takes fifteen to thirty minutes for a well-generated case and longer when the generator has invented specificity the domain does not support.

---

## The trade-off: cases cost more than quizzes

Before the worked example, one named trade-off.

Quizzes and recall cards are cheap to generate and easy to verify. A quiz question about a design principle — "What does kerning affect?" — either has a correct answer or it does not. You run the generator, you read the output, you spot obvious errors, you accept or reject. Total human time: three to five minutes per question.

A case requires something different. You are checking not just factual accuracy but *situational authenticity*: does this situation actually represent a real professional tension in this field, or did the generator manufacture plausible-sounding friction? A generated case can be grammatically and factually correct while describing a tension that no practicing designer would actually face, or describing a resolution that misrepresents how real professionals in this domain navigate it. That kind of error passes a fact-check and fails a domain-knowledge check.

The second cost: cases can mislead if the domain facts are wrong. A worked example with an error is unfortunate but usually recoverable — the reader sees the steps and can spot the wrong turn. A case with wrong domain facts embeds the error inside the framing. If the case assumes that design contracts routinely include AI-disclosure clauses as of 2026, when they do not, the reader's reasoning about the case is calibrated against a false premise. The debrief then generalizes a false premise into a transferable principle. This is the highest-risk failure mode for AI-generated cases.

The consequence for the author: allocate time for case vetting that you do not allocate for quiz vetting. The rule of thumb in this pipeline is five questions of design time to verify one case. If you have generated twelve cases and blocked an afternoon, you are in the right order of magnitude.

The consequence for the reader: cases drive more transfer than quizzes when they are good, and drive confusion or miscalibration when they are wrong. The investment is worth making. The investment requires being made.

---

## Worked example: a case for *ai-for-designers*

What follows is a condensed version of the case generated by the Appendix 91 prompt, seeded with the disclosure scenario from this chapter's opening. The generator produced a full draft; this is the author-reviewed version.

---

**Case 14.1 — The Disclosure Email**

*Context:* You are a freelance graphic designer, eighteen months into a working relationship with Meridian, a mid-sized marketing agency. You have just completed a rebrand for one of their clients — a specialty food manufacturer — and the project was well-received. Earlier today, your primary contact at Meridian, the creative director you have worked with most directly, sent an email that included the following:

*"Quick question before we close out the project — did you use AI to generate any of the visual elements or copy in the deliverables? One of our clients has started asking, and we want to get ahead of it."*

You used AI tools as follows: Midjourney to generate six rough direction explorations that you used as references when developing the final directions by hand; Claude to produce a first draft of the brand rationale document, which you rewrote substantially; Adobe Firefly to generate one texture that you modified heavily and used as a small background element on one slide of the final deck. You estimate the AI-touched work at roughly forty to fifty percent of the project time in some form, though the final deliverables bear your judgment throughout.

Your contract with Meridian specifies ownership and revision terms. It does not mention AI use or disclosure in either direction.

*The tension:* Meridian has a real business interest in knowing — they are fielding client questions and want accurate information. You have a real interest in your relationship with Meridian and an uncertainty about how they will receive the answer. You also have a genuinely unsettled question about what "AI-generated" means here: is a Midjourney rough you discarded in round one the same thing as a final deliverable you handed to the client?

*The decision point:* You are composing a reply. What do you say, and how do you characterize the role AI played?

*What you know:* The email. Your process. The approximate role of each tool. Your eighteen months of relationship with this creative director.

*What you do not know:* What triggered the question — whether this is a policy question, a specific client concern, or something else. What Meridian's own AI policy is (if they have one). How the creative director personally views AI use. Whether "AI-generated" in Meridian's usage means anything AI-touched or only outputs directly taken from a model.

*Debrief:* Three considerations shape thoughtful answers to this case. First, the framing of the question matters: Meridian asked about AI-generated elements, and the designer's honest answer is that the final deliverables are not AI-generated in the sense of AI-produced — they are AI-assisted in specific ways, with the AI's contribution transformed substantially. Distinguishing the process use from the deliverable content is not evasion; it is accuracy. Second, the missing information is actionable: the single most important unknown is what Meridian means by "AI-generated," and the designer can ask directly as part of the reply without damaging the relationship. Third, the relationship is eighteen months old, which means the creative director has worked with the designer's judgment over time. Disclosing the actual process — specific tools, specific roles, specific amount of transformation — is more likely to build trust than a vague answer, because it demonstrates that the AI use was embedded in a professional process rather than substituted for one.

The transferable principle: *When a client asks about AI use, the most professionally sound answer describes the actual process at sufficient specificity for the client to make an informed assessment — not a binary yes/no, but an account of what AI did and what the human judgment layer contributed.*

---

That case was generated in one session with the Appendix 91 prompt and the *ai-for-designers* pantry as context. The human vetting took about twenty minutes, focused on two checks: whether the tension is real (yes — disclosure norms in design contracts as of 2026 are genuinely unsettled) and whether the debrief's transferable principle is accurate rather than fabricated (the "describe the process at specificity" guidance is grounded in professional ethics literature on disclosure and in the emerging design community discourse around AI use, though no single canonical standard exists). [verify — disclosure norms in design contracts as of publication; check against AIGA and Graphic Artists Guild current guidance]

The case required no fact-check against technical standards. It required a domain-judgment check: would a working designer recognize the situation? That check cannot be automated.

---

## Where cases live in the pipeline

Cases are authored during the enrichment pass — Chapter 10's territory — and stored as structured files alongside the chapter they belong to. Each case is one `.md` file with the five components as labeled sections. The Appendix 91 generator produces files in this format.

In the final book, cases appear either at the end of chapters (after the worked example, before the exercises) or collected in a dedicated section if the book's structure calls for a case bank. In the Canvas `.imscc` export (Chapter 17), cases become discussion activities or ungraded assessments. In the Anki deck (Chapter 16), the situation section is the card front; the debrief principle is the card back.

One case per chapter is the default in the *ai-for-designers* pipeline. Some chapters generate two. The chapters that generate none are usually chapters where the content is procedural rather than judgment-requiring — the generator runs, but the situations it produces feel like worked examples with ambiguity forced onto them. That is a signal: some chapters genuinely need examples, not cases, and the enrichment pass should recognize the difference.

---

## AI Wayback Machine — Christopher Langdell

Christopher Columbus Langdell, dean of Harvard Law School from 1870 to 1895, invented modern case-based legal education. Before Langdell, law was taught by lecture and treatise: the professor recited principles; the students memorized them; the exam asked them back. Langdell replaced the treatise with the casebook — a collection of real legal decisions, stripped of pedagogical apparatus, that students were asked to read and analyze before class. The Socratic method followed: the professor asked not "what does the rule say?" but "what would you have decided, and why?"

The principle Langdell articulated: law is not a set of rules to be memorized but a science to be practiced — and practice requires working with real cases, not principles abstracted away from the situations that produced them.[^langdell]

The AI+1 case generator is doing something Langdell understood a hundred and fifty years ago: putting the reader inside a situation and making them reason rather than recall.

> **Prompt to run in Claude or ChatGPT:**
>
> "Look up Christopher Langdell and the case method he introduced at Harvard Law School. Explain his argument for why cases teach better than lectures on principles. Then identify two modern criticisms of the case method — for example, that cases privilege a certain kind of adversarial reasoning, or that they can teach students to argue any position rather than to find the right one. Finally: how does an AI-generated case for a textbook differ from Langdell's original cases — which were real legal decisions — in ways that matter for pedagogy?"

[^langdell]: Langdell, C. C. (1871). *A Selection of Cases on the Law of Contracts*. Little, Brown (preface, pp. vii–viii). Archived at Harvard Law School Langdell Hall Library.

---

## Exercises

**Exercise 14.1 (Apply).** Open the Appendix 91 prompt. Identify a professional tension from your domain — a real situation in which a practitioner would face competing legitimate goods with incomplete information. Write the situation seed in one sentence. Run the generator with your domain material as context. Confirm the output contains all five components. Save the generated case.

**Deliverable:** The one-sentence situation seed plus the five-component case draft.

**Exercise 14.2 (Analyze).** Read the case you generated in Exercise 14.1 against the five-component anatomy. For each component, write two sentences: what the generator produced, and whether it is situationally authentic to your domain (would a practitioner in your field recognize the tension as real?). Mark any component where the generator invented specificity that your domain does not support.

**Deliverable:** A five-item annotated review — one entry per component, two sentences each.

**Exercise 14.3 (Analyze).** Run the three-question audit from Chapter 10 against your case's debrief: Does it require domain knowledge to evaluate? Does it require judgment, not just pattern-matching? Does the transferable principle break if you swap your domain for a different one? Write one sentence per question with your verdict and evidence.

**Deliverable:** Three-question audit applied to Case 14.1.

**Exercise 14.4 (Evaluate).** Take the Disclosure Email case (Case 14.1) in this chapter and rewrite the debrief to reflect your own domain. Replace the design-specific framing with the professional context of your field — what would the equivalent disclosure decision look like for a practitioner in your domain? What competing goods would a thoughtful person in your field name? What transferable principle replaces the one in the chapter's debrief?

**Deliverable:** A domain-adapted debrief (150–250 words), with the original side by side.

---

## Bridge — Chapter 15

You now have cases: structured judgment scenarios with real tension, explicit information gaps, and debriefs that generalize. Cases are generated by a practitioner-facing prompt, human-vetted against domain authenticity, and stored as structured files.

The next enrichment artifact does something different. It is not a scenario with a resolution. It is an exchange — a prompt that puts the *student* in the position of defending their thinking to an AI, and uses the AI's push-back to surface the reasoning the student did not know they had. It is called a glimmer. It requires no case bank, no situation archive, and no debrief. What it requires is harder: the student has to commit to a position before they know what the AI will say.

That commitment is what Chapter 15 is about.

---

## References

1. Sweller, J. (1988). Cognitive load during problem solving: Effects on learning. *Cognitive Science*, 12(2), 257–285.
2. Perkins, D. N., & Salomon, G. (1992). Transfer of learning. In T. N. Postlethwaite & T. Husén (Eds.), *International Encyclopedia of Education* (2nd ed., pp. 6452–6457). Pergamon Press.
3. Gentner, D., Loewenstein, J., & Thompson, L. (2003). Learning and transfer: A general role for analogical encoding. *Journal of Educational Psychology*, 95(2), 393–408.
4. Christensen, C. R., Garvin, D. A., & Sweet, A. (Eds.). (1991). *Education for Judgment: The Artistry of Discussion Leadership*. Harvard Business School Press.
5. Langdell, C. C. (1871). *A Selection of Cases on the Law of Contracts*. Little, Brown.
