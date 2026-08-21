# Chapter 9 — Simulation and Planning: The Rat That Regretted

*A brain that can run the world backward is already planning forward.*

In David Redish's laboratory at the University of Minnesota, a rat is running a circular track called Restaurant Row. Four stations are arranged around the track, each offering a different food flavor. At each station entrance, a chime indicates how long the rat must wait for a reward. The waits range from one second to forty-five. The rat has one hour and must decide, constantly: stay and collect, or skip to the next station.

The rats develop preferences. Each has a threshold — the longest wait it will accept for each flavor. In 2014, Adam Steiner and Redish arranged the track so they could observe what happened when a rat made a costly mistake: skipped a chocolate offer at a wait within its threshold, then arrived at the next station to find a cherry deal at a wait *above* its cherry threshold. A good deal declined, a bad one accepted instead.

The rat looked back.

It turned its head toward the restaurant it had just left. The look-back occurred only when the rat had passed up a genuinely good offer for a genuinely worse one. While the rat looked back, neurons in the orbitofrontal cortex were firing in the pattern they had previously fired *while the rat was at the chocolate station*. The brain was not encoding the disappointing cherry. It was encoding what the rat should have done a few seconds ago. After the look-back, the rats waited longer at subsequent stations than usual — exactly the behavioral correction that regret produces in human subjects.

A small mammal had just run a counterfactual. It had simulated the alternative it had not taken, compared it to what actually happened, and updated its policy accordingly.

---

To understand what the rat was doing, you need to understand two fundamentally different ways a brain can learn from experience. They are not alternatives — real animals use both — but they are computationally distinct in a way that matters.

Consider a rat in a box with a lever. It presses the lever by accident. A food pellet drops. It presses again. Another pellet. The rat presses many times. The value of pressing the lever has been cached: lever press → reward. This is one way to learn — storing what paid off in the past and retrieving it when the same situation arises. Call it model-free learning.

Now the experimenter, without the rat's knowledge, poisons the food pellets. The rat presses the lever. Eats a pellet. Gets sick. One circuit updates: food pellets are now aversive. But the lever-press value was cached separately. When the rat is hungry again, it presses the lever. It has to experience the bad outcome again before the cache updates. Bernard Balleine and Anthony Dickinson documented this failure mode cleanly in the 1990s with their devaluation paradigm. The model-free agent does not know that lever-pressing leads to the now-aversive food; it only knows that lever-pressing has historically been rewarded.

A different kind of agent would not make this mistake. It maintains a model: lever-pressing leads to food pellets, food pellets are currently aversive. It can chain those representations without pressing the lever, compute the expected outcome, and decide not to bother. This is model-based learning, and it is qualitatively different from the first kind. The model-free agent retrieves a cached value. The model-based agent simulates — it runs a mental rehearsal of what would happen before committing to an action.

| | Model-free | Model-based |
|---|---|---|
| What is stored | Cached action values | World-model + reward function |
| How decisions are made | Lookup of cached value | Forward simulation through the model |
| Speed at decision time | Fast | Slow |
| Cost of environmental change | High — old cache is wrong | Low — re-simulate |
| Failure mode | Habit, devaluation-insensitive | Compute cost; model errors propagate |
| Neural substrate | Dorsolateral striatum | Dorsomedial striatum + prefrontal cortex; hippocampus for spatial models |

Judea Pearl's framework for causal reasoning describes three levels of what a system can ask about the world. The first is association: A and B co-occur. The rooster crows at sunrise. The lever produces food. Pure habituation and classical conditioning operate here. The model-free cache is this level applied to action values — this state-action pair has historically paid off, retrieve when hungry. The second level is intervention: what happens if I do X? The model-free system answers this by lookup, retrieving the cached value acquired from past experience. The model-based system goes further. The third level — the one the rat at Restaurant Row reached — is counterfactual: what would have happened if I had done otherwise? This requires holding two possible world-states in memory simultaneously, the actual and the counterfactual, and computing the difference. No amount of caching can produce this. It requires a world-model and the ability to run it.

