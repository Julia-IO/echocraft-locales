# es-ES terminology audit — 2026-11-01

**~46 es-ES strings checked (39 validated), 31 mapped concepts. Findings: 2 term mismatches, 0 forbidden variants, 1 status change, 7 availability issues. 0 target labels proposed, 8 new-concept candidates submitted.**

## New since last audit

- **Term change in Black Ice:** Melody Generator (`feat_00000010`) es-es term changed from "generador de melodías" to "generador melodías" (status `pending`, availability `available` unchanged). The new term looks like a typo (missing "de"); es-ES strings still use "Generador de melodías". Likely an ontology error — terminologist should review rather than changing locale files.
- New term mismatch caused by the above (see Term match).

## Term match

- `locales/es-ES/onboarding.json:168 plan_features.melody_generator` — "Generador de melodías" vs ontology "generador melodías" (`feat_00000010`). **New.** Same wording in `dashboard.json:15 nav.melody_generator`.
- `locales/es-ES/onboarding.json:157 plan_features.punch_in_recording` — "Grabación con punch-in" vs approved "grabación con Punch-In" (`feat_00000266`). Capitalisation only. (Unchanged.)

## Forbidden variants

- None. 39 strings validated in one `validate_translation` call; no flags (`scanned: 7`). No `info` hits. Concepts have no allowed/forbidden variants defined.

## Status changes

- `feat_00000010` Melody Generator: term "generador de melodías" → "generador melodías". Affected keys: `onboarding.json:168`, `dashboard.json:15`, `sample.json:12` (inflected use in text).

## Market availability (unchanged)

- `onboarding.json:180 plan_features.comments_markers` — Comment & Marker (`feat_00000016`) is `not_available` but listed as plan feature.
- `onboarding.json:179 plan_features.version_history` — Version History (`feat_00000017`) is `planned`.
- `onboarding.json:107 plan_selection.audience_tab_studio` — Studio (`prod_00000002`) is `planned`.
- `onboarding.json:136/138/140 plans.studio_*_name` — Studio Starter/Pro/Max (`plan_00000004–6`) are `planned`.
- `onboarding.json:186/187/190 plan_features.feature_includes_studio_*` — upsell copy for `planned` Studio plans.

Unknown availability (`not_set`): Arrangement Timeline (`feat_00000267`), Scale Assistant (`feat_00000268`).

## Target labels proposed

- None. Only concept without an es-es term is Stem Separation (`feat_00000269`; `check_term` returns null), which appears in no string.

## New-concept candidates

Response: `added: 0`, `counted_as_repeats: 8`, `hidden_previously_rejected: 0`, `resurfaced_for_review: 0`, no errors.

- AI Composition — "Composición con IA", 3
- Sound Design — "Diseño de sonido", 3
- Metronome — "Metrónomo", 2
- Key — "Tonalidad", 4
- Drum Pattern Generator — "Generador de patrones de batería", 2
- Audio Comping — "Comping de audio", 1
- Chord Explorer — "Explorador de acordes", 1
- Interactive Lessons — "Lecciones interactivas", 1

## Other observations (unchanged)

- `onboarding.json:86` "Diseño de sonido" names the discipline, not the role "Sound designer".
- `onboarding.json:166` market profile says "UI: master", ontology term is "cadena de masterización".
- `onboarding.json:196` en-US note says Style Transfer "Do not translate"; ontology es-es term is translated and es-ES follows it.
