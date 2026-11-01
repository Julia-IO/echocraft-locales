# es-ES terminology audit — 2026-11-01

**50 mapped es-ES strings checked across 32 of 35 concepts (check_term on all 35; 0 have variants defined); all validated in `validate_translation` (50 distinct texts, 1 call): 0 forbidden, 0 info. Findings: 0 new term mismatch (1 carried over), 2 status changes, 1 English label change, 8 availability issue strings (unchanged). 0 target labels proposed, 7 candidates submitted (0 added, 7 repeats).**

## New since last audit

Black Ice reverted the Melody Generator rename. Main's baseline had `feat_00000010` as "Melody Composer" / "compositor de melodías"; it is now back to "Melody Generator" / "generador de melodías" (status `pending`, availability `available`). The three shipped strings use the current labels, so last audit's Melody Generator term mismatch is resolved.

- `feat_00000010` English label change: "Melody Composer" → "Melody Generator" (es-es term unchanged by us; see Status changes) — 3 strings
  - `dashboard:nav.melody_generator` (`locales/*/dashboard.json:15`)
    - en-US: "Melody Generator"
    - es-ES: "Generador de melodías"
  - `onboarding:plan_features.melody_generator` (`locales/*/onboarding.json:168`)
    - en-US: "Melody Generator"
    - es-ES: "Generador de melodías"
  - `sample:sample_strings.field_key_helper` (`locales/*/sample.json:12`)
    - en-US: "Choose the key your project is in — this sets the default scale for the melody generator."
    - es-ES: "Elige la tonalidad de tu proyecto: será la escala predeterminada del generador de melodías."

- `feat_00000010` es-es term change: "compositor de melodías" → "generador de melodías"; strings now match — 3 strings
  - `dashboard:nav.melody_generator` (`locales/*/dashboard.json:15`)
    - en-US: "Melody Generator"
    - es-ES: "Generador de melodías"
  - `onboarding:plan_features.melody_generator` (`locales/*/onboarding.json:168`)
    - en-US: "Melody Generator"
    - es-ES: "Generador de melodías"
  - `sample:sample_strings.field_key_helper` (`locales/*/sample.json:12`)
    - en-US: "Choose the key your project is in — this sets the default scale for the melody generator."
    - es-ES: "Elige la tonalidad de tu proyecto: será la escala predeterminada del generador de melodías."

Our proposal from last audit was applied:

- `feat_00000272` AI Composition es-es term: none → "composición con IA" (status `pending`, availability `not_set`) — 3 strings
  - `dashboard:nav.ai_composition` (`locales/*/dashboard.json:17`)
    - en-US: "AI Composition"
    - es-ES: "Composición con IA"
  - `dashboard:studio.ai_composition_label` (`locales/*/dashboard.json:130`)
    - en-US: "AI Composition"
    - es-ES: "Composición con IA"
  - `sample:sample_strings.track_type_midi_description` (`locales/*/sample.json:14`)
    - en-US: "Add a MIDI track when you want to program notes with the AI composition tools instead of recording live audio."
    - es-ES: "Añade una pista MIDI para programar notas con las herramientas de Composición con IA en vez de grabar audio en directo."

No new concepts, forbidden/info flags, term mismatches or availability findings.

## English label changes

- `feat_00000010`: "Melody Composer" → "Melody Generator" (retired labels now: "Melody Generator" is current again; "Melody Composer" retired). en-US strings use the current label, so no stale en-US strings. es-es term changed too: now "generador de melodías".

## Status changes

- `feat_00000010` es-es term "compositor de melodías" → "generador de melodías" — 3 strings
  - `dashboard:nav.melody_generator` (`locales/*/dashboard.json:15`)
    - en-US: "Melody Generator"
    - es-ES: "Generador de melodías"
  - `onboarding:plan_features.melody_generator` (`locales/*/onboarding.json:168`)
    - en-US: "Melody Generator"
    - es-ES: "Generador de melodías"
  - `sample:sample_strings.field_key_helper` (`locales/*/sample.json:12`)
    - en-US: "Choose the key your project is in — this sets the default scale for the melody generator."
    - es-ES: "Elige la tonalidad de tu proyecto: será la escala predeterminada del generador de melodías."

- `feat_00000272` es-es term none → "composición con IA" — 3 strings
  - `dashboard:nav.ai_composition` (`locales/*/dashboard.json:17`)
    - en-US: "AI Composition"
    - es-ES: "Composición con IA"
  - `dashboard:studio.ai_composition_label` (`locales/*/dashboard.json:130`)
    - en-US: "AI Composition"
    - es-ES: "Composición con IA"
  - `sample:sample_strings.track_type_midi_description` (`locales/*/sample.json:14`)
    - en-US: "Add a MIDI track when you want to program notes with the AI composition tools instead of recording live audio."
    - es-ES: "Añade una pista MIDI para programar notas con las herramientas de Composición con IA en vez de grabar audio en directo."

## Term match

- `feat_00000266` Punch-In Recording — es-ES "Grabación con punch-in" vs approved "grabación con Punch-In" (case only; carried over, unchanged) — 1 string
  - `onboarding:plan_features.punch_in_recording` (`locales/*/onboarding.json:157`)
    - en-US: "Punch-In Recording"
    - es-ES: "Grabación con punch-in"

Judgment call, not flagged: `dashboard:nav.chord_progression` "Progresiones de acordes" read as a short nav label for `feat_00000013`.

## Forbidden variants

None. 0 `forbidden`, 0 `info`. No concept has allowed/forbidden variants defined.

## Market availability

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

- `feat_00000267` Arrangement Timeline — 1 string
  - `onboarding:plan_features.arrangement_timeline` (`locales/*/onboarding.json:152`)
    - en-US: "Arrangement Timeline"
    - es-ES: "Línea de tiempo de arreglos"

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
- Branch note: remote branch `audit/es-ES-2026-11-01` already exists (merged in PR #32), so this run was pushed as `audit/es-ES-2026-11-01-b` (no force-push).

## Affected string IDs

```
dashboard:nav.ai_composition  feat_00000272  status-change
dashboard:nav.melody_generator  feat_00000010  label-change, status-change
dashboard:studio.ai_composition_label  feat_00000272  status-change
onboarding:plan_features.comments_markers  feat_00000016  availability
onboarding:plan_features.feature_includes_studio_pro  plan_00000004  availability
onboarding:plan_features.feature_includes_studio_pro_all  plan_00000005  availability
onboarding:plan_features.melody_generator  feat_00000010  label-change, status-change
onboarding:plan_features.punch_in_recording  feat_00000266  term-match
onboarding:plan_features.version_history  feat_00000017  availability
onboarding:plan_selection.audience_tab_studio  prod_00000002  availability
onboarding:plans.studio_max_name  plan_00000006  availability
onboarding:plans.studio_pro_name  plan_00000005  availability
onboarding:plans.studio_starter_name  plan_00000004  availability
sample:sample_strings.field_key_helper  feat_00000010  label-change, status-change
sample:sample_strings.track_type_midi_description  feat_00000272  status-change
```