These two modes are not redundant. They trade off against each other in ways that determine which dominates at any moment. Model-free is fast — cached values are retrieved in milliseconds and drive action without deliberation. Model-based is flexible — simulation can evaluate novel situations and adapt to environmental changes — but it requires time and working memory. Under stress or time pressure, the model-free system tends to take over. This is why practiced skills become automatic: not because the model-based system breaks down, but because the model-free cache has accumulated enough to produce correct behavior faster than deliberation can. The pathology of addiction is partly the model-free system overcaching a substance value that the model-based system knows is net negative — with the lookup winning under the drug cue because it is faster.

---

In 1948, Edward Tolman published a paper in the *Psychological Review* describing something he had noticed watching rats at T-junctions. A rat approaches a junction, pauses, and swings its head left, then right, then left again. It looks as if it is weighing its options. Tolman called this *vicarious trial and error* and argued the rat was trying out the alternatives in its head before committing. His behaviorist colleagues were skeptical — VTE could be an indecisive head-swing with no cognitive content. The claim could not be adjudicated with 1948 neurophysiology.

Sixty years later, the electrodes were fine enough to settle it.

The hippocampus — the seat of the spatial map — turns out to be a trajectory generator. The same place cells that fire when the rat is in a particular location also fire, in rapid sequence, when the rat is not moving, during brief high-frequency oscillations called sharp-wave ripples in the CA1 and CA3 subfields.

Brad Pfeiffer and David Foster, recording simultaneously from many hippocampal place cells in 2013, captured the forward version of this. Just before a rat began moving toward a remembered goal location, a brief sweep of place-cell firing — starting at the rat's current position and ending at the goal, traversing the path in between — occurred in roughly a hundred milliseconds. Far faster than the rat could physically run the path. The sweep predicted which route the rat subsequently took. Sometimes it predicted the route better than the rat's prior behavior would have suggested, as if the simulation had evaluated options and selected the better one. The hippocampus was pre-experiencing the trajectory before the body took a single step.

This is forward replay. The hippocampal map runs a fast simulation of a candidate future path, on the same neural substrate that encodes the real path when the rat is actually moving.

Foster and Matthew Wilson, working with earlier data, had documented the complementary phenomenon: after a rat ran a trajectory and arrived at reward, the hippocampal place cells fired in reverse order — from the reward location backward through the path just taken. Reverse replay also occurs during sharp-wave ripples, immediately post-reward. Its function is credit assignment: propagating the reward signal backward through the trajectory so that each step that contributed to reaching the reward gets its value updated. In the language of temporal-difference learning, forward replay computes the value of states the animal is about to enter; reverse replay propagates the reward signal backward through the chain of states that produced the outcome.

![Hippocampal replay — forward (planning) and reverse (credit).](../images/09-simulation-and-planning-fig-01.png)

*Figure 1 — Hippocampal replay — forward (planning) and reverse (credit).*

Together, the two forms of replay give the hippocampus its role as a planning substrate. Forward replay evaluates candidate futures. Reverse replay assigns credit to past choices. The animal can sit still and do the mental work of navigation — evaluating paths, updating values — at twenty or thirty times the speed of physical experience, in the gaps between actual movement.

Tolman's vicarious trial and error is, on this account, the behavioral surface of hippocampal forward replay. When the replay sweep runs down one candidate arm and then the other, the rat's head follows the simulated trajectory, turning toward each option as the simulation visits it. What looked like hesitation was the rat's body partially executing the trajectories that the hippocampus was projecting forward.

The events are also *prioritized*: not every past trajectory is replayed with equal frequency. Trajectories toward high-reward locations, novel routes, and recently visited places are replayed more often. The system allocates its simulation budget to the experiences most useful for current decisions. Replay also occurs during sleep, particularly slow-wave sleep, when sharp-wave-ripple events compress entire behavioral sessions into rapid neural sequences — the nightly archive of the day's simulations.

---

Return now to the rat looking back at the chocolate station. The Steiner-Redish result is philosophically significant because it exploits a precise cognitive distinction that is usually obscured in everyday language.

*Disappointment* is a generic worse-than-expected signal. The outcome was below what the prediction said it would be. It is a pure prediction error. Disappointment does not require any representation of an alternative action. It requires only a representation of expectation and outcome.

