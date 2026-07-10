# Nutrition — "The Mess": First Hierarchy Sketch

*Instance #1 content · v0.1 · **CANDIDATE map**, drawn from general knowledge and
**unsourced**. This is a scaffold to verify, not a set of verdicts. It maps the
**structure** of the debate; it does not adjudicate it. Every node needs a
citation before any verdict, and orthodox and contrarian claims appear here as
peers — inclusion is not endorsement.*

> Purpose: give the framework in `subject-analysis-idea.md` one real hierarchy to
> run against, and see whether the objects, evidence-kinds, and defect map earn
> their keep on actual content.

## How to read this

- **Layers:** `T` top-level conclusions / policy → rest on `M` mid-level claims →
  rest on `F` foundations (mechanisms, definitions, raw data).
- **`rests on`** = the dependency edge. Discover top-down; evaluate bottom-up.
- **`[defect?]`** = a catalogue failure mode *alleged* to attach here — a place to
  check, not a proven error.
- **★** = load-bearing foundation to test first.

## Top-level claims (what policy asserts)

- **T1** — Limit saturated fat to prevent heart disease.
- **T2** — Eat a low-fat, carbohydrate-based diet (the guideline era).
- **T3** — Dietary cholesterol is dangerous. *(note: largely walked back in the
  2015 US guidelines — a top-level claim that already fell; a useful calibration
  case for the model.)*
- **T4** — Obesity is calories-in / calories-out; a calorie is a calorie.
- **T5** — Salt causes hypertension; everyone should cut salt.
- **T6** — Red / processed meat causes cancer and heart disease.
- **(corollary)** — Replace saturated fat with polyunsaturated seed oils to lower
  CHD. *(rides on T1/T2; mapped as Branch G.)*

## Branch A — saturated fat → heart disease (most developed)

```
T1  Limit saturated fat to prevent heart disease
 │
 ├─rests on─ M1  High blood LDL/cholesterol causes atherosclerosis   (the lipid hypothesis)
 │            ├─rests on─ F1 ★ mechanism of atherosclerosis (LDL infiltration)      [kind: mechanistic]
 │            └─rests on─ F2   observational epidemiology: cholesterol ↔ CHD        [kind: epidemiological]
 │
 ├─rests on─ M2  Eating saturated fat raises blood LDL
 │            └─rests on─ F3   controlled metabolic-ward feeding data                [kind: interventional]
 │
 └─rests on─ M3  The harmful fat is DIETARY in origin        [defect? conflated / unseparated sources]
              └─contradicted by─ F4 ★ de novo lipogenesis makes saturated fat ENDOGENOUSLY (carbs → palmitate)

Origin / provenance:
  Seven Countries Study (Keys, 1950s–60s), 1977 Dietary Goals, 1980 Guidelines
  [defect? laundered conclusion — an interpretation promoted to axiom]
  [overlay: provenance spine — this is the transmission origin for much of T1/T2]

Tension (evidence pointing the other way):
  Direct sat-fat → CHD link "hard to make": Minnesota Coronary / Sydney Diet-Heart
  reanalyses, and meta-analyses reporting weak association   [kind: interventional + meta]
```

## Branch B — low-fat / high-carb guideline

```
T2  Eat a low-fat, carbohydrate-based diet
 ├─rests on─ T1 (above)
 └─rests on─ M4  Replacing dietary fat with carbohydrate is safe/beneficial   [defect? mislocated cause]
              └─contradicted by─ F5 ★ carbohydrate-induced hypertriglyceridemia (excess carbs → raised triglycerides)
              └─rests on─       F6 ★ sugar/fructose metabolism (fructokinase unregulated; uricase lost)
                                     [taint: studies assuming fructose is handled like glucose are downstream of F6]
```

## Branch C — dietary cholesterol (a *resolved* case: calibration)

```
T3  Dietary cholesterol is dangerous            [status: field reversed it — 2015 guidelines dropped the limit]
 └─rests on─ M5  Eating cholesterol raises blood cholesterol   [defect? conflated / unseparated sources]
              └─contradicted by─ F7 ★ most blood cholesterol is SYNTHESISED endogenously (hepatic),
                                        dietary intake is minor and homeostatically down-regulated
```

