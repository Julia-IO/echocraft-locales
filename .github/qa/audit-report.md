# es-ES terminology audit — 2026-11-01

**~58 es-ES strings checked (49 validated in batch), 32 concepts mapped of 35 (check_term on all 35; 0 have variants defined). Findings: 1 term mismatch (new) + 1 carried over, 0 forbidden, 1 status change, 1 English label change, 7 availability issues. 1 target label proposed, 7 candidates submitted.**

## New since last audit

- **English label change + es-es term change:** `feat_00000010` "Melody Generator" → "Melody Composer"; es-es term "generador de melodías" → "compositor de melodías" (status `pending`, availability `available`).
- **New concepts:** `feat_00000270` Smart Mix Assistant, `feat_00000271` Lyric Assistant, `feat_00000272` AI Composition (no es-es term; none of the first two appear in any string).
- **Term mismatch:** Melody Generator strings (below), a consequence of the rename.
- **Target label proposed:** AI Composition → "composición con IA" (was a candidate last audit; now a concept).
- AI Composition removed from candidates (now a concept).

## English label changes

- `feat_00000010`: "Melody Generator" → "Melody Composer". es-es term changed too (see Status changes). Stale en-US keys still using the old label:
  - `locales/en-US/onboarding.json:168 plan_features.melody_generator`
  - `locales/en-US/dashboard.json:15 nav.melody_generator`
  - `locales/en-US/sample.json:12 field_key_helper` ("melody generator")
  - Also mentioned in notes at `dashboard.json:136`, and in Creator Pro / Studio Pro / AI Composition concept definitions in Black Ice.

## Status changes

- `feat_00000010` es-es term: "generador de melodías" → "compositor de melodías" (status `pending` and availability `available` unchanged). Affected keys: the three below.

## Term match

- NEW `locales/es-ES/onboarding.json:168 plan_features.melody_generator` — "Generador de melodías" vs "compositor de melodías" (`feat_00000010`).
- NEW `locales/es-ES/dashboard.json:15 nav.melody_generator` — "Generador de melodías" vs "compositor de melodías".
- NEW `locales/es-ES/sample.json:12 field_key_helper` — "generador de melodías" vs "compositor de melodías".
- `locales/es-ES/onboarding.json:157 plan_features.punch_in_recording` — "Grabación con punch-in" vs approved "grabación con Punch-In" (`feat_00000266`). Unchanged since last audit.
- Judgment call, not flagged: `dashboard.json:16 nav.chord_progression` "Progresiones de acordes" read as a short nav label for `feat_00000013`.

## Forbidden variants

- None. 49 strings validated in one `validate_translation` call: 0 forbidden, 0 info flags. No concept has variants defined, so none could be flagged.

## Market availability

Unchanged since last audit:
- `onboarding.json:180 plan_features.comments_markers` — Comment & Marker (`feat_00000016`) is `not_available`.
- `onboarding.json:179 plan_features.version_history` — Version History (`feat_00000017`) is `planned`.
- `onboarding.json:107 plan_selection.audience_tab_studio` — Studio (`prod_00000002`) is `planned`.
- `onboarding.json:136/138/140 plans.studio_*_name` — Studio Starter/Pro/Max are `planned`.
- `onboarding.json:186/187/190 plan_features.feature_includes_studio_*` — upsell copy for `planned` Studio plans.

Unknown availability (`not_set`/null): Arrangement Timeline (`feat_00000267`), Scale Assistant (`feat_00000268`), AI Composition (`feat_00000272`, used at `dashboard.json:17/130`).

## Target labels proposed

- `feat_00000272` AI Composition → "composición con IA" — `applied` (id 9178e172-c54d-4e1b-a304-f575b3dd1609); shipped at `dashboard.json:17`, `dashboard.json:130`, `sample.json:14`.
- Stem Separation (`feat_00000269`), Smart Mix Assistant (`feat_00000270`), Lyric Assistant (`feat_00000271`): no es-es term, appear in no string — nothing proposed.

## New-concept candidates

Response: `added: 0`, `counted_as_repeats: 7`, `hidden_previously_rejected: 0`, `resurfaced_for_review: 0`, no errors.

- Sound Design — "Diseño de sonido", 3
- Metronome — "Metrónomo", 2
- Key — "Tonalidad", 4
- Drum Pattern Generator — "Generador de patrones de batería", 2
- Audio Comping — "Comping de audio", 1
- Chord Explorer — "Explorador de acordes", 1
- Interactive Lessons — "Lecciones interactivas", 1

## Other observations (carried over)

- `onboarding.json:86 field_role_option_sound_designer` — "Diseño de sonido" names the discipline, not the role.
- `onboarding.json:166 plan_features.mastering_chain` — market profile says "UI: master"; ontology term is "cadena de masterización".
- `onboarding.json:196` en-US note says Style Transfer "Do not translate"; ontology es-es term is translated.
- es-es term for Melody Composer is the terminologist's call; es-ES strings not edited.
