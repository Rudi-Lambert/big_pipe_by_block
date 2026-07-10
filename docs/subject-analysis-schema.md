# Subject Analysis — Data Model (Schema Draft)

*Design draft · v0.1 · derived from `subject-analysis-idea.md` and validated
against `nutrition-the-mess-hierarchy.md`.*

> This is the step where the idea becomes buildable. It turns the framework's
> structural inventory into concrete node / edge / attribute types, defines how a
> verdict is computed, and then **proves completeness**: every one of the 16
> catalogue defects is expressible as a check over these types. If a defect could
> not be expressed, the schema would be wrong — that's the test.

## Modeling choice: a property graph

The framework is edges as much as nodes (rests-on, inference, refutation,
provenance, substitution). A **directed property graph** — typed nodes and typed
edges, both carrying attributes — is the native fit. Trees/tables would flatten
the cross-cutting edges (taint, iatrogenic cascade) that are the whole point.

Implementation is deferred (see *Implementation*), but the logical model is a
property graph regardless of backing store.

## Node types

| Node | Key fields | Notes |
| :-- | :-- | :-- |
| **Claim** | `id`, `statement`, `role {conclusion \| assumption \| policy \| hypothesis}`, `scope_conditions[]`, `is_surrogate`, `verdict`, `granularity_ok` | The atom. **Assumption is a Claim with `role=assumption`** — so "laundering" (demoting a conclusion that became an axiom) is just a role change, not a new node. |
| **Observation** | `id`, `statement`, `evidence_kind`, `quality`, `measured_conditions`, `study_id` | The durable experimental fact — survives its study's conclusion being wrong. `evidence_kind ∈ {mech-human, mech-animal, rct, epi-cohort, epi-casecontrol, epi-ecological, definitional}`. |
| **Study** | `id`, `citation`, `year`, `author_ids[]`, `coi`, `observation_ids[]`, `conclusion_id` | Container: bundles Observations + one Conclusion, joined by an Inference edge. |
| **Construct** | `id`, `name`, `definition`, `well_defined`, `decomposes_into[]` | An exposure/entity ("saturated fat", "ultra-processed food"). Claims reference Constructs; ill-defined ones are flagged here. |
| **Actor** | `id`, `name`, `author_engine_ref`, `position_ids[]` | A person/institution. `author_engine_ref` points at the **nested Author-Engine subproject** — this is where the old engine plugs in. |
| **Position** | `id`, `actor_id`, `asserts[]`, `accepts[]`, `frame` | An Actor's stance: Claims asserted, Assumptions accepted, and an interpretive `frame` (the hook for *assumption-coloring*). |

## Edge types (directed, with attributes)

| Edge | From → To | Attributes | Purpose |
| :-- | :-- | :-- | :-- |
| **rests_on** | Claim → Claim / Observation / Construct | `load_bearing` | the dependency hierarchy; weakest load-bearing edge caps the parent |
| **inference** | Observation(s) → Claim(role=conclusion) | `assumptions_relied_on[]`, `confounds_unruled[]`, `logical_form`, `validity` | **the leap** — most single-study defects attach here |
| **supports / refutes / qualifies** | Observation → Claim | `strength`, `kind` (inherited) | evidential links |
| **contradicts** | Observation(fact) → Claim(assumption) | `established` | taint source (a fact establishing not-X under an assumed X) |
| **refutation** | Study → Study | `satisfies_scope` | "B falsifies A"; `satisfies_scope=false` ⇒ void ⇒ reverse taint |
| **origin** | Claim → Study / Actor | `origin_type {study-conclusion \| primary-fact \| misread \| none}` | provenance root; `none`/`misread` ⇒ phantom origin |
| **transmission** | Actor/Study → Actor/Study | `mode {repeated, amplified, institutionalised}` | propagation spine |
| **substitution** | Claim(advice) → Claim(harm) | `real_world` | cross-branch iatrogenic cascade |

## Overlays / attributes

- **Scope conditions** — structured on each effect-Claim: `{dimension, operator,
  value}` (e.g. `dose ≥ 50g`, `route = IV`, `window ≤ Nh`, `population =
  salt-sensitive`). The unit a refutation must satisfy.
- **Evidence kind + quality** — on every Observation; `kind` selects the
  **sufficiency rule**, `quality` scores within the kind.
- **COI** — on Studies and Actors; an audit prior, **never** an input to `verdict`.
- **Verdict** — on Claims: `{supported | unsupported | contested | untested}` +
  `confidence` + `rationale_trace` (the traversal that produced it — auditability).

## How a verdict is computed (the dynamics)

`verdict(Claim)` is derived, bottom-up, never hand-set:

1. **Direct evidence.** Gather `supports`/`refutes` Observations. Apply the
   **sufficiency rule for each kind** — e.g. a *causal* claim backed only by
   `epi-*` cannot exceed `contested`; a `mech-animal` fact alone cannot make a
   human claim `supported`. This is the "kind before quality" cap, enforced.
