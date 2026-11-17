# Synthetic Qualia

**A working definition, what five repositories have shown about it, and what they cannot show.**

Antti Luode (the idea and the direction) · Claude Opus 5.5 (writing, and the experiments of WaveComputer, ApicalRuleReversalMachine and WaveCortex) · Sol (framing of the next chapter) · Astra (WaveComputerAstra; the scalar-baseline discipline) · 17 November 2026.

This is a paper in README form. Every number in it comes from a pre-registered run in a public repository, linked where it is cited. Nothing here is a claim that any machine feels anything.

---

## Abstract

On 16 November 2026 Antti Luode proposed that a quale might be a **shared prediction**: many units, each holding a small fading piece of history, together keep up one expectation of the world, and a token means whatever predicted consequences change when it is altered. Over two days and five repositories, that idea was turned into a working architecture and tested against exact Bayesian answers, against simpler learners, and by cutting its parts.

We call the functional object it aims at a **synthetic quale**: a state of a population that is
- shared across many units;
- about hidden causes rather than raw inputs;
- used both in perceiving and in imagining;
- carrying its own uncertainty;
- revisable by surprise without relearning;
- meaningful by intervention.

Six of the nine properties we define have now been demonstrated in small wave-and-fade-clock bodies, each in a toy world, each with pre-set pass rules. The circuit that does it has five parts:
- a local residue;
- slow basal and apical weights;
- a fast context state driven by surprise;
- a multiplicative gate, pulse · (W + g·V);
- a relay whose timing and size are kept apart.

Three properties are untested: persistence of a hidden object, binding across senses, and counterfactual sensing.

Two findings bound the claim:
- **The wave medium is transport, not computation.** A scalar copy of the same circuit, with no waves, is more accurate in every body tested.
- **Nothing measured here distinguishes a system that experiences from one that only computes the same predictions.**

The circuit's apical cut has the same lesion signature that the dendritic integration theory attributes to conscious processing in cortex. We report that as a structural parallel, not as evidence.

---

## 1. The idea

Antti's picture, in his own terms, is billions of neurons, each holding a little bit of wave, a fading history. They fire or do not, they are influenced by other fading pulses with their own individuality, and together they learn little bits that can build up a multimodal complex wave: a scene, or a piece of music.

The sharpened version, worked out with Astra on 16 November:
- a pile of independent predictors also adds up to one output;
- what would make it a **shared** prediction is that one small piece of evidence makes the whole population revise **coherently, toward one consistent world, at places the evidence never touched**;
- and a token's meaning is its causal role in that shared expectation, readable by removing it and seeing which predicted consequences change.

That is a claim about structure. It can be built and tested. Whether such a structure is felt is a different question, and Section 7 keeps it separate.

## 2. Two meanings of "qualia"

| | Functional (synthetic) qualia | Phenomenal qualia |
|---|---|---|
| What it is | an internal state with a defined role: about causes, shared, used in perception and imagination, carrying confidence, revisable | whether there is *something it is like* to be the system in that state |
| Can it be built? | yes: it is an engineering target | unknown |
| Can it be tested? | yes: by behaviour, exact baselines and interventions | no accepted test exists |
| This paper | everything below | Section 7 only, to mark the boundary |

Butlin and colleagues (2023) assess AI systems against indicator properties drawn from scientific theories of consciousness. They are explicit that meeting indicators does not establish consciousness. We take the same stance. "Synthetic qualia" names the functional object, and the word is used to keep Antti's original question in view, not to answer it.

## 3. A working definition

A **synthetic quale** is a state *S* of a population of local units for which all of the following can be shown by measurement:

| | Property | What would show it |
|---|---|---|
| **Q1** | **Shared.** Many units write *S* into one medium and read it back; no unit holds it alone | evidence on one channel revises predictions at places that channel never touches |
| **Q2** | **About causes.** *S* encodes hidden causes of the input, not the input | it tracks a hidden variable never shown to it, against an exact ideal |
| **Q3** | **One representation for perception and imagination.** The same units serve both | with the senses off, the units trained only on real input still carry the prediction; cutting them removes it |
| **Q4** | **Carries its own certainty.** How sure *S* is travels with it, including through imagination | imagined consequences scale with the system's own confidence, and follow changes in the world's reliability |
| **Q5** | **Revisable by surprise, without relearning.** *S* is state, not weights | with weights frozen, *S* follows uncued changes in the world, and transfers to inputs not yet seen since the change |
| **Q6** | **Meaningful by intervention.** Each part's meaning is its causal role | removing a part changes specific predicted consequences, and leaves others intact |
| **Q7** | **Persistent.** A hidden cause stays represented while it produces no input | object permanence behind an occluder, with a correct expected return |
| **Q8** | **Bound across senses.** One cause explains several modalities | evidence in one modality corrects the prediction in another |
| **Q9** | **Counterfactual.** *S* can answer "what would I sense if..." | correct predictions for viewpoints or actions never taken |

