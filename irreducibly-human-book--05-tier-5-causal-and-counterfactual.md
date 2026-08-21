# Chapter 5 — Tier 5: Causal & Counterfactual

*Prediction is not identification*

---

## A model that was right about everything and wrong about what to do

A health-technology team ships a readmission-prediction model. On held-out data it is accurate — call it ninety-four percent, the kind of number that ends the meeting and starts the press release. The operations team does the obvious thing: it routes the model's high-risk flags to the nursing staff, who place extra follow-up calls to the patients most likely to bounce back to the hospital. The intervention is humane, cheap, and aimed precisely where the model says the danger is.

Readmissions go up. [Medium — this is a documented pattern synthesized from production deployments rather than a single named, peer-reviewed case; present as composite. [verify: a citable named deployment]]

Nothing in the model broke. It captured every correlation in the training data faithfully. The problem is that being *flagged as high-risk by a predictive model* does not share a mechanism with *being readmitted*. The model learned which patients tend to come back; it learned nothing about what would happen if you reached in and changed something. When the team acted on the flags — intervened on the correlates — the relationships the model had memorized shifted underneath it, because the model had been trained on a world in which nobody was making those calls. The patients who got the extra attention did not improve, because the feature that predicted their readmission was not a cause of it.

This is the cleanest possible illustration of the chapter's claim, and it is worth stating plainly before any formal apparatus arrives: **capturing every correlation in a system is not the same as understanding a single cause within it.** A model can be a near-perfect predictor and a near-total stranger to the mechanism. Prediction is association. Acting on a prediction is intervention. The gap between them is the territory of Tier 5, and it is a gap no amount of predictive accuracy crosses on its own.

![Paired bars contrasting high predictive accuracy with low causal-structure recovery, the low red bar barely above a dashed random baseline, illustrating the prediction-identification dissociation.](images/05-tier-5-causal-and-counterfactual-fig-02.png)

*Figure 5.2 — A model can be near-perfect at prediction and near-chance at recovering causal structure: the gap no accuracy crosses.*

---

## Pearl's ladder, and the rung the machine lives on

The structure underneath all of this was systematized by Judea Pearl in *Causality* (2000) and given its popular statement in *The Book of Why* (2018) [High]. Pearl's ladder of causation has three rungs, and the distance between them is the whole subject.

![A three-step ascending ladder labelled association/seeing, intervention/doing, counterfactual/imagining, with a red marker pinning the machine to the lowest rung and a dashed Causal Hierarchy Theorem barrier above it.](images/05-tier-5-causal-and-counterfactual-fig-01.png)

*Figure 5.1 — Pearl's three rungs; the machine is pinned to rung one, and no quantity of rung-one data climbs to the next.*

The first rung is **association**: *what is correlated with what?* This is the rung of seeing. It answers questions of the form "if I observe X, what should I expect about Y?" — the readmission model's entire world. The second rung is **intervention**: *what happens if I do X?* This is the rung of doing, and it is categorically different, because doing X is not the same as observing X. Patients who are observed to take a drug differ from patients who are made to take a drug; the act of intervening severs the web of reasons people had for taking it in the first place. The third rung is **counterfactual**: *what would have happened to this patient had we done Y instead?* This is the rung of imagining — reasoning about a world that did not occur, for a specific case, holding everything else fixed.

Current AI, including the most capable large language models, operates primarily on the first rung [High]. It is architecturally optimized to extract pattern from observational data and to predict from it. This is not a slur; it is what the technology is for, and on the first rung it is often superb. The trouble begins when first-rung machinery is asked to do second- and third-rung work — when a predictive output is read as if it told you what to *do*.

The decisive point is that the higher rungs are not reachable from the lower ones by accumulating more data. This is the **Causal Hierarchy Theorem** (Bareinboim, Correa, Ibeling, and Icard) [High]: interventional and counterfactual quantities are, in general, *not identifiable* from purely observational data without additional structural assumptions. This is a theorem about information, not about architectures. No quantity of rung-one observation — no matter how vast, how clean, how well-modeled — determines a rung-two or rung-three answer on its own. You need a causal model, and the model carries assumptions that did not come from the data. As Pearl puts it, the data do not speak for themselves; someone must supply the causal story, and the story comes from outside.

That "someone" is the human, and the act of supplying the story is what this chapter calls the **identification layer** — the judgment about whether a given causal claim can be estimated from given data, under given assumptions. It is the single most important thing in the tier, and it is precisely the thing the machine cannot supply.

