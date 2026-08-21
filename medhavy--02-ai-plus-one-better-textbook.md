# Chapter 2 — AI+1 Is a Better Textbook. Is That Enough?

*The question sounds modest. The answer determines everything that follows.*

---

There is a category error that gets made constantly in educational technology, and it goes like this: someone builds a better version of an existing thing, demonstrates that it is in fact better, and then the institution concludes that better means sufficient. A better textbook is adopted. Outcomes improve marginally. The improvement is noted, and everyone moves on. What nobody asks is whether a better textbook was actually the binding constraint on learning in the first place — whether the thing that was limiting students was the quality of their reading material, or something else entirely.

This distinction is not pedantic. It is the whole chapter.

AI+1 is a better textbook. I want to be careful about what that claim means, because it does not mean what most people expect when they hear "AI-powered learning." The text was produced with AI — a domain expert and an AI drafting tool working in combination — but the AI does not run at read time. When a student opens the Kindle edition, she is not querying a model. She is reading a book written by a pharmacist or a nurse educator or a physician, a book that happened to be produced faster and cheaper than conventional academic publishing allows, because the expert's judgment was paired with a tool that handles synthesis and drafting at scale. The "+1" in the name refers to the human contributor — the person who cannot be removed without changing what the book actually is. Paul Daugherty and James Wilson called this arrangement the "missing middle" in their 2018 *Human + Machine*: the work that humans do badly alone, machines do badly alone, and the pair does well together. AI+1 is the missing middle applied to publishing.

What AI+1 produces is a book that sounds like one expert practitioner talking to one student, because the production model requires an expert practitioner to anchor it. That is rarer than it sounds. Most textbooks sound like committees. This one sounds like a person — which is, it turns out, pedagogically relevant. Jerome Bruner argued in 1966 that students learn from narrative and voice in ways they do not learn from taxonomic enumeration; what he was describing is the difference between a book that tells you what is known and a book that shows you how a practitioner thinks. AI+1 is designed to be the second kind.

<!-- → [IMAGE: diagram showing the AI+1 production model — expert practitioner + AI drafting tool → frozen text → Kindle delivery → student reads; contrast with a "live AI at read time" diagram; student should see the distinction between AI at write time vs. AI at read time] -->

So: it is a better textbook. The delivery is cheap — a dollar on Kindle, which is not a concession to the market but a philosophical position about what textbook economics should look like. The slides that accompany it in class are Brutalist — text-heavy, no animations, no decorative themes — because the name comes from a 2014 web design manifesto by D.B. Copeland that argued decoration imposes a cognitive-load tax on readers, and the slides are making the same argument about lectures. The whole stack is designed around one idea: the content should be good, the delivery should be cheap, and nothing should get between the student and the material.

For a significant fraction of deployments, that stack — AI+1 on Kindle, Brutalist slides in class, Canvas for grades, an instructor who knows her students — is complete. Not a compromise, not "good enough for now." Complete. The right answer.

The question this chapter is built to answer is: complete for whom?

---

Before I can answer that, I need to explain what AI+1 is not, because the confusion between what it is and what it is not is where most institutional decision-making goes wrong.

AI+1 is not Medhavy. This sounds obvious when stated directly, but the two products come from the same publisher and share a lineage, and institutions frequently assume that adopting AI+1 textbooks means they have adopted something like Medhavy. They have not. Medhavy is a measurement and adaptation layer — software that runs at read time, on top of the AI+1 content, and does things the content cannot do by itself: present material differently to different learners based on what they have demonstrated, measure whether the variation is helping, and adjust. The content and the layer are different products solving different problems. Having the first does not give you the second.

The other confusion is between AI+1 and what might be called an "adaptive textbook" — ALEKS-style platforms where the content itself shifts based on student performance. AI+1 is not that. The AI+1 text is frozen. The student adapts to the book; the book does not adapt to the student. Whether you also want a layer that adapts at read time is a separate question with a separate answer, and conflating the two is the error that produces expensive deployments of software that adds no value over a Kindle and a good instructor.

Beverly Park Woolf made an early version of the relevant distinction in *Building Intelligent Interactive Tutors* in 2009. Woolf has a PhD in computer science and an EdD, which is an unusual combination, and her position was unusually precise: an intelligent tutor adds value beyond a well-designed textbook when the deployment cannot rely on a human teacher to do the adaptation — and the conditions under which that holds are conditions of scale, heterogeneity, and accountability. That was 2009. Sixteen years later, her three conditions are a first draft of the diagnostic this chapter is building toward.

---

Let me describe a standard deployment so the diagnostic has something to work against.

