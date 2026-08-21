# Chapter 6 — Pattern Recognition and Perception: The Fish That Picked a Face Out of Forty-Four

*The architecture that recognizes your face is five hundred million years old and fits in a pea.*

The archerfish does not have a face area.

It has no neocortex — that six-layered sheet of tissue mammalian neuroscientists sometimes call the seat of intelligence. It has a brain the size of a pea, organized around a three-layered structure hundreds of millions of years old. It spends its days hovering just below the water surface, watching the overhanging vegetation for insects, calculating the refraction of light through the water-air boundary, and spitting a precision jet to knock its targets down.

In 2016, researchers at the University of Queensland put two photographs of human faces above a tank of archerfish. One face was paired with a reward. The other was not. The fish learned which face meant food. Then the experiment got harder. The trained face was placed in a lineup of forty-four photographs — the familiar face plus forty-three faces the fish had never seen. Which would it spit at?

It spat at the right face. Eighty-one percent of the time. The experimenters controlled for color, brightness, and head shape — none of those simpler cues explained the performance. The archerfish was picking a specific human face out of a crowd of human faces, using machinery that evolution assembled before the first dinosaur walked the earth.

The surprise here is not that the fish is clever. The surprise is that we ever thought face recognition required anything the fish does not have. The architecture that does it is not a special innovation of primates, or of mammals, or even of vertebrates with a neocortex. It is the foundational vertebrate solution to a computational problem that appeared the moment the first animal with eyes had to tell apart objects in a visual world. The fish has been solving it for five hundred million years. This chapter is about how.

---

Before any architecture can be examined, the problem it solves needs to be stated precisely, because the central tension of perception is not obvious.

Any perceptual system that acts intelligently in the world has to do two things that pull against each other.

The first is discrimination. Two stimuli that are similar but different must be kept distinct. The predator and the harmless decoy have similar silhouettes — but treating them as identical will get you killed. The toxic berry and the edible one look nearly the same. A perceptual system that cannot discriminate similar inputs cannot act appropriately.

The second is generalization. A stimulus encountered in a new form must be recognized as the same kind of thing encountered before. The predator from above and the predator from below cast different silhouettes onto the retina. The face in dim light has different luminance values from the face in bright light. A perceptual system that cannot generalize across these variations cannot recognize anything it has not seen in exactly that form before.

These two requirements are in tension because they demand opposite operations on the input. Discrimination needs representations that are *far apart* for similar inputs — so a small difference in what arrives produces a large difference in how it is represented, keeping the two stimuli distinct. Generalization needs representations that are *close together* for different instances of the same category — so the predator from above and the predator from below produce similar representations that lead to the same behavioral response.

![Discrimination–generalization tension in representational space.](../images/06-pattern-recognition-and-perception-fig-01.png)

*Figure 1 — Discrimination–generalization tension in representational space.*

There is a third problem that compounds both, and it is the hardest: *invariance*. Not just discrimination and generalization across instances, but recognition that is stable across changes in viewpoint, scale, rotation, illumination, and partial occlusion. The frog is the frog whether you see it from above, from the side, or upside down. A face is a face at forty-four different angles and under every demographic variation. A system without invariance recognizes only what it has already seen, in the form it has already seen it.

The vertebrate cortex solves all three simultaneously. The same neurons, the same architecture, the same circuit. And it has done this for at least five hundred million years, which is the strongest possible evidence that the solution is not one design choice among many. It is the solution.

---

The vertebrate pallium — the cortex's evolutionary ancestor — has a conserved architecture that makes everything else in this chapter possible.

In 2017, Shreyas Suryanarayana and colleagues at the Karolinska Institute published a careful comparison of the lamprey pallium to the mammalian cortex. The lamprey split from the rest of the vertebrate lineage approximately five hundred million years ago. It has no jaw, no paired appendages, no bones — about as primitive a vertebrate as anything still alive. And its lateral pallium, examined at the level of cellular types, projection patterns, and molecular markers, shows a three-layered structure with glutamatergic projection neurons in an outer layer, a mixed inner layer, and a plexiform zone where incoming inputs meet dendrites — closely matching the organization of ancient cortical regions in reptiles and mammals.

