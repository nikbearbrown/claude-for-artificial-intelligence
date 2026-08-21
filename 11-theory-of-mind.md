# Chapter 11 — Theory of Mind

*The ape looked at the wrong place. She knew the right place. She looked at the wrong one because the actor was going to the wrong one — and she knew that too.*

---

In a primate research center in Japan, a chimpanzee is sitting in a quiet room. An infrared eye-tracker is watching her eyes. On the screen in front of her, a video is playing.

The video shows a person searching for an object. A few minutes ago — in the video — the person watched the object get hidden in a particular spot. Then the person left the room. While the person was gone, someone moved the object to a different location.

The person is now returning. In a few moments, they will begin to search.

A fraction of a second before the person starts to move, the chimpanzee's eyes shift. They move to a location on the screen.

They move to the place where the object *used to be*. The place where the actor falsely believes it still is. Not the place where it now sits. The place the actor *thinks* it is.

The chimpanzee is anticipating a mistake. She is predicting that the actor will go to the wrong place, based on a belief she knows to be false — and she is doing this before the actor has made any movement she could simply follow.

Christopher Krupenye and colleagues published this result in *Science* in 2016. It was the first time any non-human animal had passed a version of the false-belief task — the test that, since 1983, had served as the gold standard for theory of mind. Forty years of prior experiments had found that great apes could not do this. Eye-tracking showed they could.

The ape looked at the wrong place. The wrong place was the right answer.

---

To understand why this matters, you need to understand the problem it was trying to solve, because the problem is harder than it looks.

The concept of theory of mind entered comparative cognition in 1978, in a paper by David Premack and Guy Woodruff. Their subject was a chimpanzee named Sarah, trained to communicate with plastic symbols. They showed her short films of a person trying to solve problems — reaching for bananas suspended too high, trying to operate a disconnected heater — and gave her photographs showing various solutions. She consistently chose the correct solution photograph. They inferred that Sarah understood the actor's *purpose*.

The philosopher Daniel Dennett read the paper and immediately identified the problem. Sarah might not be attributing anything to the actor at all. She might simply be solving the physical problem in her own head and selecting the correct photograph — with no reference to what the actor believes or wants. To rule this out, Dennett argued, you need a design in which the subject's knowledge of the world *differs* from the actor's knowledge, and the test is whether the subject predicts the actor's behavior based on the actor's false belief rather than on the truth.

Heinz Wimmer and Josef Perner provided the design in 1983. Baron-Cohen, Leslie, and Frith made it canonical in 1985 with the Sally-Anne paradigm.

Sally puts a marble in a basket. Sally leaves the room. Anne moves the marble to a box. Sally returns.

Where will Sally look for her marble?

![The Sally-Anne false-belief task.](../images/11-theory-of-mind-fig-01.png)

*Figure 1 — The Sally-Anne false-belief task.*

Four-year-old neurotypical children answer correctly: the basket, where Sally left it and where Sally *believes* it still is. Three-year-olds answer incorrectly: the box, where the marble actually is. The three-year-old's error is not a memory failure. Ask where the marble is and the three-year-old knows. Ask where Sally will look and the three-year-old says the box — their own accurate knowledge of the marble's location overrides the inference about Sally's belief.

What changes between age three and age four is the capacity to hold a representation of a belief *as a representation* — as a mental state that exists in a mind and that can be wrong about the world. The three-year-old represents the world as it is. The four-year-old can also represent how someone else represents the world, even when that representation is false.

For forty years after Sally-Anne was established, great apes failed every version of it. Across multiple laboratories, multiple species, multiple experimental variations, the apes behaved like three-year-olds. The consensus hardened: great apes could attribute goals and perhaps desires, but not beliefs. They were perspective-takers but not false-belief reasoners.

Krupenye's result broke the consensus. It is worth being precise about how.

---

The difference between 2016 and the previous forty years is not the species. It is the measure.

All previous false-belief tests with non-human animals used behavioral responses: select a photograph, press a button, search in a location. These *explicit* measures require active, controlled, deliberate response. In humans, the explicit false-belief task recruits substantial executive function — particularly the ability to suppress your own accurate knowledge about where the marble is in order to compute what Sally believes. Human children show the anticipatory-looking pattern in *implicit* false-belief tasks — where no response is required and the eye-tracker simply records where attention goes — as early as fifteen months, more than two years before they can pass the explicit version.