A word of discipline here. It is tempting to escalate the Causal Hierarchy Theorem into a claim that no machine *architecture* could ever climb the ladder — to reach for an impossibility proof about transformers specifically. The honest position is narrower and stronger for being narrow. The theorem is about what observational data can yield, not about what silicon can compute. The boundary at Tier 5 is at the *identification layer* and it is *distributional*: machines fail to generalize causal judgment beyond the distribution they were trained on, not because some kernel of their wiring forbids it forever. [Medium — the "permanent architectural obstruction" framing is contested; lean on the data-level theorem, not a hardware-level one.]

---

## How the field teaches causation — and the error the teaching produces

If the identification layer is the human's job, you would expect education to teach it. It largely does not. What it teaches instead is a slogan and a hierarchy, and both miscarry in instructive ways.

The slogan is *correlation does not equal causation.* It is true, it is necessary, and taught carelessly it produces the opposite error from the one it was meant to prevent. Work in psychology education finds that teaching the slogan leads a substantial share of introductory students — over 30%, on the order of a third — to conclude not that correlation is insufficient for causation but that *correlation cannot mean causation*, that observational data can never license any causal claim at all (Stevens, Witkow & Isbell, *Improving the teaching of "correlation does not equal causation" in Introductory Psychology*, *Frontiers in Psychology*, 2025) [Medium]. This is not a small slip. It disarms the student in front of exactly the situations — most of medicine, most of policy, most of the social world — where randomized experiments are impossible and causal questions must nevertheless be answered from observation. A heuristic built to instill caution instead instills paralysis, and paralysis in front of a confident predictive model is the worst possible posture.

The hierarchy is the research-methods pyramid with the randomized controlled trial at its apex: experiments yield causation, observational studies do not. This is the standard pedagogy across psychology, education, medicine, public health, and the social sciences, and it is partially correct and systematically incomplete. It teaches students a binary — experiment good, observation suspect — rather than the framework that working causal inference actually uses: directed acyclic graphs, the potential-outcomes formalism, the backdoor criterion, the do-calculus. That framework, associated with Miguel Hernán and Judea Pearl among others, gives a formal language for stating causal assumptions, for deciding what can be estimated from observational data and what cannot, and for separating a prediction estimand from a causal one [High]. It exists. It is teachable. Hernán and Robins's open textbook *Causal Inference: What If* is a standard reference [High]. And it remains confined almost entirely to epidemiology, econometrics, and specialist data-science programs. It is not standard in medical education, in law, in engineering, or in business. The fact that nursing graduate programs are now being *called upon* to adopt directed-acyclic-graph methods tells you how wide the gap still is. [Medium]

The professional version of the student's error is more expensive. Among researchers, a common and consequential misunderstanding is that the coefficients of a prediction model can be read as causal effects (Dyer, *Variable selection for causal inference, prediction, and descriptive research: a narrative review of recommendations*, *European Heart Journal Open* 5(3):oeaf070, May 2025) [High]. They cannot. A prediction model is built to forecast under the existing distribution; it is not built to eliminate confounding, avoid collider bias, or keep causal paths open. Reading its coefficients as the effects of intervening is a category error, and it produces five distinct structural failures, each of which yields a model that is predictively accurate and causally wrong:

| Error | Mechanism | Consequence |
|---|---|---|
| Confounding | A third variable causes both predictor and outcome; it is not in the model | The predictor looks effective; intervening on it does nothing |
| Reverse causation | The outcome causes the predictor, not the reverse | Intervening on the "cause" cannot move the outcome |
| Collider conditioning | The model conditions on a variable caused by both predictor and outcome | A spurious association is *created* by the model itself |
| Mediation | The model adjusts for the mechanism on the causal path | The path is blocked; the real effect disappears from view |
| Selection bias | Current treatment is included as a predictor | Prediction-under-treatment is confused with prediction-under-intervention |

The conclusion the methods literature draws is not optional and not hedged: predictions meant to inform interventions require causal reasoning during development and validation. The identification layer is not a nicety added at the end. It is the condition under which a model's output may be acted upon at all.

---

## What the machine actually does: the causal parrot

There is a temptation to assume that a system fluent enough to write a flawless paragraph about confounding must, somewhere inside, understand confounding. The evidence says otherwise, and it is now substantial and consistent.

