# Chapter 17 — AI as Data Point

*The diagnostic question has been the same since Chapter 1. We are applying it one more time.*

---

The screen in the Tübingen lab shows a cat.

You can see the ears, the posture, the silhouette — everything that makes something a cat. What you cannot see is a square centimeter of cat skin. The surface is gray and wrinkled and deeply furrowed, mapped from a photograph of an elephant. The researchers have done something surgically precise: they have separated the two cues that, in almost every natural photograph, arrive together. Shape says cat. Texture says elephant. It is a forced choice.

The network says: elephant.

The network in question is a convolutional neural network trained on ImageNet — 1.2 million labeled photographs, the benchmark on which deep-learning vision had, by 2018, matched and in some tasks exceeded human-level accuracy. Superhuman performance on the standard test. And here it is, looking at a cat-shaped object and reporting elephant.

The researchers ran the inverse: elephant-shaped objects covered in cat fur. Network said cat. Across hundreds of cue-conflict images the pattern held. The ImageNet-trained networks had learned to classify textures. The benchmark, it turned out, had texture cues redundant with the shape cues all along, and the networks had taken the statistically easier road. They reached human accuracy via a computation that was not the computation the human was running.

![Geirhos cue-conflict — texture beats shape in ImageNet-trained CNNs.](../images/17-ai-as-data-point-fig-01.png)

*Figure 1 — Geirhos cue-conflict — texture beats shape in ImageNet-trained CNNs.*

This is the diagnostic test. Not "did the system get the right answer" — it got superhuman-level right answers on ImageNet for years. The diagnostic is: *what is the system actually doing to produce the answer it produces?* That is the same question this book has been asking since the first page. It produced different results for the bacterium, the octopus, the crow, and the chimpanzee. It produces a different result here.

---

"Is AI intelligent?" is not a question. It is three different questions wearing the same phrase, and conflating them produces the circular arguments that have dominated public conversation about this technology since the field came alive.

The first question assumes intelligence is a quantity, like mass, that can be reported as a single number per entity. Sixteen chapters of comparative cognition have been the empirical case against this. The chickadee can cache 70,000 food items across a territory of several kilometers and recover most of them months later. It cannot produce a sentence. The octopus integrates color and polarization and texture information from eight independently mobile arms, producing a real-time environmental model richer in some dimensions than anything our visual cortex achieves. The octopus has almost no social cognition. The chimpanzee reads coalition dynamics and tracks third-party relationships with precision no textbook can fully capture. The chimpanzee cannot reliably pass a test of recursion. No organism is uniformly high on all axes. "More intelligent" only has an answer once you specify which axis. Applied to AI: there is no global answer. What follows is a profile.

The second question conflates skill with skill-acquisition efficiency. François Chollet, in a 2019 paper, drew a line that comparative cognition had been drawing for decades without a clean name. A model trained on ten trillion tokens that scores 95% on a mathematics benchmark is showing skill. A child who scores 95% on the same problems after seeing five examples in school is showing something different — a much higher skill-acquisition efficiency, a richer deployment of prior structure, a much smaller data footprint for the same performance. Current AI systems buy skill with data at a cost that would be biologically ruinous. The ImageNet-trained network needs 1.2 million labeled examples and, as the Tübingen finding showed, gets there via a different computation than the human uses. Skill present. Skill-acquisition efficiency: much lower than the human child.

The third question — the most important and most easily confused — is whether the function is running or just the language. Systems that produce text learn that text. They learn the language that describes cognitive capacities: "I'm not sure about that," "I might be wrong," "I can see why someone would think that, but..." This language, in humans, is produced by cognitive operations — uncertainty monitoring, belief attribution, perspective-taking. In a language model, it is produced by next-token prediction on a training distribution that included enormous quantities of that language. The question is whether, underneath the language, there is an operation. Not a question about consciousness. A question about mechanism.

| Question | What it assumes | Evidence that would answer it | Evidence that cannot |
|---|---|---|---|
| (1) Is intelligence a height or a shape? | A single ranking exists across all systems | Multi-axis profile across cognitive capacities | Performance on one benchmark, however high |
| (2) Is the system *doing* the thing or *buying* the output? | Skill and skill-acquisition efficiency are separable | Performance on novel tasks given few examples (Chollet ARC) | Performance on tasks similar to training distribution |
| (3) Is the function running or just the language? | Surface output and underlying operation can be separated | Ullman-style perturbations that preserve logic and alter surface | Fluent text production on canonical templates |

---

Now the profile, axis by axis.

**Pattern recognition.** A modern transformer trained on a large enough corpus achieves, on next-token prediction and on many static-pattern-classification tasks, accuracy that no biological system matches in throughput, breadth, or scale. The 2017 dermatology result — a convolutional network trained on 130,000 dermoscopic images matching board-certified dermatologists on sensitivity and specificity — is real. AlphaFold2's protein structure predictions are real. The benchmark improvements are real.