What Krupenye found, across chimpanzees, bonobos, and orangutans, was that the anticipatory gaze went to the false-belief location before the actor began to search. The gaze shift happened before any movement occurred that the ape could simply track or imitate. Something in the visual anticipation system was generating a prediction based on the actor's mental state.

The critic's response was immediate. Cecilia Heyes, the Oxford comparative psychologist who has spent decades pushing back on mentalistic interpretations, argued that the apes could be running *submentalizing* — simple learned rules about where objects last appeared in an actor's view, with no representation of belief as a mental state. The apes had extensive experience watching objects get moved; they might have learned a statistical regularity that actors tend to look where they last interacted with an object.

Fumihiro Kano and colleagues answered this directly in their 2019 follow-up in *PNAS*. They pre-exposed different apes to barriers of the type used in the main experiment — opaque for some apes, transparent for others. Later, all apes watched a video in which an actor stood behind a barrier of the same type they had experienced. The apes' anticipatory gaze depended on their *own past experience* with that specific barrier type. Apes who had experienced the barrier as opaque expected the actor to be ignorant of what was on the other side. Apes who had experienced it as transparent expected the actor to have seen through it.

| Pre-exposure condition | What the ape learned | Submentalizing prediction | Perspective-projection prediction | Observed result |
|---|---|---|---|---|
| Opaque-barrier group | Barriers of this type block vision | Actor will not have seen → look at false-belief location | Actor will not have seen → look at false-belief location | Anticipatory gaze to false-belief location |
| Transparent-barrier group | Barriers of this type are see-through | Actor will not have seen (same surface cue) → look at false-belief location | Actor *did* see through → look at true location | Anticipatory gaze to true location — distinguishes the two accounts |

This is not a statistical regularity about objects in actors' views. The apes were *projecting their own perceptual experience* onto the actor — using their knowledge of what that type of barrier permits or blocks to infer what the actor had been able to see. The actor's belief depends on what the actor was able to perceive, and the ape knows something about what that barrier allows one to perceive. This is the core operation of visual perspective-taking elevated to false-belief computation.

The floor of theory of mind has moved. The apes are not doing Sally-Anne explicitly. They are doing something structurally equivalent to it, implicitly, in a prediction system that runs before any deliberate response is made.

---

Theory of mind is actually computing something specific, and a computational frame makes the comparative evidence much clearer.

In ordinary reinforcement learning, an agent is given a reward function and learns a policy that maximizes it. In *inverse reinforcement learning*, the situation reverses. An observer watches another agent behave and infers the reward function that explains the behavior. Pieter Abbeel and Andrew Ng introduced this as a technique for robot learning from human demonstration; the cognitive science literature has been converging on the view that it is a general description of what theory-of-mind systems do.

When you watch someone walk toward the kitchen, you do not just represent their trajectory. You infer that they are hungry (the reward function) and believe food is in the kitchen (the world model). From observed behavior, you back-compute a compact set of latent variables — desires, beliefs, intentions — that explains everything the person is doing and that will, if accurate, predict what they do next in situations you have not yet observed.

This compression is what makes theory of mind useful. Without it, social prediction requires memorizing every behavior sequence every individual has ever produced in every context. With it, a small number of attributed mental states generalize to predictions about infinitely many novel situations. The attributed reward function is the compact model; observed behavior is the data the model is fitted to.

![Inverse reinforcement learning as theory of mind.](../images/11-theory-of-mind-fig-02.png)

*Figure 2 — Inverse reinforcement learning as theory of mind.*

Applied to the hierarchy of capacities in this chapter: goal attribution is inverse reinforcement learning that infers only the target state of the agent's policy. Perspective-taking adds the agent's information state — what it can see. False-belief reasoning adds the possibility that the agent's world model is *wrong*, and uses the agent's false model rather than the true world to predict behavior. Each level requires the observer to hold a richer internal representation of the target agent's mind.

---

The great ape result is compelling for what it shows in a lineage close to our own. The corvid result is compelling for a different reason: it shows the same functional capacity appearing in a brain built on entirely different principles, in a lineage separated from humans by more than 300 million years.

Western scrub jays store food in hundreds of small caches distributed across their territory. They are prodigious thieves — they routinely raid each other's caches, and dominant birds displace subordinates from discovered food. Knowing who has seen what about where food is cached is survival-relevant information.

