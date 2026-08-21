# Chapter 13 — The Adoption Decision

*This chapter does not make the decision for you. It gives you the structure to make it yourself and the language to explain it to a budget committee.*

---

Gerd Gigerenzer spent his career studying how experts actually decide under uncertainty — emergency room physicians, military commanders, investors with incomplete information. His finding, replicated across domains, was that experts do not weigh many options against many criteria. They recognize the situation as a familiar pattern and check whether one well-chosen course of action holds up under scrutiny. The three-question test from Chapter 11 is exactly that kind of recognition aid. Once you have named the pattern — scale, accountability, willingness — the decision tends to fall out. What remains is the artifact: the one-page document that goes to the budget committee, which requires you to write your recognition down in a form someone else can evaluate.

That artifact is this chapter.

---

## The six fields

Everything the book has built — the three questions, the mode-to-need matching, the institutional requirements, the timeline — compresses into one document with six structured fields. The format is hybrid by design: structured enough that a committee can scan it in three minutes, open enough that the reasoning shows through. A pure table implies more deterministic decision-making than the situation warrants. A pure flowchart hides the nuance. Six fields in prose with fixed labels splits the difference.

<!-- → [TABLE: Adoption decision tool — six structured fields with side-by-side AI+1-only vs AI+1+Medhavy comparison] -->

**Field 1 — Deployment under evaluation.**

One sentence. Name the deployment, the enrollment, the section structure, the instructor staffing, and the strategic pressure — accreditation, board pass rates, retention, whatever is driving the question — tightly enough that a committee member who has never heard of the course can understand the stakes.

*Example: "Pharmacology service course, 320 students across four sections, three instructors with varying experience, shared final exam, accreditation review next year flagging inter-section variance in board pass rates."*

**Field 2 — Three-question answers and reasoning.**

Three short paragraphs, one per question. State the answer — yes, no, contingent — and the one or two sentences of reasoning driving it. The reasoning matters more than the answer. A yes you cannot defend is not a yes; a contingent you can specify precisely is almost a yes.

*Example for Q3: "Yes, contingent. The chair has authority and has stated publicly that the underperforming section will be redesigned. The precommitment is not yet in writing. Field becomes unambiguous yes upon written agreement among the three instructors, expected before contract signing."*

**Field 3 — What Medhavy would add that Canvas does not.**

Two to three sentences, no acronyms, no mode names. The committee version of the loop in plain language: what question does the institution gain the ability to answer that it cannot answer now?

*Example: "Canvas tells us which students submitted, when, and at what score. It does not tell us which students learned the material well enough to retrieve it six weeks later without the textbook. Medhavy measures that, per student per concept, and adapts how the material is presented based on what it measures."*

**Field 4 — First-term success criteria.**

Two to three specific, time-bounded, falsifiable outcomes. If these are met by end of the first or second term, the contract renews. "Improved learning" is not a criterion. "Section-to-section board pass-rate gap narrows by 50% by end of term 2" is.

*Example: "Section-to-section pass-rate gap on the shared final narrows by at least 50% by end of term 2. GLP retrieval-strength signals at week 14 predict final exam performance at r > 0.4 in the pilot section. Pilot-section faculty self-report dashboard actionability above 3 on a 5-point scale, with at least one concrete redesign decision made based on dashboard data within term two."*

**Field 5 — Non-renewal triggers.**

Two to three specific outcomes that end the deployment. This is the field most often left vague, and the field that matters most. SaaS edtech tools mostly fail at renewal, not at adoption. The renewal decision is the honest one.

*Example: "No measurable narrowing of inter-section pass-rate gap by end of term 2. Faculty case-review burden exceeds 30% of original-authorship-equivalent time. Underperforming section is identified but the institution does not act on the data within one term of identification — the willingness-to-act condition has lapsed."*

**Field 6 — Honest acknowledgment of uncertainty.**

One paragraph naming what you do not yet know and how you will find out. This field is not optional. A recommendation that pretends to certainty is less defensible than one that names its uncertainties. The committee should see the reader's honesty here, not paper over it.

