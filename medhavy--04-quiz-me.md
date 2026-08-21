# Chapter 4 — Quiz Me: Making Knowledge Stick

*The study technique that feels most productive is not the one that produces the best retention. The gap between feeling and outcome is the variable your students are navigating every time they open a textbook.*

---

Here is a finding so well-replicated it functions as a law: testing yourself on material produces more durable learning than re-reading it, even when re-reading feels more productive. Students who study by testing themselves perform worse on a quiz given immediately after the study session and better on every subsequent quiz at longer delays. The crossover is reliable. The size is meaningful. And the direction runs exactly opposite to student intuition.

Henry Roediger and Jeffrey Karpicke demonstrated this cleanly in a 2006 *Psychological Science* paper that has since been replicated hundreds of times. Their paradigm was elegant. Students read short prose passages. Some students re-read the passages multiple times. Others read once and then tested themselves with free recall. Immediately after the study session, the re-readers scored higher — they could reproduce more from the passage. They felt productive. They predicted they would do better on the follow-up. Then came the delays: two days, one week. The re-readers' performance collapsed. The self-testers' performance held. By the one-week measurement, the testing group was outperforming the re-reading group by a margin large enough to overturn fifty years of intuitive study advice.

The students' predictions, before the delay, were exactly backwards.

This is the finding Quiz Me is built on. Not as a metaphor or a design inspiration — as a mechanism. The chapter's job is to install that mechanism clearly enough that the reader can see why Quiz Me is not a quiz, not a flashcard app, and not a graded assessment. It is retrieval practice implemented as a daily habit, scheduled by an algorithm that knows more about your students' forgetting curves than your students do.

---

Memory is not a recording you replay. It is a structure you rebuild every time you retrieve. The rebuilding is what consolidates the memory — each retrieval is a reinforcement of the pattern that lets you retrieve it next time. Re-reading skips the rebuilding step. You recognize the material on the page; recognition is much easier than recall; recognition does not consolidate the trace the way recall does. Two students who spend the same hour on the same material — one re-reading, one self-testing — leave the hour with different memory structures. The self-tester has the structure that survives.

Karpicke and Blunt sharpened this in a 2011 *Science* paper that ran retrieval practice against elaborative study with concept maps — a technique many curriculum directors actively recommend. Retrieval practice won again on delayed retention. The concept-map students predicted they would do better. They did worse. The chapter is not asking the reader to abandon concept maps; they have other uses. But the reader needs to know that retrieval practice outperforms even the techniques her faculty are most likely to endorse when the outcome is retention at delay.

The summary a curriculum director can take to a budget meeting is Dunlosky and colleagues' 2013 review in *Psychological Science in the Public Interest* — open-access, written for policy audiences, ranks ten common study techniques by evidence strength. Two techniques receive "high utility" ratings: practice testing and distributed practice. The other eight range from moderate to low. Quiz Me is built on both techniques at the top of the list. This is not a marginal evidence base; it is the strongest evidence base in the entire study-skills literature.

Robert Bjork and Elizabeth Bjork named the underlying principle "desirable difficulties" — the observation that interventions which slow current performance often improve durable retention. Quiz Me feels harder than re-reading. Students will report it as harder. They will rate their comprehension lower. That is the predicted experience of a technique tuned to produce desirable difficulty, and the chapter's recommendation, here and in Chapter 11, is that student satisfaction in the first three weeks of Quiz Me deployment is not the right signal to act on. Wait for the retention measurement.

---

The second mechanism is spacing. If you have an hour to study something, distributing that hour across multiple sessions over days produces more durable retention than spending the hour in one block. Cepeda and colleagues' 2006 meta-analysis in *Psychological Bulletin* synthesized 184 studies of verbal recall and found the effect large, consistent, and independent of age and domain. Distributed practice is the technique that paired with practice testing to earn the Dunlosky "high utility" rating. Together they are the two pillars Quiz Me runs on.

The mechanism is the same as before, now applied to scheduling. Each retrieval reinforces the trace; some forgetting occurs between sessions; the next retrieval is slightly harder because of the forgetting; the harder retrieval, when successful, reinforces the trace more strongly than an easy retrieval would. The longer the gap — without crossing into total forgetting — the more the retrieval costs and the more it pays. An algorithm that schedules retrievals at the right intervals is implementing this principle in software.