Nathan Emery and Nicola Clayton, in their 2001 *Nature* paper, gave a jay the opportunity to cache food while another jay watched from a nearby cage. In other trials, the caching jay worked alone. Subsequently, the caching jay was given private access to all the cache sites and could move items freely.

Jays that had been observed during caching moved their caches to new locations. Jays that had cached unobserved did not. The caching jay was responding to whether it had been *seen* — perspective-taking. But the theory-of-mind claim rests on the next observation: the protective re-caching occurred specifically in jays that had themselves been thieves in the past. Naive jays, who had never stolen another bird's cache, did not re-cache even when observed. Only experienced thieves took the protective measure.

The mechanism Emery and Clayton proposed is self-projection: the experienced thief knows what it does when it watches another bird cache — it steals — and it projects this behavioral tendency onto the watching observer. The computation is: *this bird is in the same perceptual position I have been in when I have stolen from others; I know what I do in that position; therefore I know what this bird is likely to do*.

This is not the Sally-Anne false-belief task. It does not require representing a false belief. But it requires something Sally-Anne does not explicitly demand: taking one's own mental states as a *model* for another agent's mental states. The jay is using itself as a theory-of-mind engine, running its own behavioral propensities forward through the lens of the other bird's perspective. It takes a thief, literally and specifically, to know what a thief will do.

Corvids lack a six-layered neocortex. Their executive control runs through the nidopallium caudolaterale — anatomically distinct from mammalian prefrontal cortex, functionally analogous. The same conclusion as the previous chapters: the computation is the constraint. The substrate is not.

---

The dog case is this chapter's most instructive contrast, because it demonstrates how two very different cognitive operations can produce the same surface behavior.

Dog owners reliably report that their dogs produce a "guilty look" when caught having done something forbidden: cowering, flattened ears, averted gaze, tail tucked. The owner interprets this as the dog *knowing it did wrong* — evidence that the dog is attributing to the owner a belief about misbehavior and producing a conciliatory response based on that belief.

Alexandra Horowitz ran the experiment. Owners left their dogs alone with a forbidden treat and returned. Before they returned, Horowitz either told them the truth (the dog had eaten the treat, or had not) or *lied* (the dog had eaten the treat but the owner was told it had not; or the dog had not eaten the treat but the owner was told it had). Owners who were falsely told their dog had misbehaved sometimes scolded the dog before looking at the treat.

The guilty look was not associated with whether the dog had actually eaten the treat. It was associated with whether the owner was scolding. Dogs that had been obedient but were scolded showed as much guilty-look behavior as dogs that had actually misbehaved. Dogs that had misbehaved but whose owners were told they had been obedient showed no guilty look.

| | Owner told *misbehaved* (scolds) | Owner told *obedient* (no scolding) |
|---|---|---|
| Dog actually misbehaved | High guilty-look rate | Low guilty-look rate |
| Dog was obedient | High guilty-look rate | Low guilty-look rate |

What the dog is doing is behavioral pattern recognition on current observable cues: when human = angry display, produce = submission signal. The dog has learned, through years of domestication, to read the signals of human displeasure and produce behavior that defuses it. This is sophisticated. It is not theory of mind.

What theory of mind would require: the dog would need to represent that the owner holds the *belief* that the dog misbehaved, and produce the guilty look in response to that represented belief rather than to the observable scolding. To test this, you would need the dog to show guilty-look behavior when the owner holds a false belief about misbehavior but shows *no behavioral cues* of it — in anticipation of discovery, not in response to expression. The current evidence does not support this.

Dogs are extraordinarily good at reading *current human behavior* — better than great apes in many studies of human communicative cuing. They have been domesticated for fifteen thousand years specifically in contexts where reading human intentions from observable cues was fitness-relevant. There is a difference between tracking observable cues and modeling the beliefs that will produce future behavior. The dog has not clearly demonstrated the second.

---

Now the AI case, which is where the inverse reinforcement learning frame becomes sharpest.

In 2022, Michal Kosinski reported that GPT-3.5 and GPT-4 passed a large battery of standard false-belief tasks — Sally-Anne and variants — with accuracy approaching human adults. The result attracted substantial attention, and speculation followed that large language models had developed theory of mind as an emergent property of scale.

