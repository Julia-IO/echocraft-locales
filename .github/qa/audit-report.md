# es-ES terminology audit — 2026-10-31

**~46 es-ES strings checked, 31 mapped concepts. Findings: 1 term mismatch, 0 forbidden variants, 0 status changes, 7 availability issues. 0 target labels proposed, 8 new-concept candidates submitted.**

## Term match

- `locales/es-ES/onboarding.json:157 plan_features.punch_in_recording` — "Grabación con punch-in" vs approved "grabación con Punch-In" (`feat_00000266`). Capitalisation of the anglicism differs; align string or ontology. (Unchanged since last audit.)

## Forbidden variants

- None. `validate_translation` scanned 7 terms per call; no es-es concept has allowed/forbidden variants defined, so it cannot flag anything. Spot-checked 7 strings (Punch-In, MIDI Editor, Multitrack, Effects Rack, MP3 Export, Comment & Marker, Chord Progression Generator): no flags. The remaining mapped strings were not individually validated (no variants exist to match).

## Status changes

- None vs `.github/qa/audit-baseline.json` (32 concepts; term, status and availability all identical).

## Market availability

- `onboarding.json:180 plan_features.comments_markers` — Comment & Marker (`feat_00000016`) is `not_available` but listed as plan feature.
- `onboarding.json:179 plan_features.version_history` — Version History (`feat_00000017`) is `planned`.
- `onboarding.json:107 plan_selection.audience_tab_studio` — Studio (`prod_00000002`) is `planned`.
- `onboarding.json:136/138/140 plans.studio_*_name` — Studio Starter/Pro/Max (`plan_00000004–6`) are `planned`.
- `onboarding.json:186/187/190 plan_features.feature_includes_studio_*` — upsell copy for `planned` Studio plans.

Unknown availability (`not_set`): Arrangement Timeline (`feat_00000267`), Scale Assistant (`feat_00000268`).

## Target labels proposed

- None. Only concept without an es-es term is Stem Separation (`feat_00000269`), which appears in no string.

## New-concept candidates

Response: `added: 1`, `counted_as_repeats: 4`, `hidden_previously_rejected: 3`, `resurfaced_for_review: 0`, no errors. (Per-term breakdown not returned.)

- AI Composition — "Composición con IA", 3
- Sound Design — "Diseño de sonido", 3
- Metronome — "Metrónomo", 2
- Key — "Tonalidad", 4
- Drum Pattern Generator — "Generador de patrones de batería", 2
- Audio Comping — "Comping de audio", 1
- Chord Explorer — "Explorador de acordes", 1
- Interactive Lessons — "Lecciones interactivas", 1

## Other observations

- `onboarding.json:86 field_role_option_sound_designer` — "Diseño de sonido" names the discipline, not the role ("Sound designer").
- `onboarding.json:166 plan_features.mastering_chain` — market profile says "UI: master", ontology term is "cadena de masterización".
- `onboarding.json:196` en-US note says Style Transfer "Do not translate"; ontology es-es term is translated and es-ES follows it.