The framing is Zečević and colleagues' *Causal Parrots* (TMLR, 2023): large language models can recite causal-sounding language because their training corpus is saturated with causal claims expressed in natural language [High]. When a model tells you smoking causes lung cancer, it is retrieving a fact stated thousands of times in its training data — not inferring a relationship from evidence. This is pattern-matching on the *surface of causal discourse*, and it is exactly as deep as the discourse on the surface.

The sharpest empirical test is Jin and colleagues' **Corr2Cause** benchmark, which asks models to infer causation from correlational statements — the identification step itself, stripped of memorizable facts [High]. Seventeen large language models were evaluated. GPT-4 achieved an F1 score of **29.08**, barely above the random-uniform baseline of roughly 20, and below the best fine-tuned baseline of around 33 [High]. Fine-tuned models could be pushed to high accuracy *on the training distribution* and then collapsed under perturbations as trivial as renaming the variables. When the answer was not in the data, performance fell to near chance.

What the models lean on instead is a temporal heuristic: if A precedes B, A probably caused B. It is a sensible default in familiar domains and it is not causal reasoning — it is temporal pattern-matching that mimics the surface of causal reasoning and breaks under reversed order, renamed variables, or a novel domain [High].

It is worth resisting an over-reading here. The benchmark literature has a complicating result: fine-tuning a model on causal-chain data (the CDCR-SFT approach) can lift CLadder-benchmark accuracy to roughly ninety-five percent, around the human baseline [Medium]. A reader looking for a clean impossibility proof will be disappointed, and should be. What that result actually shows is that *benchmark* performance can be engineered upward by fitting the benchmark's distribution — which supports the memorization reading, not a refutation of it. The boundary is not "the machine can never produce a correct causal token." The boundary is that the machine cannot perform the *identification judgment* — choosing the variables, asserting and defending a causal structure, deciding what is estimable — and cannot do it reliably outside the distribution it was trained on. That judgment is what the human supplies, and it is what no benchmark score substitutes for.

So the ledger for Tier 5 is precise. The machine can retrieve memorized causal claims, generate causal-sounding prose that passes surface review, assist with directed-acyclic-graph notation and causal-inference code, and explain the concepts at textbook level. It cannot identify whether a causal effect is estimable from given data, select variables for a causal as opposed to a predictive analysis, detect an unmeasured confounder in a novel domain, distinguish collider bias from confounding in an unfamiliar structure, or validate whether a counterfactual contrast is licensed by the assumed model. The first list is real work and worth deprioritizing to the machine. The second list is the work to supervise and protect — by formal result, not by preference.

---

## The machine boundary

State it cleanly. At Tier 5 the machine is bounded not by current capability but by the structure of the problem. It retrieves and assists; it does not identify. The reason is the Causal Hierarchy Theorem: the answers the identification layer needs are not contained in the observational data the machine learns from, and so cannot be extracted from that data by any amount of scale. The human's irreducible contribution is the causal model itself — the assumptions about which variables matter, which paths are open, which interventions are valid, which counterfactuals are estimable — together with the prior judgment about whether the question in front of you is even a causal one. That last judgment is where the recursion bites: deciding that a problem requires intervention reasoning rather than prediction is *itself* a causal act, one of the very rungs the tier describes.

---

## Failure modes and consequences

The cost of confusing the rungs is not theoretical. It is documented, large, and growing as predictive outputs are increasingly piped into decisions about what to do.

**The canonical case is Obermeyer and colleagues (2019, *Science*).** A commercial risk-prediction algorithm, used across major United States health systems, predicted future healthcare *costs* as a proxy for clinical *need* — and was accurate at predicting costs [High]. It was also causally blind to a confounder: because of systemic barriers — lower income, worse access, institutional bias — less money is spent on Black patients at any given level of illness. The algorithm read lower spending as lower need. The arithmetic of that blindness was that, at any given risk score, the Black patients flagged were substantially sicker than the White patients flagged — by one analysis carrying about twenty-six percent more chronic conditions [High]. The system steered care-management resources away from the patients who needed them most, and did so on the strength of a confounded correlation it had no way to recognize as confounded. A scale caveat matters and must be stated honestly: the *study itself* analyzed roughly fifty thousand individuals from a single health system; the widely quoted "two hundred million" figure refers to the scale at which algorithms *of this class* are applied across the American health system, not to the study's sample [High — phrase as class-scale, not study sample]. The mechanism is the point: a purely predictive system, optimizing a proxy, reproduced and automated a structural injustice it could not see.

