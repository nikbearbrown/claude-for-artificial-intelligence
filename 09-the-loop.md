# Chapter 9 — The Loop: Present, Measure, Adapt

In 1952, a Columbia statistician named Herbert Robbins published a short paper in the *Bulletin of the American Mathematical Society*. The paper was called *Some Aspects of the Sequential Design of Experiments*. It described a problem that sounds deceptively simple: you are in a casino with a row of slot machines, each with an unknown payout rate, and you have a finite number of pulls. How do you allocate your pulls?

If you only play the machine that has paid out best so far, you never discover whether a different machine pays out better. If you only try machines you have not tested yet, you waste pulls on options that probably will not work. The problem is how to balance *exploitation* — use what you know — against *exploration* — learn what you do not yet know. Robbins showed that this tension has a precise mathematical structure and that you can, in principle, navigate it optimally.

The paper sat largely in statistics for forty years. Then it became one of the most-deployed algorithmic ideas in modern technology. The article a news aggregator chose for you this morning was selected by a contextual bandit. So was the show your streaming service surfaced last night. So was the ad that appeared on your search results page. The algorithm that Robbins sketched in 1952 is now running at scale across most of the platforms that compete for your attention.

And now it is running inside a learning system. The translation from casino to classroom is direct, and it is worth making precisely, because the translation is where the interesting design decisions live.

---

## The loop, stated plainly

Medhavy is not a smarter way to present content. It is a system that learns, per student per concept, which interventions produce genuine learning — and surfaces those interventions more frequently.

The loop has four steps, and all four have to be present for it to close.

First, present differently. Not a wordier explanation for a struggling student and a tighter one for a strong student — that is the naive version of adaptive learning, and it is not what is happening here. The variation is in *pedagogical approach*: Socratic versus didactic, problem-first versus concept-first, spaced retrieval versus generative assignment. Each is a different cognitive operation. The four modes from the earlier chapters — Ask AI, Quiz Me, Case Study, Glimmer — are the units of variation the loop selects among.

Second, measure whether it helped. Not engagement metrics. The seven signals from Chapter 8 — the behavioral traces that distinguish genuine learning from borrowed certainty. Chapter 7 established why engagement metrics cannot serve as the success signal: the Bastani study showed identical engagement profiles producing opposite learning outcomes. The measurement has to be the right kind of measurement, or the loop optimizes for the wrong thing.

Third, adapt. The algorithm updates its policy for this student-concept pair. Interventions that produced learning signal get more weight. Interventions that did not get less. The policy evolves.

Fourth, repeat. The loop runs continuously across the term, across the concept map, across the student population.

Canvas can do the first step in a limited way — different assignments to different students — and the third step not at all. There is no algorithm inside Canvas that reads signals and updates policy. A general-purpose chatbot can do neither. The loop requires measurement and adaptation in the same system. That is the architecture-level reason a bolt-on tool cannot close it.