Piotr Woźniak, a Polish biology student studying English vocabulary in the early 1980s, decided to run self-experiments on his own retention. By 1985 he had built SuperMemo and the SM-2 algorithm — years before the cognitive psychology mainstream caught up to the practical importance of spacing. Woźniak published the algorithm openly. He continued running experiments on himself for decades. The academic literature on the spacing effect was developing in parallel, but Woźniak was operating ahead of it on the practical questions: how long to wait, by how much, when to adjust, what to do when retrieval fails. SuperMemo influenced Anki, which influenced the broader flashcard ecosystem, which influenced FSRS — Free Spaced Repetition Scheduler — the open-source algorithm Quiz Me runs today. FSRS models memory with three parameters (difficulty, stability, retrievability) and personalizes the schedule per card, producing roughly 20-30% fewer reviews for equivalent retention compared to SM-2.

A caveat the chapter has to flag: FSRS is demonstrably more *efficient* than its predecessors. It is not separately demonstrated to produce better *learning outcomes* — the efficiency gain means students spend less time on review for equivalent retention, but whether that translates to measurable course improvements is not a peer-reviewed claim. The honest framing is that FSRS scales the spacing effect efficiently to a curriculum's worth of material. The mechanism is older and more settled than the software.

Harry Bahrick, at Ohio Wesleyan, ran a 50-year retention study published in 1984 — 733 former students of high-school Spanish, tested decades after their last formal instruction. The students whose original study had included spaced retrieval retained vocabulary in what Bahrick called "permastore" — a memory state that resists decay for decades. The students whose original study had been massed lost their vocabulary on the timescale of years. A daily Quiz Me habit in a 15-week pharmacology course is not just preparing the student for the final exam. On Bahrick's long-tail evidence, it is building a memory structure that can survive to the bedside encounter three years out.

---

Now I want to address the question every curriculum director asks when she hears about Quiz Me, because she will have already heard the pitch for Anki and will want to know the difference.

Many health-sciences students use Anki. Many faculty have written or curated Anki decks. Anki is free and it runs FSRS. The "why pay for Quiz Me when Anki is free?" question is real and the chapter has to answer it honestly. Four differentiators, each one load-bearing.

The first is concept-map integration. Anki cards are orphans. They exist in the deck, scheduled by FSRS, decoupled from any curriculum structure beyond the tags the student or deck author chose to apply. Quiz Me cards are pinned to nodes in a concept map — a graph the institution builds that names the concepts in the curriculum and the prerequisite relationships between them. When the bandit that governs mode selection (Chapter 9) decides whether to schedule a Quiz Me session on receptor pharmacology, it is operating on the same concept node that Ask AI and Case Study operate on. A struggle on a Quiz Me card on beta-1 selectivity becomes a signal the bandit can use to decide whether to deploy Ask AI on the prerequisite concept. The cards are not orphans. They are instrumented nodes in a measured curriculum.

<!-- → [IMAGE: diagram showing an Anki card as an isolated node vs. a Quiz Me card as a node in a concept-map graph with prerequisite edges and bandit connections; student should see that the integration is structural, not cosmetic] -->

The second differentiator is priority weighting for high-importance concepts. Anki treats every card equally — the algorithm schedules based on retention alone. Quiz Me weights concepts by institutional importance. A safety-critical concept — the contraindications for beta blockade in decompensated heart failure, the difference between IV push and IV piggyback for a high-alert medication — is weighted upward; the algorithm allocates more practice to it even if the student is consistently retrieving correctly. The instructor assigns the weights. Quiz Me operationalizes them.

The third differentiator is what I call the aviation pedagogy override, and it is the most consequential one for nursing and pharmacy programs. The FAA Aviation Instructor's Handbook is the most explicit articulation of this principle outside the military: commercial pilots review certain procedures — emergency descent, stall recovery, decision speed callouts — *regardless of recent demonstrated competency*. The recall score is irrelevant; the procedure is reviewed on a fixed schedule because the cost of forgetting it is fatal. Aviation has built this override into every flight school's curriculum for decades, and the safety record reflects it. Quiz Me brings the same override to health sciences. The faculty designates certain concepts as safety-critical. Those concepts get reviewed on a regular schedule, never spaced out below a minimum interval, no matter how strong the student's retrieval history has been. This is not an FSRS feature. It is not an Anki feature. It is a Quiz Me feature, and for a program that graduates students who will handle high-alert medications and emergency procedures, it may be the single most important differentiator on the list.

The fourth differentiator is prerequisite interleaving. When FSRS schedules a card, it schedules that card. Quiz Me, because it knows the concept map, can interleave cards from the prerequisite chain — practicing the beta-1 selectivity card alongside cards on adrenergic physiology and sympathetic activation. Interleaving forces discrimination learning: the practice that distinguishes between similar-looking concepts under time pressure. Two drugs with similar-sounding names and different mechanisms. Two clinical syndromes with overlapping presentations and different management. The interleaved-practice literature, developed by Rohrer and colleagues from 2007 onward, is clean: interleaved practice produces better discrimination than blocked practice, and discrimination is what clinical performance under pressure requires.