The lamprey pallium receives input from the olfactory bulb with the same topology as the mammalian piriform cortex. It projects to the deeper brain structures that drive behavioral output via the same basic route. The blueprint, in the relevant architectural sense, has been preserved across half a billion years of vertebrate evolution.

![Three-layer pallial blueprint across vertebrate phylogeny.](../images/06-pattern-recognition-and-perception-fig-02.png)

*Figure 2 — Three-layer pallial blueprint across vertebrate phylogeny.*

What the blueprint specifies is a sheet of excitatory neurons — the pyramidal cells — embedded in a mesh of inhibitory interneurons. Inputs arrive from the senses. Outputs leave toward motor structures. And crucially: the neurons are connected to each other by horizontal *recurrent collaterals* — axons that travel sideways through the cortical sheet and synapse on neighboring excitatory cells. The inhibitory interneurons perform *lateral inhibition* — they suppress activity in neurons that are not the most strongly driven by the current input.

Excitatory projection cells. Inhibitory interneurons. Recurrent excitatory connections among the projection cells. These three elements, and their interaction, are the entire story. Let me build it up carefully.

---

The clearest way to see how the cortex solves discrimination and generalization simultaneously is through the olfactory system, because the olfactory version of the problem is the oldest and most transparent. Most of the vertebrate pallium's deep history is olfactory; vision arrived later and was plugged into hardware originally designed for smell.

A fish has several hundred olfactory receptor types in its epithelium. Each receptor responds to a broad range of odorant molecules with varying affinity; each odorant activates a broad range of receptor types at varying intensities. The signal arriving at the cortex is a high-dimensional pattern of activity across hundreds of receptor channels simultaneously — a combinatorial code whose potential diversity, across only a few hundred receptor types, runs into the trillions of distinguishable patterns. The task: identify which patterns belong to known categories, generalize across slight variations within a category, and discriminate between categories even when the input patterns overlap.

Here is how three operations built from those three circuit elements accomplish this.

**The first operation is dimensionality expansion.** Fibers from the olfactory bulb project diffusely onto the pyramidal neurons of the lateral pallium. Each bulb fiber connects to many cortical neurons; each cortical neuron receives inputs from many bulb fibers. The effect is that the high-dimensional input representation at the bulb is projected onto an *even higher-dimensional* representation at the cortex. The cortex has more cells available to represent the signal than the input pathway had channels to carry it.

This matters for the following reason. When you project a set of points into a higher-dimensional space, points that were close together in the original space tend to spread apart. Two odors that produced similar patterns across the receptor array — close together in input space — become less similar in the cortical representation, simply because the expanded dimensionality provides more room for representations to diverge. The cortex does not need to be clever about separating similar inputs. The expansion does it geometrically. This is the mathematical insight underlying the kernel trick in support vector machines and the cover theorem in information theory. The brain had it first.

**The second operation is sparse coding through lateral inhibition.** The expanded representation is not just large — it is *sparse*. Of all the cortical neurons potentially responsive to a given odor, only a small fraction actually fire. The rest are held silent by the inhibitory interneurons, which receive input from the active excitatory neurons and broadly suppress the less-strongly driven ones, enforcing a winner-take-most competition.

The sparseness is essential for discrimination. Two odors that produced overlapping sets of active neurons at the input tend to activate *different* sets of sparse cortical neurons after the competition. The inhibitory contest amplifies small differences into large ones. Two odors with twenty percent input overlap might produce cortical representations with only one percent overlap, because the competition forces divergence. What was similar becomes distinct.

**The third operation is recurrent auto-associative completion.** This is the one that handles generalization, and it is the most remarkable.