*Example: "It is not yet clear whether the three-instructor coordination required for term-2 redesign will hold under the chair-leadership transition scheduled for the following year. The contract should include a renewal clause keyed to Field 4 outcomes rather than a multi-year auto-renewal. The pilot scope — one section — is deliberately narrow; full-program adoption is a separate decision next year."*

The six fields assemble into one page when printed. The committee sees the artifact, not the eleven chapters behind it.

---

## What success actually looks like

Success in the first term is not "GLP scores improved." It is the specific outcome the deployment was purchased for.

For the pharmacology service course: success is the inter-section pass-rate gap narrowing. The shared final exam is the measurement instrument the institution already has, calibrated to a standard the institution already accepts. Medhavy's job is not to invent new measurements. It is to produce the diagnostic evidence that lets the chair narrow a gap the existing measurements have already documented but cannot explain.

By week ten of a fifteen-week term, the GLP signals should show two things. First, per-concept patterns that match the chair's intuition where she has one — her two-decade experience tells her receptor pharmacology is the rate-limiting concept, and the retrieval-strength signals at concept-node level confirm it. Second, per-concept patterns that surprise her where she doesn't — her intuition said dosing decisions were the hardest piece; the temporal engagement and uncertainty calibration signals point instead to drug-drug interactions. The dashboard does not contradict her judgment. It adds a second voice to it.

By end of term, the bandit's per-concept policy should show differentiation that the gradebook does not. Maria and Marcus both scored 86% on the unit-two exam. The bandit's policy for Maria has converged on Ask AI plus Quiz Me, with high retrieval strength at delay; Maria has learned. The policy for Marcus has converged on Case Study plus Glimmer with weak temporal engagement on Quiz Me; Marcus is performing but not retaining. The Canvas gradebook said both students were the same. The loop said they were not.

What would justify renewal: Field 4 outcomes met, faculty using the dashboard with greater than fifty percent regularity in the second half of term — meaning the technology is actually integrated into practice, not licensed and forgotten — and at least one instance of action taken on the data within term two. A section redesigned, a concept reordered, a Case Study revised because the signals pointed to it.

What would not justify renewal: Field 4 outcomes missed despite good faith. Faculty usage trending toward zero. The data never having shown anything actionable — which is itself information, telling the institution that Q1 or Q2 was a no in disguise.

---

## What failure looks like

There are three documented failure modes for adaptive measurement platforms in higher education, and they correspond symmetrically to the three questions.

The first is the wrong deployment context. Q1 was a no that got called a yes. The institution adopted Medhavy in a deployment where an attentive instructor was already adapting in real time with better information than any dashboard can produce. The loop runs in parallel to the actual educational process and adds nothing to it. The honest signal this has happened: by end of term one, the instructor cannot name three specific decisions she made based on the dashboard that she would not have made without it. The fix is non-renewal, not iteration.

The second is insufficient curriculum design. Q2 was a yes in intent but a no in investment. The institution adopted Medhavy and treated the concept map as a fifteen-minute upload of the syllabus. The bandit cannot adapt because the map is too coarse — every concept is just "chapter six" — and the system flags students as struggling without being able to say where. Vendors sometimes encourage this pattern by offering auto-generated maps from the syllabus. The output is unusable. The fix is to staff the curriculum design layer properly — three sessions of three hours, plus revisions, plus faculty review — or to accept that the loop will not close and non-renew.

The third is unwillingness to act. Q3 was answered yes but turned out to be no. The institution adopted Medhavy, built a real concept map, authored real Case Studies, populated the dashboard. The dashboard works. It flags the underperforming section. The institution does not redesign it. The chair has retired. The senior faculty member whose section is flagged refuses to engage with the data. The new chair does not want to inherit the political fight. The dashboard becomes a museum piece. This is the most common SaaS edtech failure mode, and it cannot be fixed technologically. If the institution cannot find the fix institutionally, the honest move is non-renewal.

The three failure modes name where adoption goes wrong in exactly the same vocabulary the three questions used to name where adoption could go right. The symmetry is not decorative. It is the framework's test of internal consistency: if you can run a deployment through the three questions honestly, you can predict in advance which failure mode it is most at risk of.

---

## The honest case for no

There are deployment types where the honest recommendation is not "adopt with caution" or "pilot first" but simply: the simpler stack is the right answer, and adding the loop is overhead.

