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

## Foundations to test first (bottom-up queue)

Per "evaluate bottom-up," these are where the leverage is:

| Node | Foundation | Kind | Why first |
| :-- | :-- | :-- | :-- |
| ★ F4 | DNL produces saturated fat endogenously | mechanistic | cross-cuts M3 **and** T1; one determination settles the conflation |
| ★ F5 | carbohydrate-induced hypertriglyceridemia | interventional/mech | directly tests M4's "carbs are safe" leap |
| ★ F6 | fructose / uricase metabolism | mechanistic | taints any study assuming glucose-like handling |
| ★ F1 | atherosclerosis mechanism (LDL infiltration) | mechanistic | the base of the whole lipid hypothesis |

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
- **Coverage is partial.** Salt, red/processed meat, fibre, seed oils, and the
  energy-balance vs carbohydrate-insulin debate under T4 are not yet mapped.
