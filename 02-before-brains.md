# Chapter 2 — Before Brains

*The oldest decision on Earth is still running, and it uses no neurons.*

---

In the year 2000, a physicist named Toshiyuki Nakagaki placed a piece of slime mold at the entrance of a plastic maze and set food at the exit. The organism was yellow, roughly the size of a dinner plate. It had no mouth, no eyes, no neurons, no brain. It was a single cell — one continuous, pulsing bag of cytoplasm with millions of nuclei sloshing through a network of self-built tubes.

Within hours, the organism had explored every passage, every dead end, every wrong turn. Then it began to withdraw. Branch by branch, the exploratory tubes thinned and disappeared. When the experiment ended, the slime mold — *Physarum polycephalum* — had concentrated its entire body into a single thick tube tracing the shortest possible path between the food sources.

No plan. No map. No nervous system. Just a cell, and a problem solved.

![Physarum solves a maze in four frames — coverage, then pruning to the shortest path.](../images/02-before-brains-fig-01.png)

*Figure 1 — Physarum solves a maze in four frames — coverage, then pruning to the shortest path.*

A decade later, Atsushi Tero and colleagues repeated a version of the experiment at a continental scale. They placed oat flakes at the geographic positions of the cities surrounding Tokyo and let *Physarum* connect them. The network the mold built matched the actual Tokyo rail system in efficiency, cost, and fault tolerance. Human engineers had spent a century designing that system. The mold reproduced its essential structure in a few days.

