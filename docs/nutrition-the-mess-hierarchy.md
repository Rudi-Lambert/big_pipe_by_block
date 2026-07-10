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

## Branch H — fibre / whole grains (epi-vs-RCT + bundling)

```
T7  Fibre / whole grains prevent CHD and colorectal cancer
 └─rests on─ M12 observational: whole-grain eaters are healthier
              [kind: epidemiological]  [defect? confounding — healthy-user bias, as in Branch F]
 └─rests on─ M13 "it is the fibre doing the work"
              [defect? conflated entity — "whole grain" bundles fibre + replacing refined carbs + healthy-user;
                        the variables were never separated]
              └─contradicted by─ RCTs for colorectal adenoma (Polyp Prevention, Wheat-Bran Fiber): null
                                 [kind: interventional — epidemiology said yes, RCT said no]
              └─weak support─ F13 colonic fermentation → short-chain fatty acids  [kind: mechanistic — real but modest]
```

## Branch I — protein (a scope + overgeneralisation case)

```
Claim  "High protein damages the kidneys" → limit protein
 └─rests on─ M14 protein load raises glomerular filtration
              [defect? overgeneralised scope — harm shown in PRE-EXISTING kidney disease, generalised to healthy people]
              └─scope condition─ applies to established CKD, not demonstrated in healthy kidneys

Cross-link  protein's satiety / thermic effect (F14, mechanistic) feeds Branch D (obesity);
            "animal vs plant protein" overlaps Branch F.
```

## Branch J — meal timing / fasting (mechanism-vs-myth + confounding)

```
Claim-a  "Breakfast is the most important meal"
 └─rests on─ M15 breakfast-eaters weigh less (observational)
              [defect? confounding — breakfast-skippers differ systematically; RCTs show weak/no causal effect]
Claim-b  "Eat frequent small meals to stoke metabolism"
 └─contradicted by─ F15 thermic effect of food is proportional to TOTAL intake, not meal frequency  [mechanistic]
Claim-c  "Intermittent fasting / TRE helps beyond calorie restriction"
 └─open─ isocaloric RCTs mixed — is there a timing effect INDEPENDENT of total calories?
          [ties directly to Branch D: energy-balance vs substrate/hormonal framing]
```

## Branch K — micronutrient supplements (the isolate-and-supplement failure)

```
Pattern  food rich in nutrient N ↔ health  ⟹  supplement isolated N  ⟹  RCT fails or HARMS
 └─exhibit 1─ β-carotene: observational (carotenoid-rich diet ↔ less lung cancer)
              → supplement trials (ATBC, CARET) INCREASED lung cancer in smokers   [kind: interventional — harm]
 └─exhibit 2─ vitamin E, antioxidant supplements: null / harm in RCTs
 [defect? reductionist isolation — a WHOLE-FOOD association attributed to one component stripped of its matrix;
          also surrogate-vs-outcome, and a route/dose cousin of the vitamin-C faux-replication case]
```

## Branch L — microbiome (tests the animal-vs-human mechanism question)

```
Claim  gut microbiome composition causes obesity / metabolic disease
 └─rests on─ F16 germ-free-mouse transplant transfers the phenotype  [kind: mechanistic — but ANIMAL]
              [defect? animal-mechanism → human extrapolation — treats an animal determination as if human-dispositive]
 └─mostly─ M16 human associations (composition ↔ disease)  [kind: epidemiological — causal direction unresolved]
```

Branch L is the map's clearest case that **"mechanistic" must split into
animal vs human** (open question Q2): a germ-free-mouse result is a real
determination, but it is *not* the same currency as a human one. Its sufficiency
rule differs, and treating the two as interchangeable is itself a defect.

## Branch M — trans fats (a POSITIVE CONTROL + iatrogenic cascade)

