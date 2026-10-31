# es-ES terminology audit — 2026-10-31

**46 strings checked, 31 concepts mapped. Findings: 1 term mismatch, 0 forbidden variants, 1 status change (vs. Aug 27 QA report), 7 availability issues. 1 target label proposed, 4 new-concept candidates submitted.**

First run — no `audit-baseline.json` existed, so status changes are compared against `.github/qa/qa-report.md` (2026-08-27) instead.

## Term match

- `onboarding.json:157 plan_features.punch_in_recording` — "Grabación con punch-in" vs approved term "grabación con Punch-In" (`feat_00000266`). Capitalisation of the anglicism differs; decide which is canonical and align either the string or the ontology.

## Forbidden variants

- None. Note: `validate_translation` scanned only 7 terms (the approved ones) and no es-es concept has forbidden or allowed variants defined yet, so this check cannot flag anything until variants are added in Black Ice.

## Status changes

- **Multitrack Recording** (`feat_00000004`) — `pending` → **`approved`**, term unchanged ("grabación multipista"). Affects `onboarding.json:153–155`. No string change needed.

## Market availability

- `onboarding.json:180 plan_features.comments_markers` — **Comment & Marker** (`feat_00000016`) is `not_available` in es-es but listed as a plan feature.
- `onboarding.json:179 plan_features.version_history` — **Version History** (`feat_00000017`) is `planned`.
- `onboarding.json:107 plan_selection.audience_tab_studio` — **Studio** line (`prod_00000002`) is `planned`.
- `onboarding.json:136 / 138 / 140 plans.studio_*_name` — **Studio Starter / Pro / Max** (`plan_00000004–6`) are `planned`.
- `onboarding.json:187 / 190 plan_features.feature_includes_studio_pro*` — upsell copy for `planned` Studio plans.

Unknown availability (`not_set`): Arrangement Timeline (`feat_00000267`), Scale Assistant (`feat_00000268`).

## Target labels proposed

- `feat_00000267` Arrangement Timeline → "línea de tiempo de arreglos" — applied as `pending` (`onboarding.json:152`).
- (test run earlier today) `feat_00000268` Scale Assistant → "asistente de escalas" — applied as `pending` (`onboarding.json:183`).
- Not proposed: Stem Separation (`feat_00000269`) has no es-es term but appears in no string.

## New-concept candidates

`added: 3`, `counted_as_repeats: 1`, `hidden_previously_rejected: 0`, `resurfaced_for_review: 0`, no errors.

- **AI Composition** (en-us, Feature) — es-ES "Composición con IA", 3 strings.
- **Sound Design** (en-us) — es-ES "Diseño de sonido", 2 strings. en-US `_notes` prefer the anglicism in ES, shipped es-ES translates it.
- **Metronome** (en-us, Feature) — es-ES "Metrónomo", 2 strings.
- **Key** (en-us) — es-ES "Tonalidad", 3 strings.
- Not submitted: "track"/"loop" — already governed by the market profile's terminology rules (pista).

## Other observations (outside the 4 checks)

- `onboarding.json:166 plan_features.mastering_chain` — market profile says "UI: master; docs: masterización", ontology term is "cadena de masterización" (pending). Profile and ontology disagree for UI surfaces.
- `en-US/onboarding.json` `_notes.style_transfer` says "Do not translate", but the Black Ice es-es term is the translated "transferencia de estilo" (pending), which es-ES follows.
- `onboarding.json:86 field_role_option_sound_designer` — "Diseño de sonido" renders a role ("Sound designer") as the discipline; likely should be "Diseñador/a de sonido".