The Tübingen diagnostic does not undo this. It specifies it. The win is real on the axes the benchmark measures. It is silent on the adjacent axes the benchmark does not measure — perceptual invariance to distribution shifts, generalization to cue-conflict inputs, causal structure below the correlational surface. "Superhuman at finding statistical structure in large, labeled, in-distribution datasets" is a true and useful sentence. "Understands what it sees" borrows a word whose full meaning extends well beyond that.

*Profile placement:* Extreme high on in-distribution pattern detection at scale. Drops sharply under distribution shift and cue-conflict conditions. The high is real. The cliff is real.

**Theory of mind.** Frontier language models pass the Sally-Anne test at near-ceiling rates. They have read every false-belief paper, every developmental psychology textbook, and an enormous quantity of fiction in which characters reason about each other's mistaken beliefs.

Tomer Ullman, in 2023, tested what happened when small, logically irrelevant perturbations were made to standard false-belief items. Make the container transparent. Have the character write the location label herself. Introduce a brief, task-irrelevant narrative interlude. In each case, the problem's logical structure was unchanged. A system actually running a false-belief inference — tracking an agent's belief state as a variable that updates based on what the agent has and has not observed — should be unaffected by these perturbations. They should not matter. In Ullman's testing, they mattered significantly: models that had reliably produced the correct answer in standard form failed under these surface-level modifications.

The Tübingen diagnostic, in a different domain. The system is producing the right output via a process that is not the process the human is using. A system operating on statistical association can produce theory-of-mind outputs if the training distribution contains enough examples of those outputs in their associated contexts. The output is sometimes correct. The machinery running underneath is not running the inference we would recognize as theory of mind.

*Profile placement:* High on standard false-belief benchmarks; drops under distribution-shift perturbations in a way that is inconsistent with the underlying operation.

**Metacognition.** Language models produce uncertainty language at appropriate-looking rates. They are also next-token predictors trained on a corpus in which competent writers deploy uncertainty language at appropriate rates. The surface behavior is present; the operation underneath it is not established. The calibration work from frontier AI labs shows partial evidence: these systems' stated confidence correlates with their actual accuracy better than chance and better than smaller models. Whether this constitutes metacognitive monitoring — a genuine internal certainty signal gating output — or a well-calibrated pattern-matcher on text features that correlate with difficulty, is not resolved.

*Profile placement:* Uncertainty language present. Calibration partially present. The underlying operation not yet established.

**Embodied navigation.** A modern multimodal language model, given high-resolution imagery of a Tunisian salt pan, can describe it in four languages, produce a historically accurate account of *Cataglyphis* biology, and discuss the path integration literature in detail. It cannot, reliably, tell you which way the ant should go to get home.

This is not a failure of knowledge. The model has more propositional knowledge about desert navigation than any ant has or could have. The failure is architectural. The ant's navigation is implemented in a body — a physical agent with proprioception, vestibular feedback, a home vector continuously updated by movement through the world, and mortality at the end of a failed return trip. The model's "navigation" is implemented in token sequences about navigation, with no feedback loop that closes on physical consequence.

*Profile placement:* Near-zero on embodied, stakes-driven navigation. Not a deficiency to be patched by adding parameters. A structural fact about a system that has never had a body.

**Collective intelligence and cumulative culture.** AI systems are extraordinary participants in the aggregation layer — fast, high-bandwidth, tireless interfaces to the explicit record of human knowledge. A researcher can access synthesis across thousands of papers in seconds. This is real and consequential.

Tomasello's ratchet runs on practice. The published paper is the frozen record of a long process of failed experiments, revised hypotheses, embodied skill at the bench. The model has access to the paper. It has not stood at the bench. It cannot fail an experiment and learn from the failure, because failure has no cost in a system without stakes and without a body that experiences the consequence of getting it wrong.

*Profile placement:* Extreme high on knowledge retrieval and synthesis. Near-zero on participation in stakes-driven cumulative culture. The gap is not performance. It is architectural.

![AI cognitive profile — extreme highs and extreme lows.](../images/17-ai-as-data-point-fig-02.png)

*Figure 2 — AI cognitive profile — extreme highs and extreme lows.*

---

The preceding sections kept returning to a phrase: *stakes absent*. It deserves its own treatment, because it is the axis that makes sense of the shape of everything above.

Every organism in this book has skin in the game. The bacterium *Escherichia coli* swims toward glucose because cells that did not swim toward glucose did not replicate. The behavior is not a preference encoded separately from fitness: it *is* fitness, crystallized into a gradient-following algorithm. The crow that caches food and protects caches from observers is running a fitness-relevant algorithm under selective pressure that killed the crows who cached carelessly. The chimpanzee tracking coalition dynamics and social rank is doing so in a world where getting it wrong means losing reproductive access or being driven from the group.