```
T8  Trans fats cause heart disease
 ├─rests on─ F17 mechanism: trans fat raises LDL, lowers HDL, promotes inflammation  [kind: mechanistic, human]
 ├─rests on─ M17 consistent epidemiology                                            [kind: epidemiological]
 └─converges with─ intervention/removal → outcomes improved                          [kind: interventional/policy]
 [status: SURVIVES bottom-up evaluation — evidence agrees across all three kinds. This is a POSITIVE CONTROL.]

Iatrogenic cascade (cross-branch):
  T1/T2 "avoid butter / saturated fat"  ─drove─▶  recommend margarine (partially hydrogenated)  ─caused─▶  T8 harm
  [a defect in one branch produced a real-world substitution whose harm is mapped in another]
```

Branch M matters twice over: it's the map's clearest **positive control** (a claim
that *should* stand), and it introduces the **iatrogenic cascade** — the mess is
not only wrong beliefs but wrong beliefs that *drove substitutions* with their own
consequences. The anti-saturated-fat advice actively pushed trans fats.

## Branch N — omega-3 (isolate-and-supplement + a questioned origin)

```
Claim  fish-oil / omega-3 supplements prevent CHD
 └─origin─ F18 "Greenland Inuit have low CVD" (Bang & Dyerberg, 1970s)
            [defect? laundered conclusion / weak-origin — the founding epidemiology was later questioned
                     (Inuit CVD rates may not have been low; poorly documented) yet propagated for decades]
 └─rests on─ M18 supplement the isolated nutrient   [defect? reductionist isolation — fish vs a fish-oil pill]
              └─contradicted by─ large supplement RCTs largely null (VITAL, ASCEND);
                                 one high-dose EPA trial positive but placebo-confound disputed  [kind: interventional]
```

## Branch O — alcohol (reference-group contamination)

```
Claim  moderate drinking protects the heart (the J-curve)
 └─rests on─ M19 observational: moderate drinkers outlive abstainers
              [defect? sick-quitter / abstainer bias — the "non-drinker" reference group is contaminated with
                       former drinkers who quit BECAUSE they were ill; this manufactures the J-curve]
              └─tension─ Mendelian-randomisation & reanalyses suggest little/no cardioprotection  [kind: genetic/epi]
 └─against─ F19 alcohol (acetaldehyde) is a carcinogen  [kind: mechanistic, human — well supported]
```

A specific, nameable variant of confounding: **reference-group contamination** —
the comparison baseline is not clean. Distinct enough from generic healthy-user
bias to track separately.

## Branch P — artificial sweeteners (reverse causation)

```
Claim  artificial sweeteners cause weight gain / metabolic harm
 └─rests on─ M20 observational: sweetener use ↔ obesity
              [defect? REVERSE CAUSATION — already-heavier people switch TO diet products; the arrow runs backwards]
 └─rests on─ F20 mouse microbiome → glucose intolerance   [kind: mechanistic, ANIMAL — extrapolation risk (cf. Branch L)]
              └─human RCTs mixed
```

New signature: **reverse causation** — direction of the arrow assumed wrong.
Related to but distinct from confounding (there a third variable; here the effect
is mistaken for the cause).

## Branch Q — ultra-processed food (an ill-defined-construct case)

```
Claim  ultra-processed food (UPF) causes overeating and disease
 ├─support─ F21 metabolic-ward RCT: UPF diet → spontaneous overeating & weight gain  [kind: interventional — notable]
 └─weakness─ M21 "UPF" as an exposure variable
              [defect? ill-defined construct — NOVA bundles heterogeneous foods/mechanisms into one category;
                       you cannot cleanly evaluate a claim whose exposure is a fuzzy bundle]
              [also confounding in the observational arm — UPF eaters differ systematically]
```

New signature: **ill-defined construct** — the exposure itself is not crisply
defined, so every downstream result inherits the ambiguity. This is the
claim-granularity problem (open Q1) showing up at the level of the *exposure
variable*, not the conclusion.

## Branch R — hydration "8 glasses a day" (a phantom origin)

```
Claim  everyone should drink 8 glasses of water a day ("8×8")
 └─trace provenance─▶  no identifiable supporting study; commonly traced to a 1945 note that
                        also said most water comes from food — i.e. the source, read in full, does NOT support it
 [defect? PHANTOM ORIGIN — the provenance trace hits a dead end or a misreading; an axiom with no support beneath it]
```