Small classes with engaged faculty. The seminar of twelve. The nursing fundamentals of twenty-eight. The senior elective of forty with a beloved instructor who has taught it for two decades. The instructor's working memory, weekly contact, and embedded relationship with each student are the adaptation mechanism. The loop is already closed by a human being who does it better than any bandit because she has information the bandit cannot access.

Single-instructor seminars where the instructor designs as she teaches. The whole point of the seminar is that the instructor is adapting based on this cohort, this term, in ways that do not generalize. The institutional infrastructure that would make Medhavy useful — concept map, case bank, prerequisite graph — would also make the seminar less of what it is.

Low-heterogeneity cohorts. Programs where students arrive with similar backgrounds, advance together, and graduate as a class. The cohort structure has already solved the differentiation problem. Per-student adaptation is a solution to a problem the program does not have.

Deployments without dedicated curriculum design capacity. The program that has the budget for the license but not the faculty time for the concept map, the case authoring, and the ongoing maintenance. This is the most common silent failure — the institution that can afford Medhavy in the line-item sense but cannot afford it in the faculty-time sense. The faculty time is the binding constraint, not the license fee, and spreading thin capacity across a layer it cannot support produces neither the loop nor a good AI+1 deployment.

I want to be precise about what a no recommendation is. It is not "Medhavy is bad." It is "Medhavy is the right answer to a specific question, and your deployment is not asking that question." Mary Parker Follett, whose work on integrative decision-making remains underread a century after she wrote it, called this the law of the situation: the right course of action is determined by the situation, not by the toolmaker's preference. The reader's situation determines the answer. A no recommendation is sometimes the most professional output a curriculum director can produce, because it requires defending a position the proposal on her desk was written to push back against.

---

## Talking to the budget committee

The budget committee is not optimizing. It is balancing. IT has one set of priorities, faculty have another, accreditation has a third, finance has a fourth. The curriculum director's job in the two-minute pitch is not to win all four. It is to give the committee a structure to evaluate the recommendation she has made.

Three sentences and one question.

**Sentence one — what it does that Canvas does not.** "Canvas tells us who submitted, when, and at what score. It does not tell us which students retain the material well enough to use it without the textbook. Medhavy measures that — per student, per concept — and adapts how each student encounters the material based on what it measures."

**Sentence two — when it is the right answer.** "It earns its cost when three things are true: we need to present content differently to different learners at scale, someone needs to know whether the variation is helping, and the institution is prepared to act on what the measurement reveals. Our pharmacology service course meets all three."

**Sentence three — when it is not.** "For our small classes with engaged faculty, our cohort programs, and the CE modules where completion is what the regulator counts, the existing stack is the right answer. The recommendation is targeted to one course, not the program."

**The one question.** "If the dashboard shows that one of the four pharmacology sections is producing weaker durable learning than the other three — who at this table is going to call the meeting with the three instructors to redesign that section?"

That question is the test of Q3. If the room can name the person, the deployment is ready. If the room looks at each other, the willingness to act is not yet in place, and the answer to the committee is not "approve" — it is "approve once we have an answer to that question."

The three sentences are structured bottom-line-on-top: conclusion first, conditions second, limits third. The committee gets the recommendation before they get the framework. The framework is in the one-page artifact they can read afterward.

---

## Maria's recommendation

What follows is a justified adoption recommendation written in the voice of the book's primary reader — Maria, the curriculum director at a mid-size health sciences program, whose deployment is the pharmacology service course.

---

**Recommendation: Adopt Medhavy for pilot in PHM 401 Pharmacology, Section 2, beginning fall term.**

**Field 1.** Pharmacology service course (PHM 401), 320 students across four sections, three instructors with varying experience, shared final exam, mid-cycle accreditation review next year flagging inter-section variance in board pass rates as a concern.

**Field 2.** Q1 — Yes. Three hundred and twenty students across four sections taught by three instructors who do not coordinate weekly. The heterogeneity in prerequisite preparation and instructional approach is real and exceeds any one instructor's working-memory capacity. Q2 — Yes. The accreditation team needs to know which section and which concepts are driving the variance. The existing final-exam breakdown tells us variance exists; it does not tell us what to redesign. Q3 — Yes, contingent on written precommitment. As department chair I have committed to redesigning whichever section the data identifies. The two senior faculty members have agreed verbally; written agreement is expected before contract signing.

