# Subject Analysis — Idea Doc

*Exploration · v0.1 · keep separate from the Author Engine (in development)*

> Status: thinking out loud. This is a framing doc, not a spec. Nothing here
> is committed-to. Example case is used to pressure-test the framework, not to
> pick a side.

## The move

The Author Engine analyses **a person** — take a figure's complete *oeuvre*,
map it semantically, fingerprint it, make it searchable. One corpus, one voice.

This doc extends the idea to **a subject** — a field, or more precisely a
*controversy* within a field. The unit of analysis is no longer "what did this
person say and mean" but "what does the field claim, where did each idea come
from, and which claims actually hold up against the evidence."

**The nesting:** author analysis becomes a *block* inside subject analysis.
A subject has actors; each actor gets run through the Author Engine; those
per-actor results feed the subject-level graph. The Author Engine doesn't go
away — it becomes a component.

```
Subject  (e.g. "the mess" in nutritional science)
 ├─ Claims        — contested propositions, author-independent
 ├─ Assumptions   — load-bearing premises, often unexamined
 ├─ Evidence      — studies / data, with strength + quality
 ├─ Actors        — each analysed by an Author-Engine block ◄── the old engine, nested
 └─ Provenance    — origin → propagation graph linking all of the above
```

## Example case (the test harness, not the thesis)

**Nutritional science**, focused on the controversy Zoë Harcombe* calls
**"the mess"** — roughly, the claim that the foundational dietary-fat /
heart-disease consensus was built on assumptions that the original evidence
never actually supported.

\* *spelling to confirm — likely "Zoë Harcombe".*

Why it's a good test case:
- Long citation lineage (ideas propagated for decades) → exercises **provenance**.
- A few load-bearing assumptions carry enormous downstream weight → exercises
  **assumption-tracking**.
- The disagreement is partly about *evidence quality*, not just conclusions →
  exercises the **evidence layer** and the "widely-repeated vs actually-evidenced"
  distinction.
- Clear actors on multiple sides → exercises the **nested Author Engine**.

The job is **not** to declare a winner. It's to build a structure that makes the
disagreement legible: what is claimed, what it rests on, and where the evidence
actually lands.

## What a subject needs that an author didn't

The Author Engine's primitives (corpus, semantic map, fingerprint) are
author-scoped. Subject analysis needs primitives that live *above* any single
author:

1. **Claim (proposition)** — first-class, author-independent. e.g. "saturated
   fat raises heart-disease risk." A claim is asserted, denied, or qualified by
   many actors; it is not owned by one. This is the atom of a subject.

2. **Assumption** — a premise a claim silently depends on. "Going deep on the
   underlying science" = surfacing implicit assumptions and making each one
   testable. Assumptions are where most of the leverage (and most of the mess)
   lives.

3. **Evidence** — a study, dataset, observation, or *mechanistic determination*,
   tagged with **kind** and **quality** (see "Evidence: kind before quality").
   Links to claims as *supports* / *refutes* / *qualifies*. The same item can
   support one claim and undercut another.

4. **Actor + Position** — an actor (Keys, Harcombe, a body like the AHA) holds a
   *position*: a bundle of claims they assert and assumptions they accept. The
   Author Engine produces the actor's profile; the position is how that profile
   plugs into the subject graph.

5. **Provenance / transmission** — *where did this idea come from?* Origin node
   (who first asserted it) + propagation edges (who repeated, amplified,
   institutionalised it). This is the spine that lets us separate **lineage**
   (how an idea spread) from **support** (whether evidence backs it).

6. **Inference (the leap)** — the edge from a study's observations to its
   conclusion. First-class and *checkable*: it carries the assumptions it relies
   on, the alternative explanations (confounds) it failed to rule out, and a
   logical form that may be invalid. This is where most errors enter, so it gets
   its own object instead of hiding inside "study."

## The two questions the framework must answer

Everything above exists to serve two queries the user named:

- **Where did this idea come from?** → trace the provenance graph back to origin
  and follow the transmission edges forward.
- **Is it actually supported by the evidence?** → trace the claim down through
  its assumptions to the evidence, and score support — explicitly distinguishing
  *"widely repeated"* from *"actually evidenced."* A claim can score high on
  propagation and low on support; surfacing that gap is the whole point.