The minimal, purest **provenance failure**: run "where did this come from?" and the
chain terminates in nothing (or in a misread source). The extreme case of a
laundered conclusion — laundered from *no* conclusion at all.

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

5. **Healthy-user confounding** — the single most pervasive defect in the map:
   meat (F), whole grains (H), breakfast (J) all lean on observational cohorts
   where the exposed and unexposed differ systematically (smoking, exercise, SES).
   It's "mislocated cause" specialised to nutritional epidemiology, and it recurs
   so often it may deserve its own named entry.
6. **Reductionist isolation** — a whole-food (or whole-context) association
   attributed to one isolated component: β-carotene the pill vs carotenoids in
   food (K), "the fibre" vs the whole grain (H). Appears twice → catalogue-ready.
7. **Animal-vs-human mechanism conflation** — germ-free-mouse results (L) treated
   as human-dispositive; the general form of open question Q2 about splitting the
   "mechanistic" evidence-kind.

8. **Reverse causation** (sweeteners P) — the arrow assumed backwards; distinct
   from confounding.
9. **Reference-group contamination** (alcohol O) — the comparison baseline is
   dirty (sick-quitters); a specific, nameable confounding variant.
10. **Ill-defined construct** (UPF Q) — the exposure variable is a fuzzy bundle,
    so results inherit the ambiguity; claim-granularity (Q1) at the exposure level.
11. **Phantom origin** (hydration R) — the provenance trace terminates in nothing
    or a misread source; the extreme of laundered conclusion.
12. **Iatrogenic cascade** (trans fats M) — a defect in one branch drove a
    real-world substitution whose harm surfaces in another. Not a reasoning error
    inside a study but a *causal link between branches*, so it attaches to the
    dependency graph itself.

New catalogue candidates surfaced by enrichment: **surrogate-vs-outcome
substitution**, **overgeneralised scope**, **assumption-coloring**, **healthy-user
confounding**, **reductionist isolation**, **animal-vs-human mechanism
conflation**, **reverse causation**, **reference-group contamination**,
**ill-defined construct**, **phantom origin**, **iatrogenic cascade** — each
earned by appearing on real content.

## Positive controls (a neutrality safeguard)

A map that only ever finds defects is indistinguishable from a contrarian
confirmation machine — and would rightly be distrusted. The framework's
credibility depends on **claims that survive evaluation** appearing alongside the
ones that fall. So far the map's **positive controls** are:

- **Trans fats → CHD (Branch M)** — evidence converges across mechanistic,
  epidemiological, and interventional kinds; it *should* stand.
- **Atherosclerosis LDL-infiltration mechanism (F1)** — a foundation that, tested
  bottom-up, is expected to hold even where claims built loosely on top of it do
  not.

Design consequence: the model must be able to render a **verdict of "supported"**
as confidently as a verdict of "unsupported," and every branch should be asked
"could this survive?" — not just "where does it break?" Positive controls are how
we keep the tool honest and detect if it has become biased toward debunking.

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
- **Coverage is now wide (A–R).** Eighteen branches span the major fat, cholesterol,
  obesity, salt, meat, fibre, protein, timing, supplement, microbiome, alcohol,
  sweetener, UPF, and hydration disputes — plus a positive control (trans fats).
  Genuinely diminishing returns now; remaining gaps (specific micronutrients,
  glycaemic index, meal-pattern variants) are unlikely to add *new* signatures.
- **Eleven catalogue candidates** now stand ready — the original six plus reverse
  causation, reference-group contamination, ill-defined construct, phantom origin,
  and iatrogenic cascade. Each has real-content backing, so by our "earn it by
  recurrence / real example" rule they're ready to promote into
  `subject-analysis-idea.md`'s catalogue.
- **The map now includes positive controls**, not only defects — a deliberate
  neutrality safeguard (see that section).