**Predictive policing supplies the runaway version.** Software trained on historical arrest records inherits historical over-policing as if it were a clean signal of where crime is. It flags those neighborhoods as high-risk; patrols increase there; the increased patrols produce more arrests; the new arrests flow back into training data as confirmation. Ensign and colleagues (FAT*, 2018) proved this escalation mathematically using an urn-model analysis of systems like PredPol [High]. The feedback loop is not a malfunction. It is the predictable behavior of a causally blind predictor deployed in a domain where its own outputs alter its future inputs — the second rung's revenge on a first-rung tool.

Two further illustrations belong here as textbook patterns rather than cited single studies. In pharmacovigilance, a predictive model mining records for adverse drug reactions may assign a high weight to a co-prescribed drug — not because that drug causes the reaction, but because the patients taking the first drug are sicker and routinely receive the second [Medium — standard epidemiological illustration, not a named study]. A causal diagram would expose the confounder at a glance; the predictive model cannot represent it. And in finance, correlation-matrix factor models tend to fail precisely during structural breaks, because the correlations they captured were never causally invariant — they held under the training distribution and dissolved under a genuine intervention like a rate shock or a regulatory change [Medium — conceptually sound]. You may have seen a striking dollar figure attached to this — an annual sum in the hundreds of billions ascribed to Fortune 500 firms confusing correlation with causation. Treat that number as an *unverified industry estimate* and do not lean on it; the qualitative claim stands on its own and needs no inflation. [Low — unverified industry estimate; label or omit.]

The market itself confirms the gap from the demand side. A "causal AI" sector is growing quickly, on the recognition that predictive-only systems are insufficient for designing interventions. Adoption is racing ahead. The curriculum that would let practitioners *evaluate* a causal-AI system's outputs — the identification layer, taught as a transferable skill — has not been built. That asymmetry is the chapter's warning in one sentence: we are deploying second-rung tools while teaching, at best, a garbled version of the first rung's caution.

---

## The applied companion

Where this book draws the boundary, the companion volume **Computational Skepticism for AI** teaches the discipline of standing at it. Its remit is exactly the Tier 5 problem operationalized: take Pearl's ladder as the diagnostic, add the supervisory skepticism of Tier 4, and train the reader to catch the statistically valid output that rests on a causally incoherent claim. The pairing is deliberate. Tier 4 supplies the habit of doubting a confident generator; Tier 5 supplies the formal content of the doubt — *is this claim even identifiable from this data?* A practitioner who has both can look at a ninety-four-percent-accurate model and ask the only question that matters before acting on it: accurate at predicting *what*, and under whose intervention?

There is also a tension worth naming, because the identification layer includes the judgment of *which* causal framework even applies. In education and parts of the social sciences, scholars increasingly resist importing the closed-system, treatment-effect machinery of the physical sciences wholesale, arguing for a "becausal" reasoning centered on human agency, values, and deliberation in open, meaning-making systems [Medium — a real and worth-acknowledging debate; [verify: specific framing before attribution]]. This is not anti-causal; it is a claim about which causal questions are the right ones in a given domain. And knowing which framework fits the question in front of you is itself a Tier 5 act — the recursion again, one level up.

---

## Synthesis and bridge

Tier 5 is where the **deprioritize / supervise / protect** spine is at its sharpest. Deprioritize the rote: regression mechanics, retrieval of textbook causal claims, the generation of notation and code — the machine is fluent here, and competing is waste. Supervise the identification layer: the choice of variables, the assertion and defense of a causal structure, the judgment of estimability, the distinction between confounder and collider, the validation of a counterfactual contrast. Protect the disposition that comes before all of it — the reflex to ask whether a question is causal at all before reaching for a predictive tool. Deprioritization is not deletion: you cannot audit a causal claim you have not learned to construct, and the entire argument of this chapter collapses if the reader hears it as permission to skip the formalism. You skip nothing. You learn enough to know when the confident model is answering the wrong rung.

The recursive thesis runs through the tier like a thread. Recognizing that you are in Tier 5 territory — that the question demands intervention or counterfactual reasoning rather than association — is itself a causal judgment, one of the rungs the chapter describes. The capacity to place a task on Pearl's ladder is one of the capacities Pearl's ladder names.

