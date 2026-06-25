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

3. **Evidence** — a study, dataset, or observation, tagged with strength and
   quality. Links to claims as *supports* / *refutes* / *qualifies*. The same
   study can support one claim and undercut another.

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
   graph explodes.
2. **Evidence scoring** — adopt an existing hierarchy (GRADE-style) or define our
   own strength model? Who/what does the scoring, and how is it kept honest?
3. **Support vs consensus** — how do we represent, in one structure, that a claim
   is *institutionally endorsed* yet *evidentially thin* (or vice versa) without
   the model itself taking a side?
4. **Where the Author Engine boundary sits** — how much actor analysis happens in
   the engine vs in the subject layer? What exactly does the engine hand up?
5. **Neutrality / auditability** — every verdict needs to trace to sources a
   skeptic can follow. The structure is the argument; it shouldn't hide a thesis.
6. **Generalisation** — nutrition is instance #1. What here is nutrition-specific
   vs reusable for any contested subject (climate, a historical debate, etc.)?