<!-- → [INFOGRAPHIC: Four-step loop diagram — Present Differently → Measure (seven signals) → Adapt (policy update) → Repeat — with annotations at each step noting what Canvas can and cannot do. The visual should make the loop's closure visible and show where Canvas exits the diagram] -->

---

## What Robbins actually solved

The mathematics of the multi-armed bandit can be stated without any formulas, and it should be, because the intuition is the important part.

Imagine you are managing a classroom and you have three teaching interventions available for a concept. You do not know in advance which one works best for any given student. You have to decide, on each session, which intervention to run. You observe the outcome. You update your beliefs. You decide again.

The naive approach is to try all three equally and take the average. The problem is that you are wasting sessions on interventions that early evidence suggests are less effective. The smarter approach is to update your beliefs after each session and gradually shift toward the intervention that seems to be working — while still occasionally trying the others, because your early evidence might be wrong.

This is the exploitation-exploration tension. Exploit too aggressively and you get stuck on a locally good option, missing the globally better one. Explore too broadly and you waste sessions on interventions you already have strong evidence against. The bandit algorithm navigates this tension with mathematical guarantees: it can bound the *regret* — the gap between the choices it made and the choices it would have made with perfect information — and show that the regret grows slowly relative to the number of sessions.

The *contextual* part of *contextual bandit* is what distinguishes the educational application from the casino version. In a plain bandit, the payout rate of each machine is fixed. In a contextual bandit, the payout depends on context — for a learning system, the context is everything the system knows about this student at this moment: their prior signal history, the prerequisites they have or have not consolidated, the time in the term, the difficulty level of the concept they are working on. LinUCB, developed by Auer, Cesa-Bianchi, and Fischer in 2002 and extended by Li and colleagues in 2010 for large-scale deployment at Yahoo News, is the workhorse algorithm. Thompson sampling, a Bayesian alternative going back to 1933 and revived in deployment in the 2010s, is the principal competitor. The specific variant Medhavy uses is an engineering choice. The class of algorithm is settled.

A curriculum director does not need to know which variant is running. A curriculum director does need to know three things: the algorithm class has rigorous mathematical guarantees; it has been deployed at scale for fifteen years across industries with far larger student populations than any single institution; and the educational deployment literature — Lan and Baraniuk, Liu and Koedinger, Clement and colleagues, J. J. Williams's AXIS system at *Learning @ Scale* 2016 — shows the bandit producing learning gains in pilots. Whether those gains are *durable* learning gains or immediate-performance gains is the open question, and it is exactly the question that the choice of reward signal determines.

---

## The reward signal is everything

Here is the decision that most adaptive learning systems get wrong, and it is worth being precise about why.

Most deployed adaptive learning systems use immediate accuracy as the reward signal. The student answered correctly; the system counts that as a win; the policy updates toward whatever intervention produced the correct answer. This sounds reasonable. It is the Bastani failure mode, precisely stated.

If the reward signal is immediate performance, an AI tutor that produces fluent immediate performance — by giving the answer — looks like a successful intervention. The bandit's policy updates toward answer-giving. The students get more interventions that give them answers. The downstream learning collapses. The dashboard says it worked.

This is not a hypothetical. It is the mechanism that Bastani and colleagues documented in 2025: students with access to an unguarded AI scored roughly forty-eight percent higher during practice and seventeen percentage points *lower* on the final exam without AI access, compared to students who had no AI at all. An adaptive system with immediate accuracy as its reward signal would have classified those students as its biggest successes.

Medhavy's reward signal is delayed retrieval accuracy — how well a student can retrieve the concept, unaided, approximately seven days after the intervention. The seven-day delay is what makes the loop optimize for the Bjork side of the performance-learning distinction rather than the immediate-performance side. It is also what makes the loop slower to converge than a system optimizing for immediate signals. Both consequences are intentional.

This is the architectural difference between Medhavy's loop and the adaptive learning systems that have been on the market for a decade. The bandit is not novel. The choice of what to optimize — what counts as a payout — is the load-bearing decision. Engagement as payout produces engagement optimization. Immediate accuracy as payout produces performance optimization that can run inverse to learning. Delayed retrieval as payout produces — the bet is — durable-learning optimization.

The bet is principled. The components are evidence-based. The integration at the scale Medhavy proposes is forthcoming evidence rather than completed evidence. If you adopt now, you are an early adopter. That is not a concealed flaw; it is the honest state of the field in 2026.

---

## Eight weeks, one student, one concept

The best way to see what the loop actually does is to watch it run. The concept is beta-blockade clinical decision-making — the same concept that has threaded through the earlier chapters. The student is in her second year of a pharmacy program.

In week one, the bandit has no data on this student-concept pair. It defaults to Ask AI, which is the appropriate mode for initial acquisition. The session produces strong engagement signals but weak calibration — the student is fluent but unconfident. The bandit notes the calibration weakness and tries Quiz Me in week two.

Week two shows coherent error patterns and growing retrieval strength on factual recall. By week three, the bandit runs a mix of Quiz Me and Ask AI and watches the retrieval signal consolidate. The prerequisite gate for Case Study is met.

Week four is the first Case Study session. Transfer signal emerges — faint but present. The student responds well to graduated hints. The bandit weights Case Study upward.

Weeks five and six show a stabilizing signal profile. Case Study is becoming primary; Quiz Me runs in maintenance mode to protect the earlier gains. By week six, all seven signals are trending upward and the policy is converging.

In week seven, the student hits the Glimmer eligibility threshold. The first Glimmer attempt surfaces specific confusions in her reasoning defense — the kind of misconceptions that would not have been visible in a quiz score. The bandit adds Glimmer to the weekly mix.

By week eight, the steady-state policy looks like this: forty percent Case Study, thirty-five percent Quiz Me, twenty percent Glimmer, five percent Ask AI. The GLP score is high. The faculty member reviews the profile.

<!-- → [TABLE: Eight-week bandit trace — columns: Week, Prior signal state, Intervention chosen, Signals captured, Policy update — rows: weeks 1–8] -->

The first three weeks look more like exploration than personalization. The bandit has no data. It defaults to the acquisition mode, observes the calibration weakness, tries the appropriate remediation, and waits for the signal to consolidate before unlocking the higher-cognitive-load modes. This is the cold-start problem, and it is real. The first six sessions for any new student-concept pair are exploratory by necessity. Faculty should expect bandit choices to look unconfident during this window. The mitigation is not algorithmic; it is faculty awareness and the ability to override.

Weeks four through eight look like what the loop is supposed to do. The policy has diverged from the population average. A different student on the same concept might end week eight with a very different policy: heavy on Quiz Me if retention is the bottleneck; heavy on Glimmer if the student is unusually advanced; mostly Ask AI if prerequisite material keeps surfacing as a gap.

Now look at the same eight weeks through Canvas. Time on page. Click counts. Module completions. The student looks the same as the student sitting next to her in week one and the same as a student on a completely different bandit policy in week eight. The loop ran eight weeks of measurement and adaptation; Canvas's view never changed.

This contrast is the one with the most purchase in a budget committee conversation. Canvas cannot produce the diverging-policy picture because Canvas has no policy to diverge.

---

## What the bandit is not

It is not a replacement for faculty. The bandit surfaces signal that the faculty cannot produce themselves — not because they lack skill, but because no instructor team can hold seven behavioral signals per student per concept in working memory across a three-hundred-student multi-section program. The bandit does the data work. The faculty do the judgment work: reviewing the GLP dashboard, overriding choices when the cold-start picture looks wrong, authoring the Case Study scenarios the bandit selects among, grading the Glimmer outputs the bandit schedules. The bandit is an instrument. The faculty are the meta-model.

It is not A/B testing the students. A/B testing splits the population in two and compares averages. The bandit operates per student per concept and converges on a policy specific to each pair, sharing priors where structure is shared and diverging where it is not. It also has rigorous regret guarantees that A/B testing does not natively have.

And it is not the AI part. The bandit is a classical algorithm — Robbins, 1952, with theoretical extensions through the 1990s and 2000s and deployment at scale through the 2010s. The AI lives in the modes: the LLM that runs the Socratic facilitation in Ask AI, the LLM-driven facilitator inside faculty-reviewed Case Study scenarios. The loop's intelligence is the bandit plus the seven-signal measurement layer. The AI is one ingredient. The architecture is larger than the AI.

---

## Five honest limits

The cold-start problem is real. Six sessions of exploratory behavior before the policy stabilizes means six sessions of sub-optimal choices for every new student-concept pair. Faculty override during this window is not a nice-to-have. It is a structural requirement.

The reward signal is a bet. Seven days is a principled choice — the Bjork literature on spacing intervals gives ranges but not a single optimal. Whether seven days is better than three or fourteen for durable-learning optimization is not established.

The bandit's policy is auditable but not natively explainable. A faculty member can see what the bandit chose. The *why* — why this student got Case Study this week rather than Quiz Me — is the kind of counterfactual explanation that bandit policy outputs do not naturally produce. This matters for student trust and faculty acceptance in ways that have not been fully worked out.

Equity of adaptation is a genuine open question. A bandit that adapts to a student's early signal signature can entrench disadvantage if the early signals are noisy — particularly for students whose engagement patterns differ from the population the priors were trained on.

The institution has to be willing to act on what the loop reveals. A bandit that produces a clear policy signal is worthless if the institution cannot or will not let the policy run. Medhavy without the institutional commitment to act on signal is expensive Canvas analytics. Be honest with yourself about this before the adoption decision. Chapter 11 is the test.

---

## Exercises

1. **(Analyze — application to your deployment)** In your current deployment, who performs the *adapt* function? Be specific. Is it an instructor who adjusts mid-term based on exam scores? A curriculum committee that revises the next year's syllabus? No one? Write the honest answer in one sentence. Then write what information that person uses to make the adaptation, and what information they currently do not have but would value.

2. **(Apply — application to your deployment)** For one high-stakes concept in your curriculum — the same concept you named in Chapter 8's Exercise 2 — describe what the loop would need to measure to determine whether students are genuinely learning the concept versus producing performance that decouples from learning. Name the two or three of the seven signals that would be most relevant. Name what *adapt* would mean concretely for this concept.

3. **(Evaluate — application to your deployment)** The bandit requires a reward signal. In Medhavy, the reward signal is delayed retrieval accuracy at seven days. In your current deployment, what is the equivalent? When you currently evaluate whether a course is *working*, what measurement are you actually looking at, on what time delay? Is that measurement available without Medhavy? If not, what would it cost — in faculty time, in student time, in instrument design — to produce it without adopting Medhavy?