Why this branch matters most as a **test**: the field *already* reached the
verdict the framework should reproduce. The defect is the **same** as Branch A's
M3 — conflating an endogenously-produced substance with its dietary source. If
the model can rediscover the 2015 reversal from F7 alone, that's evidence the
machinery works. (See "Cross-branch patterns.")

## Branch D — obesity: two competing top-level frames

```
T4  Obesity is calories-in / calories-out
 ├─rests on─ F8   conservation of energy                       [kind: definitional/physical — unassailable]
 └─rests on─ M6   "a calorie is a calorie" — all calories are metabolically equivalent for fat storage & appetite
                   [defect? mislocated level — F8 is true, but M6 is the contested LEAP, not F8]

Competing frame:  Carbohydrate–Insulin Model (CIM)
 └─rests on─ F9   insulin drives lipogenesis / suppresses lipolysis   [kind: mechanistic]

"Eat less, move more" advice
 └─rests on─ M7   a sustained voluntary energy deficit is achievable
                   [defect? ignores F10 ★ adaptive thermogenesis — the body lowers expenditure to defend weight]
```

Note the *assumption-coloring* hazard: the same trial data get read as supporting
whichever frame (T4 vs CIM) the analyst already holds. That's an **assumption
shaping interpretation**, not evidence deciding between them — a thing the model
must flag rather than resolve.

## Branch E — salt (a scope-conditions case)

```
T5  Everyone should cut salt
 ├─rests on─ M8  high salt raises blood pressure
 │            └─rests on─ F11 renal sodium handling            [kind: mechanistic — but effect is population-variable]
 └─rests on─ M9  cutting salt lowers CVD events for EVERYONE   [defect? overgeneralised scope]
              └─scope condition─ effect concentrated in salt-SENSITIVE individuals
              └─tension─ J-curve: both very-low AND very-high intake associated with risk   [kind: epidemiological]
```

This is the cleanest **scope-conditions** exemplar in the map: a real effect in a
subgroup ("raises BP *when* salt-sensitive") extended to a universal mandate. The
scope condition is the whole disagreement.

## Branch F — red / processed meat (an evidence-kind-mismatch case)

```
T6  Red/processed meat causes cancer and CHD
 └─rests on─ M10 observational associations (e.g. processed-meat cancer classification)
              [kind: epidemiological — small relative risks (~1.1–1.3)]
              [defect? mislocated cause / confounding — healthy-user bias: meat-avoiders differ in smoking, exercise, SES]
              └─weak support─ F12 mechanistic candidates (heme iron, N-nitroso, TMAO)  [kind: mechanistic — proposed, contested]
              └─gap─ interventional (RCT) evidence sparse
```

The signature here: **policy-strength conclusions from weak observational
associations** — the exact kind/quality confusion the evidence typology exists to
catch. Small RRs in confounded nutritional epidemiology vs the certainty of the
public message.

## Branch G — seed oils / PUFA replacement (a faux-replication / selective-outcome case)

```
Corollary  Replace saturated fat with PUFA seed oils to lower CHD
 └─rests on─ M2 (sat fat raises LDL) + M11 "lowering LDL via PUFA lowers CHD events"
              └─contradicted by─ Minnesota Coronary Experiment & Sydney Diet-Heart:
                                  PUFA LOWERED cholesterol but did NOT lower (possibly raised) mortality
                                  [defect? selective outcome / delayed-unfavourable-data reporting]
                                  [kind: interventional (RCT) — the strongest evidence, pointing against M11]
```

Here the *intervention* worked on the surrogate (LDL) but not the endpoint
(death) — a surrogate-vs-outcome split that also stress-tests whether the model
distinguishes "moved a marker" from "helped a patient."

## Cross-branch patterns (recurring signatures)

Coverage reveals defects that repeat across branches — these are higher-order
findings the single-branch view can't see, and strong candidates for their own
catalogue status:

