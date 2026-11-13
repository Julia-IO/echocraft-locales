# es-ES terminology audit — 2026-11-09

**50 mapped es-ES strings checked across 32 of 35 concepts (check_term on all 35: 32 found, 3 without es-es term; 0 have variants defined); all validated in `validate_translation` (50 texts, 1 call): 0 forbidden, 0 info. Findings: 1 term mismatch (carried over), 2 status changes, 0 English label changes, 9 availability issue strings (2 new). 0 target labels proposed, 7 candidates submitted (0 added, 7 repeats).**

## New since last audit

- `feat_00000013` Chord Progression Generator: availability `available` → `planned` (es-es term "generador de progresiones de acordes", approved, unchanged). The feature is presented as part of the plan offer — 2 strings
  - `onboarding:plan_features.chord_progression_generator` (`locales/*/onboarding.json:169`)
    - en-US: "Chord Progression Generator"
    - es-ES: "Generador de progresiones de acordes"
  - `dashboard:nav.chord_progression` (`locales/*/dashboard.json:16`) — judgment call: short nav label read as this concept
    - en-US: "Chord Progression"
    - es-ES: "Progresiones de acordes"
- `feat_00000267` Arrangement Timeline: status `pending` → `approved`, availability `not_set` → `available` (es-es term unchanged: "línea de tiempo de arreglos"; string already matches) — 1 string
  - `onboarding:plan_features.arrangement_timeline` (`locales/*/onboarding.json:152`)
    - en-US: "Arrangement Timeline"
    - es-ES: "Línea de tiempo de arreglos"

## Resolved since last audit

- `feat_00000267` was listed under unknown availability (`not_set`); now `available`, so no longer an open item.

## Status changes

- `feat_00000013` availability `available` → `planned` — 2 strings (see above; also under Market availability)
- `feat_00000267` status `pending` → `approved`, availability `not_set` → `available` — 1 string (see above)

## Term match

- `feat_00000266` Punch-In Recording — es-ES "Grabación con punch-in" vs approved "grabación con Punch-In" (case only; carried over, unchanged) — 1 string
  - `onboarding:plan_features.punch_in_recording` (`locales/*/onboarding.json:157`)
    - en-US: "Punch-In Recording"
    - es-ES: "Grabación con punch-in"

## Forbidden variants

None. 0 `forbidden`, 0 `info`. No concept has allowed/forbidden variants defined.

## Market availability

- `feat_00000013` Chord Progression Generator (`planned`, new) — 2 strings
  - `onboarding:plan_features.chord_progression_generator` (`locales/*/onboarding.json:169`)
    - en-US: "Chord Progression Generator"
    - es-ES: "Generador de progresiones de acordes"
  - `dashboard:nav.chord_progression` (`locales/*/dashboard.json:16`)
    - en-US: "Chord Progression"
    - es-ES: "Progresiones de acordes"

Unchanged since last audit:

- `feat_00000016` Comment & Marker (`not_available`) — 1 string
  - `onboarding:plan_features.comments_markers` (`locales/*/onboarding.json:180`)
    - en-US: "Comments & Markers"
    - es-ES: "Comentarios y marcadores"
- `feat_00000017` Version History (`planned`) — 1 string
  - `onboarding:plan_features.version_history` (`locales/*/onboarding.json:179`)
    - en-US: "Version History"
    - es-ES: "Historial de versiones"
- `prod_00000002` Studio (`planned`) — 1 string
  - `onboarding:plan_selection.audience_tab_studio` (`locales/*/onboarding.json:107`)
    - en-US: "Studio"
    - es-ES: "Studio"
- `plan_00000004` Studio Starter (`planned`) — 2 strings
  - `onboarding:plans.studio_starter_name` (`locales/*/onboarding.json:136`)
    - en-US: "Studio Starter"
    - es-ES: "Studio Starter"
  - `onboarding:plan_features.feature_includes_studio_pro` (`locales/*/onboarding.json:187`)
    - en-US: "Everything in Studio Starter, plus:"
    - es-ES: "Todo lo incluido en Studio Starter y además:"
- `plan_00000005` Studio Pro (`planned`) — 2 strings
  - `onboarding:plans.studio_pro_name` (`locales/*/onboarding.json:138`)
    - en-US: "Studio Pro"
    - es-ES: "Studio Pro"
  - `onboarding:plan_features.feature_includes_studio_pro_all` (`locales/*/onboarding.json:190`)
    - en-US: "Everything in Studio Pro, plus:"
    - es-ES: "Todo lo incluido en Studio Pro y además:"
- `plan_00000006` Studio Max (`planned`) — 1 string
  - `onboarding:plans.studio_max_name` (`locales/*/onboarding.json:140`)
    - en-US: "Studio Max"
    - es-ES: "Studio Max"

Unknown availability (`not_set`), listed once:

- `feat_00000268` Scale Assistant — 1 string
  - `onboarding:plan_features.scale_assistant` (`locales/*/onboarding.json:183`)
    - en-US: "Scale Assistant"
    - es-ES: "Asistente de escalas"
- `feat_00000272` AI Composition — 3 strings
  - `dashboard:nav.ai_composition` (`locales/*/dashboard.json:17`)
    - en-US: "AI Composition"
    - es-ES: "Composición con IA"
  - `dashboard:studio.ai_composition_label` (`locales/*/dashboard.json:130`)
    - en-US: "AI Composition"
    - es-ES: "Composición con IA"
  - `sample:sample_strings.track_type_midi_description` (`locales/*/sample.json:14`)
    - en-US: "Add a MIDI track when you want to program notes with the AI composition tools instead of recording live audio."
    - es-ES: "Añade una pista MIDI para programar notas con las herramientas de Composición con IA en vez de grabar audio en directo."

## Target labels proposed

None. Concepts without an es-es term (`feat_00000269` Stem Separation, `feat_00000270` Smart Mix Assistant, `feat_00000271` Lyric Assistant) appear in no string. No strings affected.

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

- `onboarding:profile_setup.field_role_option_sound_designer` (`onboarding.json:86`): "Diseño de sonido" names the discipline, not the role.
- `onboarding:plan_features.mastering_chain` (`onboarding.json:166`): market profile says "UI: master"; ontology term is "cadena de masterización".
- `onboarding.json:196` en-US note says Style Transfer "Do not translate"; ontology es-es term is translated.
- Baseline housekeeping: `feat_00000010` `en_previous_terms` listed its current label "Melody Generator"; removed (current label is never retired).

## Affected string IDs

1. Needs a string fix
```
onboarding:plan_features.punch_in_recording  feat_00000266  term-match
```
2. Needs a product or terminology decision
```
dashboard:nav.chord_progression  feat_00000013  availability
onboarding:plan_features.chord_progression_generator  feat_00000013  availability
onboarding:plan_features.comments_markers  feat_00000016  availability
onboarding:plan_features.feature_includes_studio_pro  plan_00000004  availability
onboarding:plan_features.feature_includes_studio_pro_all  plan_00000005  availability
onboarding:plan_features.version_history  feat_00000017  availability
onboarding:plan_selection.audience_tab_studio  prod_00000002  availability
onboarding:plans.studio_max_name  plan_00000006  availability
onboarding:plans.studio_pro_name  plan_00000005  availability
onboarding:plans.studio_starter_name  plan_00000004  availability
```
3. Changed in Black Ice, strings already in sync
```
onboarding:plan_features.arrangement_timeline  feat_00000267  status-change
```