The four differentiators together are the answer to the budget-meeting question. Anki is a free, excellent tool for self-directed learners. Quiz Me is an institutional tool that integrates with curriculum, instructor dashboards, and the rest of the loop. A program that wants to ensure 300 students across five sections retain safety-critical material before they touch a real patient cannot get that guarantee from a free flashcard app, however good the algorithm.

---

Let me work through a concrete comparison so the mechanism is visible rather than asserted.

Two PharmD students preparing for the same pharmacology board exam, twelve weeks out. Same content, same baseline, same target.

Student A re-reads. Ninety minutes every Sunday afternoon with the AI+1 pharmacology text. Highlights. Margin notes. Self-rates comprehension as high after each session. Two weeks before the board exam, she takes a practice test and scores 78. She feels prepared.

Student B uses Quiz Me. Twelve minutes every morning before clinical rounds, working through whatever the algorithm has scheduled. Sixty to ninety cards a day, some from six months ago, some from this week. She finds the practice annoying — many days she retrieves cards wrong, and she has no way to feel productive about it. Two weeks before the board, she takes the same practice test. Scores 72. She does not feel prepared.

By every in-session signal, Student A is winning. The dashboard shows Student A winning.

The board exam. No AI, no notes. Student A scores 81. Student B scores 89.

What happened is the testing effect in one scenario. Student A's re-reading produced strong recognition memory — the practice-test items, written by the same faculty as her textbook, looked familiar; she could pick the right answer through partial recognition. The board exam items, written by the national testing body, did not look familiar. Recognition memory does not transfer when the surface features change. Student A had the structure of a re-reader: high in-session performance, weak retrieval at delay.

Student B's spaced retrieval produced durable recall memory. The board exam required retrieval, not recognition. She had practiced retrieval every morning for twelve weeks. The cards she had struggled with had been spaced out; the cards she had retrieved easily had been spaced out further. By exam day, her retention structure was the structure that survives the lossy transfer from study material to test material.

For the curriculum director: the chapter is not asking for faith. It is asking for recognition that the dashboard signals your faculty currently trust — practice-test scores, student satisfaction, perceived comprehension — are signals from inside the practice window. The signal you care about is on the other side of the lossy transfer to the licensure exam, the clinical encounter, the situation twelve months from now when the student retrieves without scaffolding. That signal lives in cards being retrieved at delay. Quiz Me's FSRS schedule is designed to produce evidence on exactly that signal.

---

Quiz Me is the retention mode. It does that job well. Three places it does not, and the failures matter because they reveal what the other modes are for.

The first failure: application under ambiguity. Quiz Me cards have a correct answer. This works for "what is the half-life of metoprolol" — there is a number, and either the student retrieves it or she does not. It does not work for "should this patient receive beta blockade?" Clinical decision-making under ambiguity has no card-correct answer; the cognitive operation is weighing competing considerations, not retrieving from memory. Forcing clinical decisions into a flashcard format produces pattern-matching — students learn the surface cues that generate the expected answer, not the reasoning that generates a defensible decision. Case Study (Chapter 5) is the right mode for that cognitive operation.

The second failure: generative work. A student cannot retrieve a novel patient-education protocol from memory, because she has not produced one yet. The cognitive operation is generative — building something new, defending it, revising it. Quiz Me does not build this. Glimmer (Chapter 6) does.

The third failure: first-encounter acquisition. A student who has never encountered a concept cannot retrieve it. Quiz Me cards on first-encounter material produce the experience of failing every card, which is demoralizing without being instructive. The right entry point is Ask AI (Chapter 3); Quiz Me enters once the schema is forming and needs to be made durable.

The sequence is acquisition (Ask AI) → retention (Quiz Me) → application under ambiguity (Case Study) → generative production (Glimmer). Quiz Me is the second step. A program that deploys it as the whole system is using the second step to do the work of all four.

---

There is one more thing the chapter has to address, and it is the thing most predictive of whether Quiz Me succeeds in a particular deployment.

Quiz Me is designed as a *habit*, not an assessment. The interface is built around a due-count counter — the number of cards waiting for review today — and a completion signal when the counter reaches zero. Twelve minutes a day, triggered by the counter, rewarded by the reset. The instructor's gradebook does not look at Quiz Me by default. The institution does not punish missed days directly. The algorithm does the work of scheduling; the student's job is to show up.