The pyramidal neurons in the piriform cortex are connected to each other via the horizontal recurrent collaterals. These connections are modifiable by Hebbian plasticity — neurons that fire together strengthen their connections to each other. When a particular odor is experienced, the set of cortical neurons that fire together strengthen their connections. This happens gradually, across many exposures.

After those connections have been strengthened, something changes about how the cortex processes that odor. If a subsequent presentation is partial — the concentration is lower, the wind has blown away some of the volatile compounds, the odor is partially masked — the incoming signal activates some of the learned ensemble but not all. The activated neurons fire. Those firing neurons are strongly connected to the other members of the learned ensemble via the strengthened recurrent collaterals. Those connections pull the remaining ensemble members into firing. The cortex *completes the pattern* — it fills in the missing portions of the representation based on what it has learned about what usually appears with what.

This is pattern completion, and it is the generalization operation. The partial or noisy input is resolved into the closest stored template by the auto-associative dynamics of the recurrent network.

Let me make this concrete. Suppose a fish has learned to associate Odor A with food. Odor A activates a pattern of forty cortical neurons out of a thousand. Hebbian plasticity strengthens the connections among those forty proportionally to how often they fire together. Now the fish encounters a dilute version — enough to activate twenty-five of the forty neurons directly. The twenty-five fire. They are strongly connected to the other fifteen via the strengthened recurrent collaterals. Summed input across multiple active ensemble members pushes those fifteen above threshold. They fire. The pattern completes to forty neurons. The downstream evaluator receives the same signal as for the full odor. The fish approaches the food source.

Without the recurrent connections, the fish represents the dilute odor with twenty-five active neurons — a weaker, different pattern. The downstream evaluator fails to recognize it as Odor A. The fish does not approach.

The recurrent completion is not a bonus feature. It is the mechanism that makes learned knowledge useful under real-world conditions where inputs are always partial, noisy, and variable.

![Pattern completion in piriform cortex — Odor A.](../images/06-pattern-recognition-and-perception-fig-03.png)

*Figure 3 — Pattern completion in piriform cortex — Odor A.*

The full system does what no simpler system could. Dimensionality expansion separates similar inputs in representational space. Sparse coding through lateral inhibition enforces discrimination by amplifying differences. Recurrent connections implement auto-associative memory that generalizes across variations. The same physical structure performs both operations — not by switching between two modes, but using the *same neurons* for both, with the operations interleaved across the time course of the response.

---

The olfactory case establishes the architecture. The visual case shows it doing something harder.

Caroline DeLong and colleagues at the Rochester Institute of Technology trained goldfish on a discrimination task using photographs of real objects: a plastic toy turtle and a plastic toy frog. The fish learned the discrimination at zero degrees of rotation. Then they were tested at ninety, one hundred eighty, and two hundred seventy degrees of rotation — including depth rotations showing the objects from entirely different viewpoints.

The goldfish were significantly above chance at every rotation. They recognized the objects even when the photograph showed a viewpoint they had never seen during training.

Two things are worth noting. First, the goldfish were not detecting simple visual features, because the rotated images differed substantially in exactly those features. A photograph of a frog from below looks different from a photograph of a frog from the front in overall brightness distribution, the positions of color patches, and the aspect ratio of the body outline. The goldfish was doing something more abstract than feature detection.

Second — and this is the detail most interesting — the goldfish were faster on the upside-down rotation than on the ninety-degree rotation. This asymmetry is not predicted by pure viewpoint-invariant recognition. If the brain were simply building a viewpoint-independent representation from the start, all rotations should be equally fast or slow. The asymmetry hints at a recognition process that is partly viewpoint-dependent — perhaps something like mental rotation — that is cheaper for a one-hundred-eighty-degree flip, which preserves bilateral symmetry relationships, than for a ninety-degree turn, which does not. I will say directly that I do not fully understand this asymmetry. But its existence tells us something real: viewpoint-invariant recognition is not a flat representation, disconnected from viewpoint. It is built on top of a viewpoint-sensitive substrate, and the two interact in ways our current models have not fully captured.