Every cognitive capacity in this book was shaped by the cost of getting it wrong, over evolutionary time. The architecture was not designed. It was selected. The selection pressure was mortality, starvation, reproductive failure — the hard stops at the end of wrong turns.

Current AI systems have no hard stops. They are trained on a loss function, optimized by gradient descent. They can have a training loss that penalizes certain outputs. They cannot have stakes in the biological sense, because there is no body to starve, no lineage to continue, no social position to lose. The training process can produce systems that *represent* stakes — that have internal states that function like urgency or avoidance — because those systems were trained on enormous amounts of text written by biological organisms whose lives were full of stakes. The function is present. The evolutionary history that built the function from stakes is absent.

This matters for a specific reason. The cognitive capacities in this book are not just behaviors — they are adaptations. They are good solutions to specific problems under specific constraints, problems that had hard, real-world costs attached. The bee's quorum decision mechanism is calibrated to the actual survival parameters of a colony overwintering in the temperate zone. The elephant matriarch's social knowledge is organized around the features of the savannah environment that actually determine whether a herd prospers or fails. These systems are good in ways that are directly downstream of being shaped by consequences.

A system trained on the *outputs* of stakes-driven cognition inherits whatever structure is visible in the text. It does not inherit the parts of the cognitive architecture that were never written down — that live in the body, the reflex, the procedural memory laid down by ten thousand iterations of actually getting it wrong.

This is not a moral point. It is a mechanical point.

---

The book's two main claims about cognition meet here, and a reader who has been paying attention should now feel the tension. Most of the book has argued *function not substrate*. The honeybee swarm runs the drift-diffusion algorithm; primate lateral intraparietal cortex runs the drift-diffusion algorithm; the algorithm is the thing, the substrate is the medium. The lamprey basal ganglia and the mammalian basal ganglia both implement temporal-difference learning. The corvid pallium and the mammalian hippocampus both support trajectory simulation. The book's repeated finding has been that what cognitive functions *are* is conserved across radically different physical implementations.

The framework that gives this argument its shape is older than the book has acknowledged. In *Vision* (1982), David Marr argued that any information-processing system has to be analyzed at three distinct levels: the computational level — what the system is computing, and why; the algorithmic level — what representations and procedures carry out that computation; and the implementation level — the physical machinery that runs the procedure. Marr's claim was that the levels are genuinely separable: you can ask, and answer, what a system is doing without yet knowing how, and what its representations are without yet knowing what neurons or transistors are running them. The comparative chapters of this book have been making level-one claims throughout. The bee swarm and the primate cortex match at the computational level.

This chapter has been arguing the opposite: that substrate matters, that AI lacks something architectural, that stakes and embodiment are not decorative. The tension is real, and the book owes the reader a resolution.

Here it is. Substrate-independence is true at the level of the algorithm. The function — the computation being run — does not care whether the carrier is bee dance steps or primate cortical neurons or transistors. The drift-diffusion model fits all three. What substrate-independence does not extend to is the layer *above* the algorithm: the question of where the right algorithm comes from in the first place. The bee swarm runs drift-diffusion because bees that ran something less calibrated to the actual statistics of nest-site quality died at higher rates. The mammalian basal ganglia tunes its temporal-difference learning rate to the statistics of the environment because mammals whose learning was poorly tuned ate less and reproduced less. The algorithm is substrate-neutral. The selection pressure that produced the right algorithm was substrate-specific — it ran through bodies, hunger, mortality, lineage.

A trained model can run the drift-diffusion algorithm — that is exactly what current systems do when they accumulate evidence toward a token prediction. What the model has not done is undergo the procedure that would tell it whether the algorithm it is running is the right algorithm for the situation. Gradient descent on a training loss is the AI analog of selection, but the loss was specified by humans whose own losses were under biological pressure. The model inherits the algorithm; it does not inherit the calibration the algorithm earned by running on a body that could fail. This is what is meant, more precisely than the slogan, by the substrate mattering. It matters at the layer where the algorithm is judged, not at the layer where it runs.

---

What does the profile look like when you step back?

It does not look like a uniform shortfall. It does not look like a smooth curve that might rise toward human-level with scale. It looks like a profile with extreme highs and extreme lows — a shape unlike any biological organism's profile.

No biological organism is simultaneously at the frontier of in-distribution pattern recognition and absent from embodied navigation. No biological organism is simultaneously able to retrieve and synthesize explicit knowledge at superhuman scale and unable to participate in stakes-driven cumulative culture. No biological organism scores at ceiling on standardized false-belief tasks and fails on logically equivalent perturbations of those tasks. The profile is not a point on a biological continuum. It is a novel shape, occupying a region of cognitive space that biology had not previously populated.