*Regret* is more specific. The outcome is worse not because it fell below prediction but because a *better option was available and not taken*. Regret requires the agent to represent the counterfactual — the option it could have taken — and compare its value to the actual outcome. Without the counterfactual representation, there is no regret. There is only disappointment.

Steiner and Redish designed their analysis to separate these two signals. The critical comparison was between two types of bad outcome. In the first type, the rat skips a bad chocolate offer — long wait, above threshold — and finds a bad cherry offer — long wait, above threshold. Outcome is below expectation, but no better option was passed up. This is disappointment. In the second type, the rat skips a *good* chocolate offer — short wait, within threshold, a deal it should have taken — and finds a bad cherry offer. A better option was available and missed. This is regret-eligible.

| | Type 1 (disappointment) | Type 2 (regret-eligible) |
|---|---|---|
| Offer skipped | Bad (rat correctly skipped a low-value option) | Good (rat skipped a high-value option) |
| Offer encountered next | Bad (also low-value) | Bad (and now committed to it) |
| Prediction error present | Yes | Yes |
| Look-back behavior | Absent | Present — rat orients backward toward the skipped offer |
| OFC neurons encoding the missed option | Absent | Present |
| Subsequent behavioral correction | Absent | Present — rat takes the next good offer that arises |

The look-back behavior appeared only in the second type of trial. The orbitofrontal neurons representing the missed chocolate option fired only in the second type. The subsequent behavioral correction appeared only after the second type. Both conditions had similar reward prediction errors — both outcomes were below expectation — but only the regret-eligible condition produced the look-back, the counterfactual neural encoding, and the behavioral update.

This is not metaphorically similar to counterfactual reasoning. It is structurally identical: represent the alternative action, evaluate it against the actual outcome, update policy accordingly. The rat was on Pearl's third rung. The OFC neurons were the evidence.

Pearl himself, writing about precisely this class of operation in *The Book of Why*, names regret and credit "the currency of a causal mind" — concepts that, in his words, "require us to compare what did happen with what would have happened under some alternative hypothesis." Pearl built the framework for the human case, with an eye on what AI would have to mechanize before it could be said to reason causally. The Restaurant Row result extends the claim downward: the operation is not waiting for human language or human prefrontal volume. It is already running, in a small mammal, in a circuit of a few thousand cells.

The same paradigm logic has been applied in macaques. Neurons in macaque orbitofrontal cortex dissociate regret-eligible from disappointment conditions in the same way — the OFC represents the missed better option during regret-eligible outcomes, not just during any below-expectation outcome. The capacity scales with prefrontal elaboration, with the representation becoming richer and more sustained in primates. But it starts in the rat.

---

Now consider a bird.

The western scrub-jay is a corvid — a member of the crow family — and it earns its living partly by caching food and recovering it later. The caching lifestyle places specific demands on memory and planning: to survive, the bird must remember what it cached, where, and when, so it can prioritize the perishable items before the shelf-stable ones.

Nicola Clayton and Anthony Dickinson's 1998 paper in *Nature* established the episodic-like memory component. Jays were given access to both wax-moth larvae — preferred when fresh, inedible when degraded — and peanuts, which are shelf-stable. After a short delay, jays preferentially recovered the larvae; the fresh ones were still good. After a longer delay, jays shifted to the peanuts; the larvae had degraded. The jays were not simply preferring one food type. They were integrating information about *what* they had cached, *where*, and *when* — and using the integrated memory to make recovery decisions that depended on all three dimensions simultaneously.

The future-planning result followed. Jays given experience that breakfast would be absent in one compartment the next morning cached food there in the evening — more food in the no-breakfast compartment than in the breakfast-available one — *while currently sated*. The caching was motivated by anticipated future hunger, not present hunger. The *Bischof-Köhler hypothesis*, which held that non-human animals cannot plan for motivational states different from their current ones, predicted this would be impossible. The jays demonstrated it was not.

Subsequent work extended this. Jays re-cache food in private after they have been observed caching — they appear to model the knowledge state of potential thieves and act to defeat that knowledge by moving the cache. This is social simulation: the jay is representing what another agent knows about the jay's own past actions, and planning in response to that representation.