Thirty nursing students. One section. One instructor — a nurse educator, twelve years of clinical experience, four years teaching the course. She has taught this material enough times that she knows which drug classes produce confusion in week six and which dose-calculation errors show up in week nine. By week three, she knows each student's name and something about how they think. She can tell from a Tuesday discussion who did the reading. She adapts in real time: she slows down on receptor binding when the class is lost, accelerates through dose calculation when they are not. She holds office hours. She fields the questions students were too embarrassed to ask out loud.

She is the loop. In the language I will use in Chapter 3 and beyond, the loop is the combination of three things: presenting content differently to different learners, measuring whether the variation is helping, and adapting based on what the measurement reveals. This instructor does all three. She does them manually, with her professional judgment as the algorithm, and she does them at a scale — thirty students — where a human being can actually do this.

Now run the same material through a different deployment. Three hundred nursing students. Five sections. Three instructors of varying experience, ranging from clinical veteran to second-year faculty. Students were placed into sections by registration order, not by entry level. The sections share a syllabus but the instructors teach differently. The program director has no shared visibility into which students in which sections are struggling with which concepts. The board exam is fourteen months out. The dean wants to know why one section had a lower NCLEX pass rate last year, and the honest answer from the program director is: I don't know.

Same AI+1 content. Same Kindle edition. Same Brutalist slides. Completely different deployment.

The instructor in the first case is performing a function that the second case has no equivalent of. The first case has a human loop. The second case has five partial loops of varying quality with no way to compare them and no way to intervene in real time across all of them simultaneously. Adding Medhavy to the first case would be overhead — the instructor is already doing what the software does, and she is doing it with judgment a contextual bandit cannot match at n=30. Adding Medhavy to the second case would be addressing a real structural problem: the measurement the dean is asking for does not exist, the loop is broken across sections, and there is no human who can hold all of it at once.

<!-- → [TABLE: two-column comparison of the 30-student single-section deployment vs. the 300-student five-section deployment — rows: number of students, number of instructors, real-time visibility into individual performance, mechanism for cross-section comparison, feedback loop between learning and instruction, board exam accountability; student should see that the difference is structural, not just quantitative] -->

The question is not which deployment is better. The question is which deployment needs what.

---

The diagnostic has three questions. I am going to give them to you plainly, then spend some time on the third one, because the third one is where most institutions fail.

The first question: *does the deployment need to present content differently to different learners at scale?* Not "present different content" — that is the curriculum question, and AI+1 handles it at the textbook level. The question is whether different learners need different pedagogical approaches to the same material. A student who has never seen the citric acid cycle needs a different entry point than a student who studied it three years ago and is rebuilding the schema. If your deployment is thirty students with one experienced instructor who can see the difference and adjust, the answer is probably no — you have not yet exhausted the human layer. If your deployment is three hundred students across five sections with heterogeneous entry levels and no human who can see the whole picture at once, the answer is probably yes.

The second question: *does someone need to know whether the variation is helping?* If you are not varying delivery, there is nothing to measure. If you are — either through a software layer or through faculty who teach different sections differently — the question is whether your institution needs to know whether the variation is producing learning or just producing variation. The active-learning literature is supportive here: Freeman et al.'s 2014 meta-analysis in PNAS found that active-learning sections reduced failure rates from 34% to 22% across 225 STEM studies. But that finding is about the structure of the intervention, not about whether any particular deployment of active learning is working. Knowing the intervention class works is not the same as knowing whether your specific deployment is working. End-of-pipeline measurement — board exam in eighteen months, licensure pass rate next year — is real data, but it does not let you intervene. If the answer to "when would I find out a section is underperforming" is "next year," Question 2 is a yes.

The third question: *is the institution willing to act on what the measurement reveals?*

This is the one that breaks things. I have seen institutions add measurement layers and produce dashboards showing exactly which sections are underperforming on which concepts, and then do nothing with the information — because acting on it would mean changing a curriculum, or having a direct conversation with a tenured colleague whose section is producing the weakest outcomes, or restructuring a sequence that has been in place for fifteen years. Measurement without willingness to act is expensive Canvas analytics. The data accumulates. Nothing changes. The question is not whether you can produce the information but whether your institution will do something when the information is uncomfortable.

The honest version of Question 3 is this: if Medhavy showed you, in week eight, that one section was producing weaker durable learning than another on the same content, what would happen? If your answer is "I would convene a curriculum committee, identify the cause, and change something," Question 3 is a yes. If your answer is any variant of "I would note it" — Question 3 is a no, and the measurement layer is a budget mistake regardless of how good the technology is.

If any of the three answers is no, stop here. AI+1 on Kindle is the right answer. Not the conservative answer. Not the "we'll upgrade later" answer. The right answer, because the deployment does not have the structural problem the additional layer exists to solve.

If all three answers are yes, the rest of this book describes what the loop looks like and what it would cost.