![Physarum's network and the actual Tokyo Kanto rail map.](../images/02-before-brains-fig-02.png)

*Figure 2 — Physarum's network and the actual Tokyo Kanto rail map.*

What you make of this depends on what you think intelligence requires. If it requires a brain, then the slime mold is not intelligent — it is merely a physical process that happens to produce optimal solutions, the way a soap film happens to minimize surface area. If intelligence requires only that a system take in information from the world and produce behavior that achieves goals, then the slime mold is doing it, and has been doing it for a billion years.

The question this chapter pursues is more specific than that, and more useful: what is the minimum thing a decision requires?

Not a brain. Not even a nervous system. The first systems that made decisions predate both by billions of years. What does the floor look like — the smallest thing that qualifies as genuine choice rather than mere mechanism? Because if you don't understand the floor, you can't understand what everything built on top of it actually added.

---

A reflex is not a decision. Your knee jerks when the doctor taps it. A Venus flytrap snaps when its trigger hairs are touched. These are physical mechanisms: input in, output out, fixed. The input determines the output every single time, regardless of history. There is no comparison happening. There is no past being weighed against a present.

A decision varies. The same stimulus can produce different responses depending on what has happened before. That is the distinction that matters. And it turns out that making a real decision — not a metaphorical one — requires exactly four things.

First: sensing. Some access to the world. Without it, there is nothing to decide about.

Second: memory. The ability to compare now to a moment ago. This is more important than it sounds. A system that only knows the present cannot detect whether things are getting better or worse. It is frozen at a single instant, like a photograph. Memory is what turns a snapshot into a movie — and only a movie tells you which direction you're traveling.

Third: integration. The ability to weigh multiple signals together over time. Not just "what is the concentration of sugar right now," but "what has been happening to the concentration of sugar over the last few seconds, and what does that trend mean?"

Fourth: variable response. The output has to be able to change. A system that always does the same thing regardless of input is not deciding — it is executing. Variation is what allows decisions to be adaptive.

| Ingredient | What it provides | What is missing without it | Biological example in this chapter |
|---|---|---|---|
| Sensing | Detection of relevant environmental signal | The agent cannot tell what state it is in | *E. coli* membrane chemoreceptors; Venus flytrap trigger hairs |
| Memory | A trace of recent state for comparison | The agent cannot detect change over time | CheR/CheB methylation trace; cytoplasmic flow patterns in *Physarum* |
| Integration | Combination of present and remembered state | The agent cannot decide; it can only react | *Physarum* network self-pruning; flytrap calcium summation |
| Variable response | Output that differs as a function of integration | The agent's behavior is fixed and signal-independent | Run-vs-tumble switching; trap closure thresholding |

What these four ingredients collectively compute is what I want to call **valence** — borrowed from chemistry, where it describes combining power. Valence here means the approach-or-avoid property of a stimulus. Food has positive valence. Toxin has negative valence. Valence is not a judgment. It may or may not involve feeling. It is simply a categorization that allows behavior: move toward this, move away from that.

Without valence, no preference is possible. Without preference, no goal. The whole story of cognition, from bacteria to human beings, is the story of making valence faster, richer, more flexible, and more accurate. It starts here.

---

Now the precise story, because precision is where understanding lives.

Imagine you are an *E. coli* bacterium. You are one cell. You are swimming in a chemical soup that contains amino acids — food — and copper ions, which will kill you. You cannot steer. You have no rudder, no fins. What you have is a flagellar motor at your tail, and the motor can spin two ways: counterclockwise, which gives you a smooth forward run; clockwise, which causes your filaments to fly apart and tumble you in a random new direction. Your behavior is this: run, tumble, run, tumble. A drunkard's walk.

But the drunkard is not stumbling randomly. When Howard Berg built a microscope in 1972 that could track a single bacterium through three-dimensional space, he watched this pattern for hours and noticed something remarkable. The run segments were longer when the cell was moving toward food. The tumbles were more frequent when things were going badly. The drunk was finding its way to the bar.

The mechanism starts at the cell surface. The membrane is studded with receptor proteins called methyl-accepting chemotaxis proteins — MCPs. Each MCP is tuned to a chemical class. When an attractant binds, the receptor changes shape — not dramatically, but a subtle conformational shift that propagates into the cell. This inhibits a kinase called CheA. A kinase's job is to phosphorylate a target — to attach a phosphate group to it. CheA's target is a small messenger protein, CheY. Phosphorylated CheY diffuses to the flagellar motors and pushes them toward clockwise rotation. Clockwise means tumble.

So: more attractant → receptor activated → CheA inhibited → less CheY-P → less tumbling → longer runs. That part is clean.

![E. coli chemotaxis — fast signaling and slow methylation memory.](../images/02-before-brains-fig-03.png)

*Figure 3 — E. coli chemotaxis — fast signaling and slow methylation memory.*

But this mechanism, elegant as it is, only responds to *current* concentration. A cell that simply reads current concentration would tumble just as readily sitting in the middle of a rich food patch as at its edge, because the absolute level is high in both places. It would have no way of knowing it is surrounded by food rather than approaching it. It would lose all directional information.

The memory is in two more enzymes: CheR and CheB.

CheR adds methyl groups to the MCP receptors. CheB removes them. The crucial point: methylation changes the receptor's sensitivity — more methylated means less sensitive to attractant. And these enzymes operate on a *slower* timescale than the binding cascade. The effect is that the receptor's current sensitivity is a record of the recent average. It has been slowly tuned to whatever the cell has been experiencing for the past several seconds. When the current concentration exceeds that baseline — when things are getting better — net CheA inhibition is high and the cell runs. When current concentration falls below baseline — when things are getting worse — CheA fires, CheY-P rises, and the cell tumbles.

In 1986, Segall, Block, and Berg measured the precise time window by pulsing bacteria with attractant. The cell weighs its chemical experience over the past four seconds, with the most recent second weighted positively and the prior three seconds weighted negatively. The cell is computing a derivative. It is responding to the *change* in concentration over time, not the level. It is doing differential calculus with two enzymes and a methylation rate.

![E. coli temporal weighting — the cell computes a difference, not a level.](../images/02-before-brains-fig-04.png)

*Figure 4 — E. coli temporal weighting — the cell computes a difference, not a level.*

The four-second window is not arbitrary. It is matched to the distance the cell can swim in a single run before Brownian motion randomizes its direction. Memory longer than that would be memory of a self that no longer exists — the cell would be comparing its current position to a position it can no longer point back to. The window is adapted to the physics of the organism's world.

This is what makes it a decision rather than a reflex. The reflex responds to a level. The decision responds to a trend. The reflex cannot tell which way things are going. The decision can.

---

To see why the memory is doing all the work, consider what happens when you remove it.

Knock out CheR and CheB — eliminate the methylation enzymes — and the cell is still alive, still swimming, still capable of responding to attractant. The CheA-CheY-P cascade still functions. Put this mutant in a gradient and it will still bias its flagella when it encounters high concentration. The absolute-level response works.

But the mutant cannot navigate. Its random walk stays random. It runs longer in rich zones, but it cannot detect whether things are improving, so it does not preferentially run *toward* the source. The drunkard in the rich zone is now just a drunkard who doesn't want to leave — not a navigator.

The cell without methylation memory has three of the four ingredients. It senses. It integrates, in a limited way. It responds variably. But it has no memory — no comparison of present to past — and without that comparison, directed behavior is impossible. This is not a soft claim. It is what the knock-out experiments show. The memory is not a refinement; it is the hinge on which cognition turns.

---

*Physarum polycephalum* — the slime mold — runs the same four-ingredient computation through a body that is a network of cytoplasmic tubes rather than a single swimming cell. The logic is architectural instead of molecular. Cytoplasm sloshes back and forth through the tubes in rhythmic oscillations. The rule is simple: tubes carrying high, sustained flow grow thicker; tubes carrying low flow thin and eventually disappear. When food is detected at a network node, local oscillations shift phase, flow toward the food increases, that channel is reinforced, and the network reorganizes.

The maze-solving follows directly. Every route is explored — the mold fills the maze. Dead-end branches carry zero net flow, because there is no food at the end of them. Dead-end tubes thin and retract. The shortest path carries the most sustained flow, because it connects the two food sources with the least detour. The shortest path is the last tube standing. No planning, no map — just the physical dynamics of flow and reinforcement.

The memory is different from the bacterium's. *Physarum* leaves a trail of extracellular slime where it has been, and avoids this trail on subsequent exploration. The memory is not molecular; it is written into the environment. This is a very old trick that turns out to be universal: encode past behavior in a physical mark that future behavior can read. Ants do it with pheromones. Humans do it with cities.

| Organism | Memory substrate | Timescale | What is encoded | Internal or external |
|---|---|---|---|---|
| *E. coli* | Methylation of chemoreceptors (CheR/CheB) | ~1 second | Recent attractant concentration | Internal (cytoplasmic) |
| *Physarum* | Cytoplasmic flow channels + extracellular slime | Minutes to hours | Where the organism has already explored | Both (channels internal, slime external) |
| Venus flytrap | Cytoplasmic calcium concentration | ~20 seconds | Recent count of trigger-hair stimulations | Internal |

What these two organisms share is not just the outcome — they both solve navigation problems — but the logical structure underneath. The bacterium runs its memory in methylation reactions on membrane proteins. The slime mold runs its memory in cytoplasmic flow dynamics and extracellular slime. The computation is identical: sense, remember, integrate, respond variably. The substrate is totally different. This is a pattern you will encounter throughout this book. Cognitive functions are substrate-independent. The brain is not running unique computations. It is running the same ancient computations faster and with more parameters.

---

The Venus flytrap, *Dionaea muscipula*, has solved a specific problem: it needs to close on insects without closing on rain. The solution is a counting rule — the trap fires only when at least two trigger hairs are touched within approximately thirty seconds. Jennifer Böhm, Sönke Scherzer, and Rainer Hedrich traced the mechanism to calcium signaling.

Each touch generates a calcium spike in the trap's cells. Calcium decays over time — the concentration drops back toward baseline as calcium pumps remove it. But it does not drop completely before the window closes. A second touch adds its spike to whatever residue remains from the first. Only when the summed calcium crosses the threshold does the trap close.

![Venus flytrap — leaky calcium integrator counts trigger touches.](../images/02-before-brains-fig-05.png)

*Figure 5 — Venus flytrap — leaky calcium integrator counts trigger touches.*

The calcium concentration *is* the short-term memory. The threshold *is* the decision rule. The trap counts to two by exploiting the fact that calcium decays slower than the interval between legitimate prey movements. This kind of mechanism — a signal that accumulates with each event and leaks away between events — is called a leaky integrator. It appears throughout neuroscience, where it describes how some neurons accumulate evidence before firing a decision. The flytrap is doing the same thing, in ionic calcium, with no neurons.

The integration window is calibrated, just like the bacterium's four-second memory, to the temporal statistics of the signal it needs to detect. Insects move with irregular, rapid perturbations — two touches in thirty seconds is characteristic of struggling prey. Rain arrives in a more regular pattern but rarely produces two contacts on the same trigger hair within the window. The physics of the problem determines the memory window. The right timescale for memory is always the one that matches the structure of the signal you need to read.

---

The frontier of this literature includes claims that need more scrutiny than enthusiasm.

Two of the most widely cited demonstrations of plant cognition have not held up cleanly. Monica Gagliano's 2014 study reported that *Mimosa pudica* — the sensitive plant — habituated to repeated drops and retained the habit for a month. Robert Biegler argued the data could be explained by sensory adaptation or motor fatigue. The dispute was not resolved by independent replication.

Gagliano's 2016 study claiming that pea plants learned to associate the direction of a fan with the direction of a light — classical conditioning — failed to replicate under blinded experimental conditions. Kasey Markel repeated the protocol with improved controls and found no effect.

The responsible position is this: habituation is clearly demonstrated in *Physarum*, and is not yet clearly demonstrated in plants. The flytrap's calcium counting is a real mechanism. The rest requires more work before it can be asserted.

The pattern of overreach in this literature is instructive. There is always a careful claim — the organism produces a behavior characteristic of X — and an inflated one: the organism *experiences* X the way we do. The careful claim is often supported. The inflated one is almost never established, and stating it as fact is not scientific courage. It is a failure to distinguish evidence from enthusiasm.

| Claim | Organism | Study | Status | What the evidence actually shows |
|---|---|---|---|---|
| Maze-shortest-path solving | *Physarum polycephalum* | Nakagaki 2000 (*Nature*) | Established | Reproducible across labs; mechanism (network pruning by flow optimization) understood. |
| Habituation to mechanical stimulation | *Physarum* | Boisseau et al. 2016 | Established | Habituation to bromide solution shows both stimulus-specific and dishabituation behavior. |
| Habituation in *Mimosa pudica* | *Mimosa pudica* | Gagliano 2014 | Established | Repeated drops produce reduced leaf-folding, persistent across days. |
| Pavlovian-style associative learning in pea | *Pisum sativum* | Gagliano 2016 | Contested | Original result has not cleanly replicated; methodological objections about light-cue confounds remain unresolved. |
| Calcium-counting of trigger-hair touches | Venus flytrap (*Dionaea*) | Hedrich lab 2016 onward | Established | Two-touch threshold mechanism mapped to specific calcium signaling and gene expression. |

---

In 1906, the chemist Søren Sørensen needed to measure the acidity of his fermentation vats. He dipped litmus paper, watched it change color, and compared it to a reference card. This was a one-point valence measurement: this batch is *okay* or *too acidic*, approach or adjust. It told him nothing about whether acidity was changing, nothing about the trend, nothing that the bacterium's temporal integration would have revealed.

The modern pH electrode does better. It converts hydrogen ion concentration into a continuous voltage. Still no trend. Still no comparison to the recent past. Still, in the four-ingredient framework, a sensor without a decision.

The instruments humans have built to detect the chemistry of the world — pH meters, smoke detectors, blood-glucose monitors, explosives-detection systems — are all artificial MCPs. They implement the sensing step. Some add a threshold rule. A few add something like integration: environmental monitoring systems that flag trends in pollutant concentration rather than instantaneous readings. None of them, as of this writing, implement the full four-ingredient architecture in a way that produces flexible, goal-directed behavior across varying environments.

| Device | Sensing | Memory | Integration | Variable response |
|---|---|---|---|---|
| Litmus paper | Yes | No | No | No (single readout) |
| pH electrode | Yes | No | No | No |
| Smoke detector | Yes | No | Yes (threshold) | Yes (alarm above threshold) |
| Blood-glucose monitor | Yes | Yes (logged history) | Partial (trend display) | No (reports, does not act) |
| Environmental trend monitor | Yes | Yes | Yes | No (no agent that acts on the integration) |

The smoke detector on your ceiling is not stupid. It is an excellent one-step sensor with a reliable threshold rule, and it saves lives. But it would tumble randomly in a chemical gradient. It cannot find the shortest path through a maze. It cannot distinguish cooking smoke from structural fire in a useful way — which is why it goes off when you make toast. It does not have the memory that makes those distinctions possible.

The step that turns a sensor into a decision-maker is the derivative: not "what is the level of X" but "how is the level of X changing relative to recent experience." Most instruments still stop one step short. The bacterium took that step two billion years ago, with two enzymes, in a picogram of cytoplasm. Understanding why that step is hard to replicate in silicon is not a small problem. It is, in various forms, one of the central problems of artificial intelligence.

---

There is a cognitive floor — a minimum viable architecture for what counts as decision-making — and it appears in systems with no neurons, no brains, and no nervous systems of any kind. That floor consists of four components: sensing, memory, integration, and variable response. Together, they compute valence: the assignment of approach-or-avoid to stimuli. Take any component away and you have something simpler than a decision. Keep all four, organized into a loop that closes on the world, and you have the oldest cognitive system biology has produced.

The bacterium's memory is molecular — methylation states on membrane proteins, encoding the last four seconds of chemical experience as a running average. The slime mold's memory is architectural and environmental — flow dynamics and slime trails encoding a history of where the body has been. The flytrap's memory is ionic — calcium residues from the last touch, decaying on a thirty-second timescale tuned to insect movement. Three completely different substrates. One logical structure.

What neurons will add — beginning in the next chapter with *C. elegans* — is speed, flexibility, and range. A nervous system allows different components to specialize, allows internal state to modulate response, allows the same sensory input to mean different things depending on context. These are genuine advances. But they are advances along the same dimension.

The common mistake is to assume that a capacity first clearly visible in complex organisms must have *originated* in complex organisms. It never does. The prototype is always older, simpler, and stranger than you expect. Search for the floor. That is where you find out what the thing actually is.