Most deployments show a bimodal adoption pattern: roughly 20% of students never form the habit and largely ignore Quiz Me; 60-80% form the habit and use it consistently; the remainder adopts late. The institutional levers that shift this distribution are not Quiz Me features. Programs that make usage a graded component — five percent of the course grade for hitting weekly retention thresholds — reliably achieve 80% or higher adoption. Programs that make it optional reliably achieve 30-50%. The habit-gap problem is not solvable by the software alone.

The aviation parallel matters again here. The FAA does not make recurrent training optional. The reason aviation has the safety record it has — the reason a 60-year-old pilot can perform a procedure she last used three years ago — is that the institution mandates the practice schedule. Quiz Me provides the algorithm and the interface. The institution provides the requirement. An institution that adopts Medhavy and then makes Quiz Me optional has not closed the loop on the retention layer. Most of the value evaporates.

This is Question 3 of the three-question test from Chapter 2, applied to a specific mode: willingness to act, in the Quiz Me context, means willingness to make Quiz Me usage an enforced component of the curriculum. If the answer to that question is uncertain, resolve it before deploying the software.

---

Quiz Me makes factual and conceptual knowledge durable. It does the retention job on the most replicated finding in cognitive psychology, with the most efficient scheduling algorithm currently available, and with four curriculum-integration features that a free flashcard app cannot replicate.

What it does not do is teach students to use that knowledge when the situation is ambiguous and the right answer is not obvious — when a patient presents with multiple competing considerations, when the textbook's clean case becomes the bedside's messy one. That gap is what the Carnegie Foundation documented in medical education in 2010 and engineering education in 2008: the distance between *knowing* and *doing*. Quiz Me does not close it. Neither does Ask AI. The next chapter introduces the two modes designed to close it — Case Study, and a mode most readers have never encountered, called Glimmer.

---

## LLM Exercises

1. **(Apply, to your own curriculum)** Identify five concepts in your curriculum that require durable factual recall — drug names and dosing ranges, anatomical structures, clinical decision criteria, lab value thresholds. These are Quiz Me candidates. Then identify five concepts that require reasoning under ambiguity — when to escalate, how to weigh competing risks, when to deviate from protocol. These are not Quiz Me candidates; they are Case Study territory. The exercise is to make sure you can tell the difference between content types. If you find yourself wanting to put a concept in both lists, that concept probably has a retrieval-foundation component (Quiz Me) and an application component (Case Study) — note both.

2. **(Analyze)** Your institution currently uses Canvas quizzes for retrieval practice. What does Quiz Me's FSRS scheduling and concept-map integration add that Canvas quizzes cannot provide? Be specific: name at least two mechanisms (e.g., adaptive scheduling per card, concept-prerequisite interleaving, safety-critical override). The exercise tests whether you can defend the line item against the "we already do quizzes in Canvas" objection — which you will hear.

3. **(Evaluate, to your own deployment)** For a 15-week course, estimate the difference in total Quiz Me sessions a student would complete if the habit forms in week 2 versus week 6. Then identify the single curriculum-design choice that, in your judgment, would most affect when the habit forms. Common candidates: making usage a graded component, requiring a 7-day streak as a course participation gate, framing Quiz Me as professional habit-building in the first lecture rather than as a study tool. The exercise is testing whether you can name the institutional lever, not just the software feature.

---

*Sources cited in this chapter: Roediger, H. L., & Karpicke, J. D. (2006). Test-Enhanced Learning. Psychological Science, 17(3), 249–255. · Karpicke, J. D., & Blunt, J. R. (2011). Retrieval Practice Produces More Learning than Elaborative Studying with Concept Mapping. Science, 331(6018), 772–775. · Cepeda, N. J., Pashler, H., Vul, E., Wixted, J. T., & Rohrer, D. (2006). Distributed practice in verbal recall tasks. Psychological Bulletin, 132(3), 354–380. · Dunlosky, J., Rawson, K. A., Marsh, E. J., Nathan, M. J., & Willingham, D. T. (2013). Improving Students' Learning With Effective Learning Techniques. Psychological Science in the Public Interest, 14(1), 4–58. · Bjork, R. A. (1994). Memory and metamemory considerations in the training of human beings. · Bahrick, H. P. (1984). Fifty years of memory for Spanish learned in school. JEP: General, 113(1), 1–29. · Rohrer, D., & Taylor, K. (2007). The shuffling of mathematics problems improves learning. Instructional Science. · Woźniak, P. (1990). SM-2 algorithm. SuperMemo documentation. · Ye, J., et al. (2022–present). FSRS — Free Spaced Repetition Scheduler. github.com/open-spaced-repetition/fsrs4anki. · Federal Aviation Administration. Aviation Instructor's Handbook, FAA-H-8083-9.*