<!-- → [INFOGRAPHIC: the three-question decision tree — Q1 (present differently at scale?) → if no: AI+1 stack is complete; if yes → Q2 (need to know if variation helps?) → if no: AI+1 stack is complete; if yes → Q3 (willing to act on measurement?) → if no: AI+1 stack is complete; if yes: proceed to Medhavy; student should see that each no is a complete answer, not a partial one] -->

---

The hardest case is the in-between deployment, and it is also the most common. Ninety students across two sections. One experienced instructor and one who is in her second year of teaching. Question 1 is a tentative yes. Question 2 is a tentative yes. Question 3 depends on whether the senior faculty member is willing to have her teaching examined alongside the new instructor's.

Most institutions hesitate at Question 3. That hesitation is itself the most important data point the diagnostic produces. If Question 3 is uncertain, the right move is to resolve it before buying the measurement layer — not to buy the measurement layer and hope. You cannot retrofit institutional willingness to act. Either the culture exists or it needs to be built, and building it is a prior project to deploying software that will produce uncomfortable findings.

J.C.R. Licklider published "Man-Computer Symbiosis" in 1960, before AI was a marketing category and decades before Kindle existed. His argument was that the durable design problem in computing was not whether machines would replace humans but how the interface between the two could be made productive. Each side does something the other cannot; the work of design is to specify the seam between them clearly enough that the combination produces value neither could produce alone. The AI+1 framework is Licklider's symbiosis applied to publishing: the domain expert provides irreducible judgment, the AI provides scale, and the combination produces something neither could produce alone. The three-question test is the question of where to put the seam for a particular deployment — whether the human side of the seam can handle the measurement and adaptation work, or whether that work needs to move further toward the machine.

In most deployments, it stays with the human. That is not a failure of ambition. It is Licklider's answer to a question he identified sixty-five years ago: know which side of the seam a task belongs on, and put it there.

---

There are things this chapter has not settled. The size threshold — where exactly does a single instructor stop being able to run the loop manually? — sits somewhere between 30 and 300, and the middle range, where most program directors actually live, does not have a clean answer. The question of how to test institutional willingness before you have committed to a measurement system also has no clean answer; asking the question in the abstract produces yes answers that do not survive contact with the first inconvenient finding. And there is a question the chapter has not addressed at all: are there deployments where AI+1 is not enough and Medhavy is also not enough — where the missing layer is something neither product provides? Clinical placement, mentorship, the kind of feedback that requires watching someone perform in a high-stakes situation and telling them what they did wrong: these are not in the AI+1 stack and are not in the Medhavy stack. The book is not claiming this stack solves all of educational delivery. It is claiming this stack solves the textbook-and-content-delivery problem well enough to bracket everything else.

The next three chapters explain what the loop does when the answer is yes. Medhavy has four pedagogical modes, and it chooses among them based on what the measurement layer is telling it. Each mode is a different cognitive operation with a different evidence base. The next chapter starts with the one that does not answer questions — the mode most easily mistaken for a chatbot, and the one whose architecture most directly responds to the finding from Chapter 1 about what passive AI assistance costs. Ask AI.

---

## LLM Exercises

1. **(Evaluate, applied to your own deployment)** Describe your primary deployment in three sentences: how many students, how many sections, how many instructors, what scale of program. Then run the three questions. Record your honest answers. If any answer is uncertain, write one sentence on what evidence would resolve it. Keep the answers — you will return to them in Chapter 11 and Chapter 13.

2. **(Apply)** For a deployment where all three answers are yes, name one specific piece of information the loop would produce that your current Canvas dashboard cannot. Not a category of information — a specific concrete piece. (Example: "Whether the students who scored 78 on the dosage calculation quiz in week 6 are likely to retain that knowledge for the board exam in 14 months.") The exercise is testing whether you can describe the value proposition in operational terms.

3. **(Evaluate)** For a deployment where at least one answer is no, write a one-paragraph defense of why the simpler stack is the *correct* answer, not a compromise. Address the reader who will say "but if Medhavy is even slightly better, shouldn't we adopt it?" The point of the exercise is to make sure you can defend the no answer with confidence to a colleague or a vendor.

---

*Sources cited in this chapter: Daugherty, P. R., & Wilson, H. J. (2018). Human + Machine: Reimagining Work in the Age of AI. HBR Press. · Freeman, S., Eddy, S. L., McDonough, M., et al. (2014). Active learning increases student performance in science, engineering, and mathematics. PNAS, 111(23), 8410–8415. · Bruner, J. S. (1966). Toward a Theory of Instruction. Harvard University Press. · Copeland, D. B. (2014). Brutalist Web Design. brutalist-web.design. · Woolf, B. P. (2009). Building Intelligent Interactive Tutors. Morgan Kaufmann. · Licklider, J. C. R. (1960). Man-Computer Symbiosis. IRE Transactions on Human Factors in Electronics.*
