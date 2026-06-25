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