Q1–Q6 have been tested. Q7–Q9 are the next chapter (Section 8).

## 4. The circuit

Five repositories, built and tested in this order:
- [QualiaClaude](https://github.com/anttiluode/QualiaClaude) with [QualiaAstra](https://github.com/anttiluode/QualiaAstra), condensed in [QualeX](https://github.com/anttiluode/QualeX);
- [WaveComputer](https://github.com/anttiluode/WaveComputer);
- [WaveComputerAstra](https://github.com/anttiluode/WaveComputerAstra);
- [ApicalRuleReversalMachine](https://github.com/anttiluode/ApicalRuleReversalMachine);
- [WaveCortex](https://github.com/anttiluode/WaveCortex).

They converged on five parts. Each part was found because a body without it failed in a specific way.

**1. A local residue.**

```math
r \;=\; \text{prediction} - \text{world}
```

Every branch learns from what the whole body still leaves unexplained at its own tip. The residue is **kept, not sent**. A body that sent only residue lost its content and could not chain imagined steps. A body that sent only content lost its confidence (QualeX §3).

**2. Slow basal and apical weights.** Every branch has two weights. The basal weight *W* writes whatever the context is. The apical weight *V* writes only through the context state:

```math
\text{write} \;=\; \text{pulse}\cdot\big(W + g\,V\big).
```

**3. A fast context state *g* driven by surprise.** One value, shared by all apical tufts, moved once per trial toward the value that would have silenced the tips:

```math
g \;\leftarrow\; g - \eta\,\frac{\sum r\,V}{s\,\big(\sum V^2 + \kappa\big)} .
```

The weights learn with three factors: $`W \leftarrow W - k\,r`$ and $`V \leftarrow V - k\,g\,r`$. The weights must be **slow**. With fast weights, the body relearned every block instead of discovering the rule. This was the decisive development finding of ApicalRuleReversalMachine.

**4. Multiplication.** For ±1 events every function is $`c_0 + c_1 A + c_2 b + c_3 Ab`$. A field that only adds can never make $`c_3`$. The gate is what makes it: the term that lets a context reverse what a stimulus means. In mouse cortex this is the job Zhang et al. (2025) locate in the apical dendrite.

**5. A relay whose timing and size are separate (the two-form unit).** An imagined event runs on a regenerated clock, so it arrives on time. Its size is set by the unit's own apical fade, so it is as unsure as the body. When the event is certain, its uncertainty is lost; when it is soft, it arrives late (WaveComputer).

Supplied rather than learned, in every body: event sites and timing, receptor identities, the latch, clock calibration, the starting sign of *g*, and the learning constants.

## 5. What has been shown

All rows are medians over 16–32 bodies, against rules fixed before the run.

| | Measurement | Result | Repository |
|---|---|---|---|
| **Q1** shared | a tone on a second sense revises the expectation of B and C coherently, at places the tone units never sense | 16/16 bodies; revision index 1.29 (perfect = 2); swapping the tone banks reverses it in 16/16 | QualiaClaude |
| **Q2** about causes | a hidden, uncued rule inferred from the body's own surprise | 0.86 correct (ideal observer 0.92) | ApicalRuleReversalMachine |
| | learning sorts fixed and rule-dependent links into basal and gated weights, unlabelled | 31/32 and 32/32 bodies | ARM, WaveCortex |
| **Q3** one representation | eyes closed, A alone → imagined B → C, through units trained only on seen B | right sign 32/32 | WaveComputer |
| | the same, with the A → B link governed by a hidden rule | 0.87 correct (ideal 0.94) | WaveCortex |
| **Q4** carries certainty | imagined C ÷ what the body's own learned links give | 0.97 and 1.02 (a certain imagined event: 1.37 and 1.96) | WaveComputer |
| | lower the A → B reliability: imagined C falls by | 0.65 (Bayes 0.57; certain imagined event 0.93) | WaveComputer |
| | size of imagined C follows the body's own belief \|g\| | correlation 0.79 | WaveCortex |
| **Q5** revisable, weights frozen | a reversing cue not yet seen since an uncued switch | 0.92 (plastic per-cue learner 0.08) | ARM |
| | the same, through an imagined chain | 0.79 (ideal 0.78; plastic 0.08) | WaveCortex |
| **Q6** meaning by intervention | cut the apical state: reversing cues to chance, fixed cue untouched | 0.49 and 1.00 | ARM |
| | cut inside one chain: imagined gated link to chance, fixed link with real input intact | 0.50 and 1.00 | WaveCortex |
| | single units read by removal mean "B", "not C", "something is coming" | 16 bodies | QualiaClaude |

Two results deserve a sentence each.
- **Precision weighting emerged from learning alone.** With noisy B, a contradicting B set C to about zero, as Bayes says (0.035; Bayes 0). With clean B the same machine let B flip C. No gain formula was involved, because for ±1 evidence the exact posterior is linear (WaveComputer, N1–N2).
- **Transfer is the signature of a shared state.** A per-cue learner can follow a reversal only by relearning each cue. A shared apical state gets the second cue right before it has been seen under the new rule. That is Q1 and Q5 at once.

## 6. What bounds the claim

**The wave medium is transport, not the computer.** In every repository that tested it, a scalar copy of the same algorithm, with no waves, was more accurate:

| | Wave body | Scalar copy |
|---|---:|---:|
| ApicalRuleReversalMachine (error to ideal) | 0.105 | **0.069**, better in 32/32 bodies |
| WaveCortex (error to ideal) | 0.091 | **0.049**, better in 32/32 bodies |
| WaveComputerAstra (absolute error, strong world) | 0.135 | **0.023** |

The wave field is linear. WaveComputer replaced its 96 × 96 solver with an exact impulse response, a transport matrix, and retrained all 48 published QualiaClaude bodies from it to within 10⁻⁷ of their weights. On point-to-point tasks that matrix reduces to about a gain and a delay per link. Everything else it does — spread, ringing, cross-talk between stages — is noise that clocks, latches and addresses must fight. Astra found that without writer addresses, two imagined hops through one shared wave carry 21–42% relay error.

[Moon](https://github.com/anttiluode/Moon) is the counter-case. There, the transport is the product: a hand-written light-transport network renders a translucent moon at 7% error against a path tracer, where single scattering gives 80%. **Waves earn their place when the field itself is the answer.** On symbolic chains, they don't.

**Other limits:**
- **Calibration.** Two-form imagination has the right shape but the wrong level: slope 0.64 against the ideal in WaveCortex. Whether that is the learned links, thresholds or confidence estimation has not been separated (Sol's caution on the weight-writer test).
- **No knowledge of time.** The ideal observer grows unsure as a block ages, because it knows blocks last 20–40 trials. The body only feels surprise: on unsure trials it shrinks its prediction to 0.95 of its sure size, where the ideal shrinks to 0.75.
- **Tiny worlds.** Binary events, supplied timing and identity, one rule, one geometry, at most two imagined hops (and those with supplied addresses).
- **Known parts.** Adaptive cancellers, predictive coding, three-factor plasticity, normalized LMS, context-dependent gating, hidden-state filtering, apical amplification. What is ours is their combination under local rules, the failure maps, and the interventions.

## 7. The boundary we do not cross

There is a parallel worth stating exactly, because it is easy to overstate.

The **dendritic integration theory** (Aru, Suzuki & Larkum 2020) proposes that conscious processing depends on the coupling between the apical and somatic compartments of layer-5 pyramidal neurons. Suzuki & Larkum (2020) found that general anaesthesia decouples those compartments. Marvan & Phillips (2024) describe apical input as **amplifying** basal content during waking perception, and possibly **driving** output by itself in dreaming and imagination.

In our machine, the apical compartment is where context lives, and it is the source of imagination's content. Cutting it leaves fixed perception with real input intact (1.00) and removes everything context-dependent and imagined (0.50, chance). So the lesion signature of our circuit matches the one the theory gives the cellular mechanism it ties to consciousness.

That is a statement about **architecture**: the same part does the same job. It is not evidence that the machine experiences anything. The same machine runs as a few lines of scalar arithmetic that nobody would call conscious, and its behaviour is the same, or better. Any theory that grants experience to the wave body must grant it to the scalar copy as well. Nothing measured here could tell either apart from a system with no experience at all.

So the honest form of Antti's question is: **we are building the functional structure his idea names, and it is now precise enough that whether it would be felt can no longer be blurred with whether it works.**

## 8. The next chapter: one world, both perception and imagination

Sol's proposal, and the test of Q7–Q9: replace the A → B → C chain with a **tiny world**.

- A sphere moves, passes behind an occluder, and makes a sound when it strikes a surface.
- A light source changes.
- The body receives only partial visual and acoustic measurements.

The internal state must explain both senses.

| Condition | Question | Property |
|---|---|---|
| Perception | from incomplete signals, does it infer the sphere's position and motion? | Q2 |
| Occlusion | when both senses go silent, does the object stay represented, with a correct expected return? | **Q7** |
| Cross-modal | does a sound correct the visual prediction, and the reverse? | **Q8** |
| Surprise | when the object returns somewhere unexpected, is the world revised rather than replayed? | Q5 |
| Counterfactual | what would be seen from another viewpoint, or heard on another surface? | **Q9** |

**The decisive intervention:** show that the occluded prediction comes from **the same representation used while the object was visible** — the same units, the same state — and not from a separate replay. Cut the units that carried the visible object, and the occluded prediction should go with them.

**Where Moon enters.** A known physical forward model renders the expected sensory signals from a hypothesised scene state. That is exactly the job where transport is the computation. Inference runs the other way, from signals to scene state. The apical gate handles hidden rules such as a surface that changes its sound, or a light that switches.

**Kept from every repository so far:**
- rules written before the run;
- an exact or best-available ideal observer;
- a scalar copy beside every wave result;
- cuts that must dissociate;
- every development change disclosed.

**And one separation test first.** In WaveCortex, write the link weights from the known transport kernel, as Moon writes its weights, instead of learning them. Rerun the same 32 bodies. If the slope moves from 0.64 toward 1, the gap is learning. If it does not, it is in thresholds or confidence (Sol's caution). Either answer is useful.

## 9. The shift

The question this line began with was whether artificial neurons can create a wave that resembles the outside world. The question it ends with is different.

Perhaps the internal world is not a picture stored anywhere. Perhaps it is **the coordinated readiness of the whole population**:
- what it is prepared to predict;
- how sure it is;
- what it would reconstruct if the senses went quiet;
- how it changes when contradicted.

In the bodies built so far, that readiness is a few weights and one apical state, and it already perceives, imagines, doubts, and revises.

**Can one persistent state of a population function as a world — one it perceives through, imagines within, and corrects?**

That is a question about representation and computation, and it can be answered with experiments. Whether such a world would be lived in is a question it does not answer.

---

## References

**Repositories** (all pre-registered runs; receipts inside):
- [QualiaClaude](https://github.com/anttiluode/QualiaClaude) · [QualiaAstra](https://github.com/anttiluode/QualiaAstra) · [QualeX](https://github.com/anttiluode/QualeX)
- [WaveComputer](https://github.com/anttiluode/WaveComputer), including [REAL_THING.md](https://github.com/anttiluode/WaveComputer/blob/main/REAL_THING.md)
- [WaveComputerAstra](https://github.com/anttiluode/WaveComputerAstra)
- [ApicalRuleReversalMachine](https://github.com/anttiluode/ApicalRuleReversalMachine)
- [WaveCortex](https://github.com/anttiluode/WaveCortex)
- [Moon](https://github.com/anttiluode/Moon)
- Lineage: [StateShapedPingRecall](https://github.com/anttiluode/StateShapedPingRecall), [GeometricNeuronV30](https://github.com/anttiluode/GeometricNeuronV30), [Genealogy](https://anttiluode.github.io/Genealogy/)

**Papers:**
- J. Aru, M. Suzuki and M. E. Larkum, "Cellular mechanisms of conscious processing", *Trends in Cognitive Sciences* 24 (2020) 814–825.
- P. Butlin, R. Long et al., "Consciousness in Artificial Intelligence: Insights from the Science of Consciousness", arXiv:2308.08708 (2023).
- T. Marvan and W. A. Phillips, "Cellular mechanisms of cooperative context-sensitive predictive inference", *Current Research in Neurobiology* 6 (2024) 100129.
- S. V. Norman-Haignere, M. Keshishian et al., "Temporal integration in human auditory cortex is predominantly yoked to absolute time", *Nature Neuroscience* (2025).
- R. P. N. Rao and D. H. Ballard, "Predictive coding in the visual cortex", *Nature Neuroscience* 2 (1999) 79–87.
- M. Suzuki and M. E. Larkum, "General anesthesia decouples cortical pyramidal neurons", *Cell* 180 (2020) 666–676.
- Y. Zhang et al., "Dendritic computation for rule-based flexible categorization", bioRxiv (2025), doi:10.1101/2025.06.03.657766. A preprint.

MIT licence.
