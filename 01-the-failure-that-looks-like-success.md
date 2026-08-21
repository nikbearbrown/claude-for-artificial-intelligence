# Chapter 1 — The Failure That Looks Like Success

*When the numbers say it's working and the exam says it isn't.*

---

There is a particular kind of institutional failure that is almost impossible to catch while it is happening. It does not look like a failure. It looks like success — engagement up, satisfaction high, completion rates in the nineties. The dashboard is green. The vendor is happy. The dean is pleased. And then the exam arrives and the students who used the AI most score lower than the students who did not use it at all.

This is not a thought experiment. In 2025, Bastani and colleagues at Wharton published a randomized trial in *PNAS* that measured almost exactly this pattern. Nearly a thousand Turkish high-school students, 9th through 11th grade, four 90-minute math practice sessions, three conditions. One group got access to an unmodified GPT-4 chatbot — ask it anything, get a complete answer. A second group got access to the same underlying model, but wrapped in a system prompt that committed it to giving hints and asking questions rather than delivering solutions. A third group practiced from the same problem set with no AI at all.

During the sessions, both AI groups outperformed the no-AI control. They worked through more problems. They reported higher satisfaction. If you had looked only at the in-session metrics — the kind any learning management system dashboard would surface — you would have concluded that the AI was working, and working well.

Then the unassisted final exam. No chatbot, no notes, same content.

The students who used the unguarded GPT scored roughly seventeen percentage points below the no-AI control group. [verify final corrected figure, 10.1073/pnas.2518204122] The students who used the hint-only wrapper matched the control group — neither helped nor harmed compared to practicing without AI.

Same model. Same students. Same content. Same four sessions. Two wrappers. Opposite outcomes on the only measurement that mattered.

---

Before asking what this means for your institution, it is worth being precise about what it actually shows, because the tempting interpretation is wrong. The tempting interpretation is that AI is bad for learning. The data do not say that. The guarded condition produced no harm. The data say something more specific: that the same model, deployed without architectural commitments about what it will and will not do, can produce strong apparent performance during practice and substantially weaker learning when the scaffold is removed.

The word "apparent" is doing important work in that sentence.

There is a distinction in cognitive psychology, formalized by Robert and Elizabeth Bjork at UCLA in the early 1990s, that the field calls the performance-learning distinction. *Current performance* is what a student can do right now, with resources present — the textbook open, the tutor in the room, the AI running on the laptop. *Learning* is what the student can do later, unassisted, possibly months from now. The Bjorks demonstrated that these two quantities are not the same, and — here is the part that still surprises people — that they are sometimes inversely related. Interventions that produce the highest current performance sometimes produce the worst learning. Re-reading is the classic example: it feels productive, it boosts in-session confidence, and it produces less durable memory than retrieval practice, which feels harder and slower and worse.

What Bastani's unguarded GPT condition did was push this effect to its maximum. The AI was producing high current performance — students could work more problems, get unstuck faster, report the session as helpful — while bypassing the cognitive work that actually builds a durable schema. The schema requires something to be constructed, not just received. You have to retrieve prior knowledge, generate a hypothesis, encounter a prediction error, repair your understanding. When the AI hands you the answer, you skip all of that. The problem gets solved. The understanding does not.

<!-- → [INFOGRAPHIC: two-path diagram showing in-session performance vs. delayed unassisted assessment — AI high engagement path leads to low exam score; no-AI control path leads to higher exam score; visual should make the inversion visceral, not just described] -->

---

The second mechanism at work in this failure is specific to the technology, and it is worth naming separately because it operates even in students who are paying close attention and genuinely trying to learn.

A well-trained large language model produces text that reads like understanding. Coherent paragraphs, domain terms used correctly, confident hedges where a real expert would hedge. When a student asks the difference between a beta-1 selective blocker and a non-selective one, and an unguarded chatbot returns three hundred fluent words, the surface of that text is indistinguishable, visually and stylistically, from what a hospital pharmacist would write. The student reads it, nods, moves on, and feels like they understood.

What did not happen in that interaction is any cognitive work on the student's side. Emily Bender and colleagues described this from the model side in 2021 — a language model's surface coherence is not a reliable index of understanding on either side of the exchange, the model's or the reader's. The reader infers understanding from fluency. The reader is sometimes right. In Bastani's data, the reader was seventeen points worth of wrong.

The cruel thing about this trap is that it is not specific to bad AI tools. It is specific to *competent* AI tools used without constraints. The better the model is at sounding like an expert, the more powerful the trap, because the apparent value of the interaction rises while the cognitive work going into it falls. The student feels like they learned something. The exam reveals that they did not. And nothing in the session gave either the student or the instructor any reason to expect the gap.

This is what I mean by the failure that looks like success. The failure is not a bug in the vendor's dashboard. The dashboard is honestly reporting what it was designed to report: engagement, completion, in-session performance. These are real measurements of real behaviors. They were never designed to be measurements of learning, and the correlation between them is unreliable enough that you cannot use one as a proxy for the other on a high-stakes adoption decision.

---

Here is the claim the rest of this book is built on, and it is worth stating plainly before going further.

**The AI is not the variable. The wrapper around the AI is the variable.**

Two products built on the same underlying model can produce opposite learning outcomes. Two vendor proposals that both say "powered by GPT-4" are not the same product. The architecture — the specific commitments a platform makes about what the AI will do and refuse to do — is the unit of analysis. The base model is a component.