![Goldfish recognition across rotations.](../images/06-pattern-recognition-and-perception-fig-04.png)

*Figure 4 — Goldfish recognition across rotations.*

The archerfish face result has the same flavor. Faces at different angles, different lighting, across demographic variation — recognized reliably by a fish without the dedicated cortical regions that mammalian neuroscientists spent decades characterizing as necessary for face processing. The fish's three-layered pallium, with its dimensionality expansion, sparse coding, and recurrent completion, is apparently sufficient for what was once thought to require specialized mammalian machinery.

This is not a demolition of mammalian neuroscience. It is a clarification of what the truly foundational operations are, and what the later elaborations add on top of them.

---

David Hubel and Torsten Wiesel's Nobel Prize-winning discovery of orientation-selective neurons in the visual cortex — simple cells responding to local oriented edges, complex cells pooling across positions to give translation invariance — was the direct inspiration for the convolutional neural network. The logic was sound: if the brain solves visual recognition by building a hierarchy of increasingly abstract features, an artificial system with the same hierarchical structure should produce similar capabilities.

In one important sense, this prediction was confirmed. Daniel Yamins and James DiCarlo trained a hierarchical CNN on object categorization and asked whether the network's intermediate activations predicted the firing of neurons in macaque inferior temporal cortex. The top layer of the trained network was the best predictor of IT neuron responses the field had produced. Architecture plus task, matched sufficiently, produces matching representations. This is a real and important finding.

In another important sense, the analogy breaks down. CNNs in their standard feedforward form are excellent at translation invariance — the convolutional structure builds this in mathematically, by sharing weights across positions. They are poor at rotation invariance, scale invariance, and recognition under unusual viewpoints unless these have been explicitly represented in the training data. The goldfish recognizing a rotated frog it has never seen is doing something the standard CNN cannot do without specific training on rotated frogs.

The deeper problem is relational reasoning. Asking whether two shapes are the same — abstracting away what the shapes are and caring only about the relation between them — requires a representation of the relation as such. Feedforward CNNs encode features of parts. They do not, in their standard form, encode relations between parts as a distinct representable quantity. Fish, and certainly mammals, can learn same-different relations and apply them to new shapes. Standard CNNs cannot, at least not from the amounts of data plausible in a biological context.

The explanation for this gap comes from what the engineers copied and what they left out. What was copied: the feature hierarchy. Local feature detectors at the bottom, progressive abstraction upward. What was not copied: the recurrent auto-associative completion. The sparse coding enforced by lateral inhibition. The thalamic gating mechanism that controls which input reaches the cortex — a selective attention system that filters the information stream before processing begins.

These omitted components are precisely the ones that explain the remaining performance gaps. Recurrent completion enables recognition of partial and degraded inputs by completing the pattern toward a stored template. Sparse coding enables resistance to catastrophic forgetting by ensuring new patterns are represented in neurons not previously committed to old ones — two sparse patterns in a thousand-neuron sheet have very little overlap, so learning one does not overwrite the other. Thalamic gating enables selective attention, allowing the system to focus on the dimensions that carry the diagnostic information while suppressing irrelevant variation.

The engineers took the feedforward recognition path and left out the recurrent stabilization path. The result is a system that is extremely good at specific discrimination tasks it was trained on, and less robust than biology on everything else.

---

The three-operation framework — dimensionality expansion, sparse coding, recurrent completion — is not unique to the olfactory or visual cortex. It appears wherever the vertebrate brain has had to solve a pattern-recognition problem.

The hippocampus runs the same architecture for spatial and episodic memory. The dentate gyrus performs pattern separation, expanding the incoming representation from the entorhinal cortex into a very sparse code, pushing similar inputs into distinct neural ensembles. CA3 performs pattern completion — it has the most recurrent collateral connectivity of any cortical region in the mammalian brain, and it uses this to complete partial spatial or episodic patterns toward stored templates. The hippocampus is the cortical architecture specialized for time-extended pattern completion, running the same three operations on sequences of experience rather than simultaneous sensory inputs.