## The shape: a dependency hierarchy of ideas

Nutritional science isn't a flat pile of claims — it's **a scaffold of stacked
assumptions**, much of it resting on low-quality epidemiology. So the structure
we build is a **dependency hierarchy**: ideas connected by *rests-on* edges,
foundations at the bottom, top-level conclusions (and policy) at the top.

Two directions, and they're opposite on purpose:

- **Discover top-down.** Start from the top-level ideas (the big conclusions
  everyone argues about), and for each ask *"what does this rest on?"* Recurse
  until you hit foundations — mechanistic facts, definitions, raw data.
- **Evaluate bottom-up.** Test the *foundations* first, because that's where the
  leverage is and where failures cascade. A higher claim can be **no stronger
  than its weakest load-bearing support**. Propagate verdicts upward: when a
  foundation falls, everything resting on it is re-scored automatically.

This mirrors the PM model's anchors: intent at the top (blue), the atomic
checkable unit at the bottom (yellow), decomposition bridging down. Here the
atomic checkable unit is a *piece of evidence*; the conclusions are derived.

> Practical first step (the one you named): enumerate top-level ideas → map each
> down to what it rests on → get the hierarchy → then go to the lower levels and
> check the evidence to see which upper levels survive.

## Evidence: kind before quality

The most important rule in this whole framework: **you cannot rank evidence on a
single scale, because different kinds answer different questions and carry
different sufficiency rules.** Quality is a second axis *within* a kind, not a
universal currency.

| Kind | Example | What makes it sufficient | What it can do |
| :-- | :-- | :-- | :-- |
| **Mechanistic / structural** | enzyme present/absent, a metabolic pathway | one rigorous determination; replication is *nice*, not *required* | **establish or refute** by mechanism |
| **Interventional (RCT)** | controlled dietary trial | adequate design + power; ideally replicated | support causal claims |
| **Epidemiological (enquête)** | observational / correlational survey | **many** repetitions; preferably **meta-analysis** | at best *suggest*; weak alone |

The trap the framework exists to prevent: treating a mechanistic fact as "just
one study" (so demanding statistical replication it doesn't need), or treating a
pile of correlated epidemiology as if volume converts it into a mechanism. Each
node must declare its **kind**, and the **sufficiency rule for that kind** is
what "is it supported?" gets checked against.

### The taint relation (cross-cutting invalidation)

A foundational mechanistic fact can sit *underneath* an assumption baked into
many downstream studies. When the fact establishes *not-X* and those studies
assumed *X*, their conclusions are **tainted** — undermined regardless of how
clean their statistics are. This needs its own edge type:

```
fact  ──contradicts──▶  assumption  ──assumed-by──▶  study  ──supports──▶  claim
                                   (taint propagates right along this chain)
```

Two consequences the model must handle:
- **Retroactive cascade.** Discovering the fact *later* invalidates an already-
  accumulated body of work. Re-evaluation must ripple, not require manual redo.
- **Asymmetric power.** A single mechanistic node can outweigh dozens of
  epidemiological nodes pointing the other way — because it changes what those
  studies were even measuring.

### Worked micro-example (fructose)

"Humans can't break down fructose" is a perfect foundational node *and* a perfect
illustration of why precision matters — as stated it's three different claims:

- **Lost uricase** — the human lineage genuinely lost the enzyme; fructose →
  uric acid → fat-storage pathway runs unchecked. *(a true "missing enzyme")*
- **Unregulated fructokinase** — we *do* metabolise fructose, but via a pathway
  lacking the feedback brake glucose has. *(not "missing" — "unregulated")*
- **GLUT5 absorption limit** — a transport ceiling, a different mechanism again.

Each is plausibly true; each **taints different downstream work**. The model's
job is to refuse the fuzzy version and force it to the precise, sourced one —
because *which* mechanistic fact it is determines *which* branch of the hierarchy
falls. This single node shows the whole framework in miniature: a mechanistic
foundation, sufficiency by determination (not statistics), and a taint cascade
into every study that assumed the opposite.

## Studies split: observation vs interpretation

A study is not one thing. It is **two layers that must be stored separately**:

- **Observation (experimental fact)** — what was actually measured. Durable,
  reusable; its *kind* is whatever the method was. ("Serum triglycerides track
  with cardiovascular problems." "In test, dietary carbohydrate raised serum
  triglycerides more than dietary fat did.")
- **Interpretation (conclusion)** — what the authors claimed it *means*. This is
  a **Claim**, not a fact, reached from the observation by an **Inference**.

Why the split is load-bearing: **the conclusion is where it usually goes wrong,
and the observation survives the conclusion being wrong.** Rejecting a study's
interpretation does not cost you its facts. So taint attaches mostly to the
*interpretation* layer — a "discredited" study often has perfectly good
observations wearing a broken conclusion. Keep the facts; re-examine the leap.

This also refines provenance: **an assumption is frequently a laundered
conclusion.** "Avoid dietary fat" did not arrive as a fact — it began as one
study's interpretation, got promoted to a field-wide assumption, then was built
on without anyone revisiting the leap. "Where did this idea come from?" often
resolves to *a conclusion that quietly became an axiom.*

### Catalogue of inferential failure modes

The leap fails in recurring, nameable ways. Cataloguing them makes them
**scannable** — each becomes a check the framework can run over any inference (a
Skill, in PM-model terms). Two from the worked cases:

**Mislocated cause** — a real association is pinned to the wrong input.
- Observation: high serum triglycerides ↔ health problems. *(real)*
- Leap → "dietary fat raises triglycerides, so avoid dietary fat." *(the error)*
- Contradicting fact: dietary **carbs** raise serum triglycerides *more* than fat
  (excess carbohydrate → de novo lipogenesis). The effect was real; the cause was
  misassigned, so the advice points at the wrong lever.

**Conflated entity / unseparated sources** — a harmful thing is identified with
one of its sources while another is ignored, and the two are never separated
experimentally.
- Observation: saturated fat (in the body) ↔ higher health risk.
- Leap → "avoid eating saturated animal fat."
- But de novo lipogenesis turns excess carbs into **saturated** fat
  endogenously. So body-saturated-fat has at least two sources — dietary and
  carb-derived — and **no one separated which one carries the risk.** Meanwhile a
  *direct* link between eating saturated animal fat and heart disease has been
  hard to establish. Blame defaulted to the visible, intuitive source.

**Faux replication failure** — a study claims to falsify an earlier one but
silently violates a boundary condition the original named as essential. A null
result *outside* the original's stated domain is reported as a refutation
*inside* it; the original gets recorded as "debunked" and that false verdict
propagates.
- *Vitamin C / cancer.* Original: effect occurs **only** above a blood
  concentration reachable solely by IV (≈50 g+ intravenous). "Refutation": 10 g
  **oral** — which cannot reach that threshold — finds no effect and concludes
  "megadose vitamin C doesn't work." It never tested the original's claim; the
  null is exactly what the original predicts for that dose/route.
- *Glutamate (MSG) / brain damage.* Original: lesions are visible **only** if
  brains are examined within a short window before they heal. "Refutation":
  switches the feeding method (so ingested dose is uncertain) and inspects the
  next morning, after healing — sees nothing. Again precisely the original's
  prediction, published as a refutation.

Anatomy (so it's scannable): the refutation (a) targets a claim carrying **scope
conditions**, and (b) alters a load-bearing one — dose, route, timing,
measurement protocol — while presenting itself as an equivalent test, often with
**rhetorical cover** ("10 g is a megadose"). Unlike the two above, this defect
lives not on a single study's inference but on the **refutation edge between two
studies** (see next section).

These aren't one-offs — "the mess" is full of them. The catalogue grows as we map
the hierarchy, and each entry becomes a reusable lens to run over every
conclusion in the graph.

## Scope conditions and refutation edges

The faux-replication pattern forces two more objects into the model:

- **Scope conditions** — the conditions under which a claim holds: threshold,
  route, timing window, population, measurement protocol. An effect-claim is
  never just "X → Y"; it's "X → Y **when** [conditions]". Most faux refutations
  win by quietly stepping outside these, so scope conditions must be captured as
  explicitly as the claim itself.
- **Refutation / replication edge** — "study B falsifies / replicates study A" is
  a first-class, *checkable* relationship, not a settled fact. The check is one
  question: **does B satisfy A's scope conditions?** If not, the refutation is
  void, and any taint it placed on A must be **reversed** — A is reinstated.

Note the inversion. Normally taint flows from a *valid* contradicting fact; here
an *invalid* refutation creates *illegitimate* taint. So the framework must be
able to run taint **backwards** — detect and undo a false debunking — which is
exactly the case where the field's recorded verdict is upside down.

## Following the money (an orthogonal layer)

Both refutations above invite a "follow the money" reading. The framework should
record **incentive / conflict-of-interest metadata** on studies and actors — who
funded it, who benefits from the verdict — but keep it **strictly orthogonal to
the evidential verdict**.

The discipline: COI is a **prior on where to look, not a verdict.** A study is
not wrong because of who paid for it — the *boundary-condition violation* is what
voids it. The money only explains *why* a broken refutation got designed and
published. Keeping these separate is what stops the system from collapsing into
ad hominem (which would destroy its credibility): the structural defect carries
the conclusion, the incentive flags the node for scrutiny. A node with **both** a
motive and a defect is the strongest audit signal — but the defect still does the
work.

## How this rides on the existing meta (PM model)

This maps cleanly onto the v0.1 PM model — it doesn't need a new orchestration
system, just new domain objects:

- A **Subject** is a *Subproject* (one-off instance). "The mess in nutrition" is
  one such instance.
- Each **Actor's Author-Engine pass** is a *nested Subproject* under it — exactly
  the nesting the PM model already allows.
- The repeatable analysis routines — *extract claims*, *surface assumptions*,
  *trace provenance*, *score evidence* — are **Skills** (reusable, invocable,
  trigger-driven). They're the natural candidates for *promote-to-skill*: do it
  once by hand for one claim, then promote the chain.

So the "new meta level" here is **domain primitives (claim / assumption /
evidence / provenance), not a new engine.** The author work nests in as a block;
the PM model runs it.

## Open questions (for discussion)

1. **Claim granularity** — what is one claim? "Saturated fat is bad" vs the
   specific, testable version. Too coarse and provenance blurs; too fine and the
   graph explodes. (The fructose node shows the same problem for *foundations*.)
2. **The evidence-kind taxonomy** — is mechanistic / interventional /
   epidemiological enough, or do we need finer kinds (animal vs human mechanism,
   cohort vs case-control)? Each kind needs an explicit **sufficiency rule**.
3. **Taint propagation rules** — when exactly does a contradicting fact *fully*
   invalidate a study vs merely *weaken* it? Partial taint, confidence decay, and
   stopping the cascade from over-reaching all need defining.
4. **Quality scoring within a kind** — adopt an existing hierarchy (GRADE-style)
   or our own? Who/what scores, and how is it kept honest?
5. **Support vs consensus** — represent, in one structure, that a claim is
   *institutionally endorsed* yet *evidentially thin* (or vice versa) without the
   model taking a side.
6. **Where the Author Engine boundary sits** — how much actor analysis happens in
   the engine vs the subject layer? What exactly does the engine hand up?
7. **Neutrality / auditability** — every verdict traces to sources a skeptic can
   follow. The structure is the argument; it shouldn't hide a thesis.
8. **Generalisation** — nutrition is instance #1. What's nutrition-specific vs
   reusable for any contested subject (climate, a historical debate, etc.)?
9. **Observation/interpretation extraction** — splitting a paper's facts from its
   conclusions is the highest-value, hardest step (papers blur them on purpose).
   Done by hand, by an LLM pass, by the Author Engine? How do we keep the split
   honest and auditable?
10. **Failure-mode detection** — is the catalogue applied manually as a checklist,
    or can a pass *scan* inferences for each pattern? Where's the line between
    flagging a candidate and asserting an error?
11. **Scope-condition extraction** — boundary conditions are stated in the
    original paper but easy to miss; pulling them out reliably is the crux of
    detecting faux refutations.
12. **Reverse taint** — mechanics of reinstating a wrongly-"debunked" claim, and
    how to display "the field believes this is refuted, but the refutation is
    void."
13. **Incentive without ad hominem** — surface COI as an audit prior while
    guaranteeing it never becomes the evidential verdict.