Bastani's study makes this visible in the cleanest possible experimental form. The intervention that separated harm from no-harm was a system prompt. Not a different model, not a different student population, not different content, not a different number of sessions. A system prompt that said: give hints, ask questions, refuse to produce complete solutions. That wrapper was the entire architectural intervention.

<!-- → [TABLE: Bastani 2025 three-condition summary — columns: condition, AI access, in-session performance, unassisted exam result; rows: GPT Base, GPT Tutor, No-AI Control — the table should make the inversion between columns 3 and 4 immediately readable] -->

This principle is not new. It has a pre-LLM history worth knowing, because the pattern repeats and the lesson was available before the current technology made it urgent. The ASSISTments tutoring platform, developed at WPI by Neil Heffernan and colleagues, produced roughly three-quarters of a year of additional math growth in Maine middle schools compared to a control. Same content as the textbook, different architecture — immediate scaffolded feedback, teacher dashboards showing where students were stuck, explicit refusal to simply give answers. Three-quarters of a year of growth is not a small effect. The wrapper was doing that work.

What has changed is not the principle. What has changed is the stakes. An LLM-powered tool can now produce a fluent, confident, apparently correct answer to almost any question a student in almost any domain might ask. The potential for the fluency trap to operate at scale — across every student, every subject, every session — is qualitatively different from what the pre-LLM tutoring literature was measuring. The architectural commitments matter more now, not less, because the underlying technology is more capable of bypassing cognitive effort without the student noticing.

---

There is an instructive marginal note in the history here. Richard Atkinson at Stanford built a computer-aided instruction system in the late 1960s that delivered individualized math and reading practice to elementary students. The system worked — published results showed real gains. It did not claim to do more than the technology could honestly do. It failed commercially anyway, killed by the economics of mainframe hardware and the politics of school adoption, not by pedagogy. The lesson that rhymes with today is this: the architecture mattered, the wrapper around the computation was what produced the gains, and the institutional decision to adopt or not ran mostly on factors unrelated to whether the system actually worked. The pattern is not new. The Bastani study is its cleanest contemporary measurement.

---

The question this chapter is not asking is whether your institution should use AI at all. The question this chapter is asking is narrower and more useful for a decision-maker with a budget meeting in six weeks.

Given that the same model can produce opposite outcomes depending on what the platform commits it to doing — what specific architectural commitments would you require any AI tool to make before adding it to your course environment?

Bastani gives you a starting list. At minimum: a commitment about what the AI will not do; a measurement that is not in-session performance; and a grounding source that constrains what the AI can wander into.

What you need from this chapter is the categorical shift: that the question "should I adopt this AI tool?" cannot be answered from a feature sheet, because the feature sheet describes capabilities, not commitments. A product that says "AI-powered tutoring" is consistent with both outcomes Bastani observed. The relevant question is not "does this product use AI?" The relevant question is "what does this platform commit the AI to doing and refusing to do, and how would I know if it failed at those commitments?"

That is the question the rest of this book is built to help you ask. The next chapter starts the diagnostic that tells you whether your context even requires these commitments, or whether the simpler path is the right one for what you are actually trying to accomplish.

---

## LLM Exercises

**1. Generate and examine.** Ask an unguarded general-purpose chatbot to walk through a worked problem in a course you know well and give you a complete solution. Does the fluency of the output tell you whether a student who read it would be able to solve a similar problem unassisted? Write two sentences: what the output looks like on the surface, and what cognitive work the student would have had to skip to get it.

**2. Apply to known context.** Take the same problem and prompt the chatbot explicitly to give only hints and questions — refuse to produce a complete solution. Compare the two outputs. Write a paragraph on what architectural commitment you just simulated with a prompt, and what its limits are.

**3. Stress-test the claim.** Try to find a counterexample: a deployment context in which you would predict that an unguarded AI produces durable learning rather than borrowed performance. What conditions would have to hold? What kind of student, what kind of content, what kind of prior knowledge? If you cannot find a genuine counterexample, describe what additional evidence would change your assessment of the claim.

**4. Draft a professional deliverable.** You are preparing a one-page briefing for a curriculum committee considering an AI tutoring tool. Using only Bastani's finding and the performance-learning distinction, write the two questions the committee should ask the vendor before approving any pilot. Each question should be specific enough that a vendor could not answer it with a feature sheet — it should require a description of an architectural commitment and a measurement approach.

---

*Sources cited in this chapter: Bastani, H., Bastani, O., Sungu, A., Ge, H., Kabakcı, Ö., & Mariman, R. (2025). Generative AI without guardrails can harm learning: Evidence from high school mathematics. Proceedings of the National Academy of Sciences, 122(26), e2422633122. Correction at 10.1073/pnas.2518204122. · Bjork, R. A., & Bjork, E. L. (1992). A new theory of disuse and an old theory of stimulus fluctuation. · Bender, E. M., Gebru, T., McMillan-Major, A., & Shmitchell, S. (2021). On the Dangers of Stochastic Parrots. FAccT '21. · Heffernan, N. T., & Heffernan, C. L. (2014). The ASSISTments Ecosystem. International Journal of Artificial Intelligence in Education, 24(4). · Atkinson, R. C. (1968). Computerized instruction and the learning process. American Psychologist, 23(4), 225–239.*