Here is what makes the corvid case theoretically important. The jay does not have a mammalian hippocampus in the anatomical sense. It has no six-layered neocortex. What it has, in the telencephalon, is a dorsal pallium with subregions that modern comparative neuroanatomy has mapped onto mammalian cortical areas by connectivity and molecular markers rather than anatomy. The corvid equivalent of the hippocampus — present in birds as a structure critical for spatial and episodic memory — is engaged during caching and recovery in the same way that the mammalian hippocampus is engaged during navigation and replay. The prefrontal-equivalent regions of the corvid brain appear to be required for the future-planning and social-inference aspects of caching behavior.

Two anatomically distinct neural systems. The same computation. Independent evolutionary origins in lineages that diverged more than three hundred million years ago.

![Convergent evolution of mental simulation in mammals and corvids.](../images/09-simulation-and-planning-fig-02.png)

*Figure 2 — Convergent evolution of mental simulation in mammals and corvids.*

This convergence is the most important theoretical result in this chapter. It tells us that simulation is a function, not a structure. The mammalian hippocampus-prefrontal system and the corvid dorsal-pallium-hippocampal-formation-nidopallium reached the same computational solution from different starting materials, because the function is valuable enough to be worth reaching independently. Any nervous system that needs to evaluate options not yet taken, plan for states not yet reached, and learn from alternatives not selected will be driven by those same pressures toward the same solution. The substrate is the variable. The function is the constraint.

---

You should be clear about what simulation adds to intelligence — and what it does not.

An organism that can only learn from physical experience must encounter every relevant situation at full biological cost and risk. It cannot adjust to a poisoned food source until it has been poisoned. It cannot evaluate an untried route until it has run it. The range of environments it can navigate adaptively is constrained by the range of environments it has physically encountered. This is the model-free ceiling.

An organism that can simulate can rehearse situations it has never been in, evaluate options it has not yet tried, and adapt to environmental changes without failing repeatedly first. The range expansion is qualitative: simulating agents can perform adaptive behavior in environments they have never physically experienced. That is what the rat does when it sweeps forward down an arm it has not yet run. That is what the jay does when it caches for a future hunger it does not currently feel. That is what happens when OFC neurons fire with the pattern for the chocolate station the rat is no longer at.

What simulation does not add: the capacity to simulate well outside the domain for which the simulation machinery was built. The corvid simulation capacity has been documented most thoroughly in food caching — the biologically relevant, high-stakes planning context that the species evolved to handle. Whether the same capacity generalizes to arbitrary planning problems is less clear. The mammalian model-based system, implemented in a more anatomically generalized prefrontal-hippocampal network, appears to generalize more broadly. This suggests that the depth and generality of simulation scales with the anatomical generality of the planning network, not just with its presence.

And simulation can miscalibrate in ways that impose costs. Regret is a genuinely useful signal when it is well-calibrated: identifying cases where a better option was available and the policy needs updating is exactly the feedback a model-based learner needs. But the same machinery that makes adaptive counterfactual reasoning possible makes pathological rumination possible. The rat's look-back is brief and produces an immediate behavioral correction; it does not persist. Human regret can persist far beyond the behavioral horizon where the policy update would remain useful, producing rumination that costs time and affect without generating additional policy improvement. The difference lies partly in the prefrontal regulation of when the simulation is terminated.

---

The digital twin — a computational model of a physical system, updated from sensor data and run forward to evaluate candidate interventions — is the external version of the same function. A fast, cheap rehearsal of trajectories the operator has not yet taken, run to inform the choice about to be made. The simulator's reach is wider and its time horizon longer than what any biological brain can hold in working memory. The choice of what to simulate, what the answer means, and what to do with it remains on the human side.

The rat at Restaurant Row and the engineer at the digital-twin console are doing the same thing at different scales, with different tools, constrained by different bottlenecks. The rat's bottleneck is the length and speed of the hippocampal replay sweep. The engineer's bottleneck is the quality of the model and the clarity of the objective. Both are running the world forward in their heads before they act. The rat just does it faster, and with neurons.

The look-back tells us where planning came from. It came from a small mammal on a circular track, feeling the weight of the option it missed, briefly running its brain in a direction its body could not follow.