1. **Endogenous-vs-dietary conflation** — the *same* defect drives both the
   saturated-fat branch (F4, DNL makes it endogenously) **and** the cholesterol
   branch (F7, the liver synthesises most of it). A substance the body produces
   is blamed on its dietary source. Two independent branches, one signature →
   worth promoting to a named, searchable pattern.
2. **Epidemiology → policy over-reach** — weak observational associations (salt
   M9, meat M10, and arguably the original diet-heart epidemiology F2) converted
   into universal mandates. An evidence-**kind** failure, recurring.
3. **Surrogate-vs-outcome substitution** — LDL (Branch G), blood pressure
   (Branch E), cholesterol (Branch C) treated as if moving the marker equals
   helping the patient. A distinct defect the catalogue doesn't yet name.
4. **Assumption-coloring** — obesity data (Branch D) read through whichever frame
   is pre-held. Not a defect *in* a study but in how the field *interprets* a
   contested body of them.

New catalogue candidates surfaced by enrichment: **surrogate-vs-outcome
substitution**, **overgeneralised scope**, **assumption-coloring** — each earned
by appearing in more than one branch.

## Foundations to test first (bottom-up queue)

Per "evaluate bottom-up," these are where the leverage is:

| Node | Foundation | Kind | Why first |
| :-- | :-- | :-- | :-- |
| ★ F4 | DNL produces saturated fat endogenously | mechanistic | cross-cuts M3 **and** T1; one determination settles the conflation |
| ★ F7 | most blood cholesterol is synthesised endogenously | mechanistic | same signature as F4; should reproduce the 2015 reversal |
| ★ F5 | carbohydrate-induced hypertriglyceridemia | interventional/mech | directly tests M4's "carbs are safe" leap |
| ★ F6 | fructose / uricase metabolism | mechanistic | taints any study assuming glucose-like handling |
| ★ F1 | atherosclerosis mechanism (LDL infiltration) | mechanistic | the base of the whole lipid hypothesis |
| ★ F10 | adaptive thermogenesis | mechanistic | undercuts M7's "sustained deficit is achievable" |

F4 and F7 share a signature (endogenous synthesis) — settling *one* teaches the
check for the other. That is the cross-branch leverage the flat view misses.

**Notice:** three of the four highest-leverage foundations are **mechanistic** —
sufficiency by determination, not statistics. They're fast to settle and, per the
taint model, each can knock out large epidemiological branches sitting above it.
That's the "kind before quality" rule paying off on real content.

## What this sketch already demonstrates (the framework working)

- **Top-down discovery, bottom-up evaluation** produced a real queue (F4/F5/F6/F1).
- **Defects self-located** against the map with no new machinery: conflation on
  **M3**, mislocated cause on **M4**, laundered conclusion on the **Keys origin**.
- **Mechanistic foundations dominate leverage** — exactly what "kind before
  quality" predicted.
- **Reverse-taint candidate:** if the *direct* sat-fat → CHD link is genuinely
  weak (the "hard to make" tension), then T1 may be propped more by **propagation**
  than by **support** — the precise gap the two-questions design exists to expose.

## Caveats (load-bearing)

- **Unsourced.** Every node is a placeholder until it carries a citation.
- **No side taken.** Contrarian and orthodox claims are peers; the structure is
  the output, not a verdict.
- **Granularity is rough.** Several M-nodes will split (e.g. M1 bundles "LDL
  causes" with "total cholesterol correlates").
- **Coverage is broader but still partial.** Branches A–G now cover saturated
  fat, low-fat/high-carb, dietary cholesterol, obesity (energy-balance vs CIM),
  salt, red/processed meat, and seed-oil replacement. Still unmapped: fibre /
  whole grains, protein, micronutrients, meal timing / fasting, the microbiome.
- **New catalogue candidates** (surrogate-vs-outcome, overgeneralised scope,
  assumption-coloring) are noted but not yet written up in
  `subject-analysis-idea.md` — do that once each has a second independent example.