**Field 3.** Canvas tells us who completed the module and at what score. It does not tell us which students retain the material six weeks later without the book. Medhavy measures retention and adapts presentation per student per concept, producing the diagnostic evidence the accreditation team has asked for.

**Field 4.** By end of pilot term: inter-section pass-rate gap on shared final narrows by at least 50% from current baseline. GLP retrieval-strength signals at week 14 predict final-exam performance at correlation greater than 0.4. Pilot-section instructor reports dashboard actionability at 3 or above on a 5-point scale, with at least one concrete redesign decision made based on dashboard data within term 2.

**Field 5.** We do not renew if: no measurable narrowing of inter-section pass-rate gap by end of term 2; faculty case-review burden exceeds 30% of from-scratch authoring time without proportional learning evidence; the underperforming section is identified but no redesign occurs within term 3. Contract is one-year initial, not multi-year auto-renewal.

**Field 6.** I do not yet know whether the three-instructor coordination will survive the chair-leadership transition scheduled for the following academic year. The contract is scoped to one pilot section; full-program adoption is a separate decision contingent on Field 4 outcomes. I do not know whether the GLP signal evidence will be as diagnostic in our cohort as in prior deployments; the first term is partly a test of that question.

*Estimated total institutional time: 80 hours faculty, 30 hours instructional designer, 6 hours IT, 20 hours institutional review. Estimated time from approval to first student in loop: 11–12 weeks.*

---

That is the artifact. One page. The committee can scan it in three minutes. It is defensible. It is honest. And if the committee asks the one question — who calls the meeting with the three instructors if the data points to one of them — the answer is already in Field 2: the chair, in writing.

---

## What would change my mind

If the GLP signal evidence base were to accumulate across many deployments to a point where the seven friction signals produced robust learning gains across a wide range of institutional contexts, the Q1 scale threshold from Chapter 11 would soften. Smaller deployments — forty students, one instructor, modest heterogeneity — could plausibly justify adoption. Q3 would remain a hard requirement regardless. But the Q1 threshold would shift, and the deployment types I listed above as honest no cases would need revisiting.

If institutional procurement processes for AI-enabled tools became standardized enough that the eight-to-sixteen-week parallel review track from Chapter 12 compressed to four weeks, the timeline considerations in Field 4 would change — specifically, the pacing of first-term success criteria and the cold-start period for the GLP score.

Neither has happened. Either could, and if either does, the framework gets revised. The reader who finishes this book should be as willing to revise her own recommendation when the evidence changes as she was to make it in the first place.

---

## Closing

AI+1 is a better textbook. For most deployments, that is enough. For deployments that need to present differently, measure whether it helped, and adapt — Medhavy closes the loop that Canvas leaves open. The decision is yours. This book gave you the framework. The rest is judgment, which is irreducibly human.

---

## LLM Exercises

**Exercise 1 (Create) — Write your adoption recommendation.** One page. Use the six fields. Must answer: which deployment are you evaluating, what are your three-question answers and the reasoning behind each, what does Medhavy add that Canvas cannot, what does success look like in measurable terms by end of the first or second term, what would cause non-renewal, and what do you not yet know. If you cannot complete a field, that is information about the decision — name what is missing rather than papering over it. The recommendation is finished when you would be willing to sign your name to it and hand it to a budget committee.

**Exercise 2 (Create) — Write your two-minute pitch.** Three sentences plus one question. No jargon. No vendor language. Sentence one names what Medhavy does that Canvas does not. Sentence two names when it is the right answer for your institution. Sentence three names when it is not. The question reveals whether the deployment is ready to act on what the measurement reveals. Practice the pitch out loud. If it takes longer than two minutes, it is not yet ready.

**Exercise 3 (Evaluate) — If your answer is no, write the revisit conditions.** Name the specific conditions under which you would revisit the three-question test. What would have to change for the answers to flip? An enrollment threshold? A leadership transition? A new accreditation standard? A change in faculty composition? The revisit conditions are the responsible version of "no." Without them, "no" reads as "never," which is rarely what you actually mean.