The reason it is a novel shape is that it was produced by novel selection pressures. Biological cognitive profiles were shaped by the problems of surviving, reproducing, and maintaining social position in a physical world with real costs for failure. The AI cognitive profile was shaped by gradient descent on a training loss, applied to a corpus assembled by biological organisms who had those problems. Indirectly, biological stakes shaped the training data. The model was trained on the output of the stakes. It was not subject to them.

Each definition of intelligence from Chapter 1 produces a different placement for AI. Legg and Hutter's goal-achievement definition: strong goal-achiever in a narrow range of digital, text-structured environments, absent in most physical ones. Sternberg's three-factor account: high analytic, mixed creative, weak practical. Wechsler's purposeful action and effective adaptation: weak, because purposeful action in the biological sense requires purposes, and purposes in the biological sense require stakes. Chollet's skill-acquisition efficiency: much lower than the human child, who arrives at comparable performance from tiny data footprints because the prior built by evolution is extraordinary.

| Definition | What it measures | AI placement | What drives the placement |
|---|---|---|---|
| Legg–Hutter | Goal achievement across environments | Strong in narrow digital, text-structured environments; absent in most physical | Stakes-absent training produces high in-distribution performance, not broad transfer |
| Sternberg | Analytic + creative + practical | High analytic, mixed creative, weak practical | Practical intelligence requires environment-shaping, which a textless agent cannot do |
| Wechsler | Purposeful action and effective adaptation | Weak | Purposes in the biological sense require stakes; the system has none |
| Chollet | Skill-acquisition efficiency given priors | Much lower than the human child | High-data, low-prior; biological priors are the gap |

Each definition produces a different placement. The non-uniqueness of the answer is not a failure of the question. It was always the case. Chapter 1's argument was precisely that there is no single answer because there is no single axis. The AI case makes this visible in a way that the biological comparisons did not, because the AI profile is so extreme in both directions. An organism that is average across all axes doesn't reveal much about the structure of the framework. An organism that is extreme high on some and near-zero on others shows you where the joints are.

A philosophical tradition runs alongside the empirical position this chapter takes, and the reader should know it exists. John Searle's Chinese Room argument (1980) holds that syntactic manipulation of symbols, however successful behaviorally, does not constitute understanding — that a system passing every observable test of intelligence may still lack the thing that makes intelligence intelligence. Roger Penrose's *The Emperor's New Mind* (1989) takes a different route to a related conclusion, arguing from Gödel's incompleteness theorems that mathematical insight is non-algorithmic in principle and therefore cannot be the output of any classical computational system. These are stronger positions than this chapter takes. Both are contested at every step, and this book does not adjudicate them. The Geirhos diagnostic, the Ullman fragility, the embodied-navigation gap, the cumulative-culture gap — these are observations about what current AI systems do and do not do, on the same comparative ground the rest of the book has used. Whether the limits this evidence reveals are permanent in the Searle-Penrose sense, or temporary in the engineering sense, is a question the chapter declines to settle. The lower-bound observation is robust enough to do the chapter's work.

---

The chapter closes with a pair of claims.

The first is about what AI is not. It is not a rung on the biological ladder — not a position on a continuum that runs from bacterium to human and has an obvious place for "very large language model." The biological ladder was built by stakes-driven evolution over 540 million years of multicellular life, with mortality and reproductive failure as the shaping forces at every step. AI was built by gradient descent on a text corpus over decades of computer science, with benchmark performance as the shaping force. These are different ladders. Asking whether AI is above or below the human on the biological ladder is like asking whether a radio is louder or quieter than a concert hall. The comparison has some meaning in narrow dimensions — both produce sound — and fails as a general question because the systems are not the same kind of thing.

The second claim is about what AI is. Every chapter in this book has closed with a brief account of a tool that extends the cognitive capacity the chapter examined. The pH meter extends the capacity to detect chemical gradients that *E. coli* does with membrane receptors. The telescope extends the visual pattern recognition that the hawk does with a fovea containing a million cones per square millimeter. The internet extends the collective memory that the honeybee colony does with a dance floor and a quorum of scouts.

AI is the next entry in that catalog. It extends, with extraordinary power, the human capacities for pattern recognition, knowledge retrieval, and language production — far beyond the biological ceiling in speed, scale, and breadth. It does not replace the capacities. It does not subsume the framework. It is an instrument through which the biological cognitive architecture that evolution built — the one that has stakes, and a body, and a lineage — does more than it could do unaided.

What the instrument is good for, and where the user of the instrument has to remain in the loop, is what the next chapter is about.