The cerebellum runs a related architecture. Its granule cells perform massive dimensionality expansion on sensorimotor inputs — more than half of all neurons in the human brain are cerebellar granule cells. The Purkinje cells then perform supervised pattern classification over this expanded representation. The learning rule differs from the Hebbian rule in the piriform cortex, but the expand-then-classify logic is the same.

The neocortex proper — the six-layered sheet that mammals expanded dramatically — adds hierarchical abstraction and executive control on top of the three-layer base, but it does not replace it. Layers two and three are the recurrent horizontal connectivity layers, the layers most involved in auto-associative completion and cross-column integration. Layers four and five handle the input-output interface. The neocortex is the three-layer architecture, elaborated vertically with more processing stages and more opportunities for top-down modulation.

The avian pallium arrived at comparable functional sophistication by a different route. Where the mammalian cortex is organized in layers, the bird pallium is organized in nuclei — clusters rather than sheets. But within those clusters, the same logic applies: cells with overlapping inputs form recurrent ensembles, lateral inhibition enforces sparse coding, and the resulting representations support both discrimination and generalization. Convergent evolution of the same computation in different anatomical implementations. That convergence is the strongest evidence the three operations are not an arbitrary design choice. They are the solution to a hard computational problem, and any nervous system that solves that problem will implement something recognizably similar.

---

The cortical pattern-recognition architecture is very good at recognizing instances of learned categories and generalizing learned categories to new instances. It is much weaker at *compositional reasoning* — taking known parts and assembling them into a novel whole in a structured way. Recognizing a face is different from understanding that the face belongs to a person on a bicycle crossing a bridge. The latter requires representing relations between objects, not just the objects themselves. How the primate cortex handles relational reasoning — whether through working memory in the prefrontal cortex, temporal synchrony binding, or some other mechanism — remains genuinely contested.

It does not easily support explicit abstraction. The auto-associative architecture stores patterns by strengthening connections among co-firing neurons and retrieves them by completing partial inputs toward stored templates. It does not, in its basic form, construct a rule that can be stated verbally and applied systematically to new instances that differ in principled ways from training examples. This is fine for perceptual recognition, which does not require explicit rules. It is insufficient for the kinds of reasoning about rules and categories that appear in primate cognition and that will occupy the later chapters of this book.

And it does not produce invariance to truly novel transformations. The goldfish's rotated-frog recognition is impressive, but it may depend on having seen a wide variety of natural objects at natural orientations, building a prior for how objects deform across viewpoints. When the transformation is genuinely novel — a kind of distortion the animal has never encountered in any domain — the auto-associative completion will produce the wrong stored pattern, because the partial match will complete toward the wrong template. The failure mode is systematic, not random, and it can be difficult to detect.

These limitations are not bugs in the cortical design. They reflect the different problems the brain needed to solve at different evolutionary stages, and the later chapters are about the mechanisms added to handle the problems the basic pattern-recognizer cannot solve alone.

---

The archerfish that picked the right face out of forty-four did not do it because it is remarkable. It did it because it has the standard vertebrate solution to a standard vertebrate problem. We are the ones who thought the problem was hard.

What made us think so is a reasonable confusion. Face recognition, in humans, is so fast and so reliable — so apparently effortless — that we assumed it must involve elaborate machinery tuned specifically to faces, machinery that took a long time for evolution to develop. And there *is* elaborate machinery in the human face-processing system: a dedicated cortical region, the fusiform face area, with preferential responses to upright human faces, with specific disruptions in prosopagnosia, with developmental trajectories that differ from general object recognition.

But the archerfish result tells us that the elaborate machinery is not what does the recognizing. The elaborate machinery is what makes face recognition fast, automatic, robust, and wired into social cognition. The basic discriminative capacity — telling this face from those forty-three others — runs on the three-layer architecture that was already in place before anything had a face worth recognizing.

The fish showed us the floor. The human face area is what happens when hundreds of millions of years of primate social life have occasion to optimize the floor.