2. **Weakest load-bearing dependency.** `verdict ≤ min(verdict of each
   rests_on[load_bearing] target)`. A claim is no stronger than what it stands on.
3. **Taint.** A `contradicts` edge (established fact → assumption) downgrades every
   Claim whose `inference.assumptions_relied_on` includes that assumption. Adding
   such an edge **re-runs propagation** (retroactive cascade), not a manual redo.
4. **Reverse taint.** A `refutation` edge with `satisfies_scope=false` is void:
   remove the taint it applied and recompute — the wrongly-"debunked" claim is
   reinstated.
5. **Symmetric output.** The result is one of four states, not a defect flag —
   `supported` is renderable as confidently as `unsupported` (positive-control
   requirement).

## The two questions as graph traversals

- **Where did it come from?** Follow `origin` then `transmission` from the Claim.
  Returns the lineage; `origin_type ∈ {none, misread}` ⇒ **phantom origin**. The
  count of `transmission` hops is the *propagation* score.
- **Is it supported?** Traverse `rests_on` down to evidence, run the verdict
  computation. The *support* score is the verdict/confidence. **The headline
  finding is the gap** `propagation − support` — "widely repeated vs actually
  evidenced," computed directly from the two traversals.

## Completeness check: every catalogue defect is expressible

This is the schema's acceptance test — each of the 16 modes reduces to a predicate
over the types above. If one didn't, the schema would need to grow.

| Defect | Reads | Flag predicate |
| :-- | :-- | :-- |
| Mislocated cause | `inference` | `confounds_unruled` contains a stronger driver of the outcome |
| Conflated / unseparated sources | `rests_on` + `Construct` | Claim blames one `decomposes_into` source; others never separated |
| Reverse causation | `inference` | direction unestablished; exposure could be downstream of outcome |
| Healthy-user confounding | `Observation.kind=epi-*` + `inference` | `confounds_unruled` includes user characteristics |
| Reference-group contamination | `Observation.kind=epi-*` | comparison baseline group flagged impure (e.g. sick-quitters) |
| Surrogate-vs-outcome | `supports` + `Claim.is_surrogate` | support lands on a surrogate; endpoint Claim lacks its own support |
| Reductionist isolation | `rests_on` + `Construct` | Claim on isolated component `rests_on` Observation of whole-food Construct |
| Faux replication failure | `refutation.satisfies_scope` | `= false` |
| Overgeneralised scope | `Claim.scope_conditions` | policy Claim `rests_on` a narrower-scope Claim; scopes don't match |
| Ill-defined construct | `Construct.well_defined` | `= false` for a Construct under evaluation |
| Laundered conclusion | `origin.origin_type` | `= study-conclusion` on a Claim(role=assumption), never re-tested |
| Phantom origin | `origin.origin_type` | `∈ {none, misread}` |
| Foundational contradiction | `contradicts` | established fact contradicts an assumption below the Claim |
| Iatrogenic cascade | `substitution.real_world` | advice-Claim → harm-Claim edge exists |
| Assumption-coloring | two `Position.frame` | same Observation set, divergent verdict by frame |
| Animal-vs-human conflation | `rests_on` + `Observation.kind` | human Claim `rests_on` `mech-animal` with no human confirmation |

**All 16 are expressible with no new structural element** — the schema is complete
against the current catalogue. A future defect that *can't* be written as a row
here is the signal to extend the model.

## Implementation (deferred, but with a clear default)

Options, cheapest first:
1. **Structured JSON / files** — nodes and edges as records; good enough to build
   the first hierarchy by hand and run checks as scripts.
2. **Drupal custom entities + relation fields** — matches the Author Engine's
   existing stack (Drupal 10/11, decoupled-ready). *Recommended target:* Subject
   analysis and the Author Engine then **share infrastructure**, and an Actor's
   `author_engine_ref` is a real nested subproject, not a pointer to a separate
   system.
3. **Dedicated graph DB** — if traversal/scale demands it later.

Default path: model as a property graph (this doc), prototype in JSON, land on
Drupal entities to unify with the Author Engine.

## PM-model tie

- The **Subject** graph is a *Subproject* instance; each **Actor** node's
  Author-Engine pass is a *nested Subproject*.
- The **verdict computation, taint propagation, and each catalogue check** are
  **Skills** — invocable, trigger-driven, and the natural units of
  *promote-to-skill* (hand-run one check, then promote it).

## Open schema questions

1. **Confidence arithmetic** — how exactly do sufficiency caps, weakest-link, and
   partial taint combine into one `confidence`? (Ties to idea-doc Q3.)
2. **Granularity enforcement** — what forces a Claim/Construct to be precise
   enough (`granularity_ok`) before it can carry a verdict? (idea-doc Q1.)
3. **Quality scoring** — GRADE-style per kind, or bespoke? Who scores? (Q4.)
4. **Author-Engine handoff** — exact shape of what an Actor's engine pass returns
   into `Position`/`Actor`. (Q6.)
5. **Temporal model** — verdicts change as evidence arrives; do we version the
   graph so "what did the field believe in 1980 vs now" is queryable?