That recursion sets up the next ascent. Tier 5 is about the judgment a single competent mind brings to a causal claim. Tier 6 asks what happens when many minds must reason together — and what is lost when a machine compresses the *outputs* of their past collective thinking while quietly dissolving the *conditions* under which they could think together again.

---

> ### AI Wayback Machine — Judea Pearl, *Causality* (2000) / *The Book of Why* (2018)
>
> Pearl gave the field its ladder — association, intervention, counterfactual — and the do-calculus that formalizes the climb between rungs. His argument is the spine of this chapter: no amount of curve-fitting reaches a higher rung from the data of a lower one. You need a model, and the model carries causal assumptions that the data cannot supply. The data, in his phrase, do not speak for themselves.
>
> The lesson lands hardest precisely now, when systems that have read everything ever written about cause and effect can produce flawless causal prose and still cannot tell you whether the effect you care about is estimable from the numbers in front of you. The ladder is older than the machine and outlasts each year's capability claims, because it is a statement about information, not about hardware. *The model needs a modeler.* Tier 5 is the working-out of that sentence — and the modeler, for the foreseeable future, is you.

---

## Sources

- Pearl, J. (2000). *Causality: Models, Reasoning, and Inference.* Cambridge University Press (2nd ed. 2009). — The ladder of causation; the do-calculus.
- Pearl, J., & Mackenzie, D. (2018). *The Book of Why: The New Science of Cause and Effect.* Basic Books. — Popular statement of the three-rung hierarchy.
- Bareinboim, E., Correa, J., Ibeling, D., & Icard, T. *On Pearl's Hierarchy and the Foundations of Causal Inference.* — The Causal Hierarchy Theorem: higher rungs are not identifiable from lower-rung data alone.
- Zečević, M., Willig, M., Dhami, D. S., & Kersting, K. (2023). *Causal Parrots: Large Language Models May Talk Causality But Are Not Causal.* *Transactions on Machine Learning Research.*
- Jin, Z., et al. (2024). *Can Large Language Models Infer Causation from Correlation?* (Corr2Cause). — GPT-4 F1 = 29.08, near the random baseline; collapse under perturbation.
- Jin, Z., Chen, Y., et al. (2023). *CLadder: Assessing Causal Reasoning in Language Models.* NeurIPS. — Benchmark across associational/interventional/counterfactual queries; CDCR-SFT fine-tuning later reported near-human accuracy.
- Obermeyer, Z., Powers, B., Vogeli, C., & Mullainathan, S. (2019). *Dissecting racial bias in an algorithm used to manage the health of populations.* *Science*, 366(6464). — Cost-as-proxy confounding; ~26% more chronic conditions at equal risk score; class-scale ~200M, study sample ~50k.
- Ensign, D., Friedler, S. A., Neville, S., Scheidegger, C., & Venkatasubramanian, S. (2018). *Runaway Feedback Loops in Predictive Policing.* PMLR (FAT*); arXiv:1706.09847. — Mathematical proof of runaway escalation.
- Hernán, M. A., & Robins, J. M. *Causal Inference: What If.* (open textbook). — Standard reference for the DAG/potential-outcomes curriculum.
- Dyer, B. P. (May 2025). *Variable selection for causal inference, prediction, and descriptive research: a narrative review of recommendations.* *European Heart Journal Open* 5(3):oeaf070. — Distinguishes variable selection for causal vs. predictive vs. descriptive aims; grounds the prediction-to-intervention structural errors. (Title verified.)
- Stevens, Witkow & Isbell (2025). *Improving the teaching of "correlation does not equal causation" in Introductory Psychology.* *Frontiers in Psychology.* — The over-correction failure mode ("correlation cannot mean causation") observed in over 30% of introductory students. (Verified; magnitude pinned.)

*Flags left for the author: the readmission opening is a documented composite, not a single cited deployment (so labeled in text). The EHJ-Open five-error citation title is now confirmed (Dyer, *EHJ Open* 5(3):oeaf070, 2025) and the Frontiers over-correction figure is now pinned ("over 30%"; Stevens, Witkow & Isbell, 2025) — both [verify] flags resolved. The "becausal" debate framing still needs source confirmation before firm attribution and remains hedged. The finance dollar figure is an unverified industry estimate and is treated as such in the text. The unverified "CausaLab 92% / 0.471 F1" figure and the "kernel obstruction theorem (May 2026)" have been deliberately omitted; the prediction/identification dissociation is carried qualitatively and by the verified Corr2Cause and Causal Hierarchy Theorem results.*