Tomer Ullman answered this in 2023 by making small modifications to the same tasks. Replace the opaque container in the Sally-Anne story with a transparent one, so that Sally could have seen the marble move even when she was present. Add a sentence explicitly granting the actor knowledge of the object's new location. Make changes that preserve the *logical structure* of the false-belief situation while altering the *surface features* of the canonical story.

GPT-4, on the modified versions, continued to predict that Sally would look in the basket — the answer correct for the canonical version — even when the modification made it clear that Sally had seen the marble move and therefore knew where it was. The model was applying the learned template: actor-absent-during-move → actor-has-false-belief. It applied this template even when the story's explicit content contradicted it.

Humans do not do this. A human reading the transparent-container version immediately updates the prediction: Sally saw it happen, so Sally knows. The inference generalizes because humans are running an actual model of Sally's information state — a model that takes the story's *content* as input and outputs a belief-state for Sally by applying the inverse reinforcement learning computation to that content.

The model is doing something, but it is not doing inverse reinforcement learning on Sally's mental states. It is matching the story to training-distribution templates, and the templates break when the stories are modified in ways that preserve logical structure while altering surface form.

| Task version | Logical structure | Surface form matches training distribution? | GPT-4 prediction | Correct prediction |
|---|---|---|---|---|
| Canonical Sally-Anne (opaque container, actor absent) | False-belief at original location | Yes | Original location | Original location ✓ |
| Transparent-container modification (actor present, can see through) | True-belief at new location | No (logical structure changed despite similar wording) | Original location | New location ✗ |
| Explicit-knowledge modification (actor told over phone) | True-belief at new location | No | Original location | New location ✗ |

By the inverse reinforcement learning frame, this is the diagnostic. A system genuinely doing theory of mind should pass Ullman's modifications, because it is computing Sally's information state from the story's content rather than from the story's surface resemblance to training examples. A system pattern-matching on narrative templates should fail the modifications while passing the canonical versions — because the template and the logic only coincide within the canonical form, and the modification is precisely designed to pull them apart.

The 2023 models failed the modifications. This is the chapter's strongest evidence that what LLMs do when they appear to pass theory-of-mind tasks is not the same operation that a great ape performs when it anticipates an actor's false belief. One is building a model of another mind. The other is matching a template.

---

Here is what the chapter has established and what it has not.

The implicit false-belief result in great apes — the Krupenye 2016 anticipatory looking, the Kano 2019 barrier-experience control — is replicable and survives the strongest submentalizing alternative tested so far. Self-projective perspective attribution in corvids — the Emery-Clayton re-caching and its theft-experience dependency — is supported and points to a different implementation of the same function. Both species are doing something that satisfies the logical requirements of false-belief reasoning, using mechanisms not simply explained by associative learning on behavioral regularities.

What is not established: second-order recursive false-belief reasoning in any non-human animal. The line between humans and non-human animals in theory of mind now sits at *explicit, second-order, recursive* mentalizing — not at any form of mental-state attribution per se. The corvid result is self-projective, not explicitly recursive. The great ape results are at the first-order level and implicit.

This boundary matters. By the operational definition of intelligence — the ability to achieve goals across a wide range of environments — theory of mind is valuable across a wide range of its levels. A social environment is navigable with perspective-taking alone. It is navigable better with first-order false-belief attribution. It is navigable best with the recursive structure that allows strategic deception, coalition-building, political maneuvering, and the transmission of cultural knowledge through deliberate teaching. The richer levels produce a qualitatively different range of achievable goals, not just better performance on the same ones.

The common mistake is treating behavioral evidence for perspective-taking as evidence for false-belief reasoning. The subordinate chimpanzee taking food the dominant cannot see is doing perspective-taking. The chimpanzee anticipating that an actor will search in the wrong place is doing false-belief reasoning. The behaviors can look similar from outside. The cognitive operations are distinct, and the experimental designs that test them are different.

And the dog's guilty look is not guilt. It is submission in response to observable scolding cues. Knowing the difference — between tracking observable behavior and modeling the beliefs that will produce future behavior — is the whole content of the implicit/explicit distinction that runs through this chapter.

The ape looked at the wrong place. That gaze carries a great deal of cognition. Forty years of experiments failed to find it not because they were looking in the wrong direction, but because they were looking with the wrong instrument.
