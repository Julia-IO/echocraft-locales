# es-ES terminology audit — 2026-11-23

**55 mapped es-ES strings checked across 24 of 37 concepts in strings (check_term on all 37: 36 with an es-es term, 1 without; 0 have variants defined); all 55 validated in `validate_translation` (1 call): 0 forbidden, 0 info. Findings: 1 term mismatch (carried over, case only), 16 status/availability changes, 0 English label changes, 0 availability issues. 0 target labels proposed, 8 candidates submitted (0 added, 5 repeats, 3 hidden as previously rejected).**

## New since last audit

Black Ice changes since the 2026-11-09 baseline (all es-es terms unchanged; every affected string already uses the current term):

- `feat_00000006` Piano Roll: status `pending` → `approved` (term "piano roll" unchanged; string already matches) — 1 string
  - `onboarding:plan_features.piano_roll` (`locales/*/onboarding.json:150`)
    - en-US: "Piano Roll"
    - es-ES: "Piano roll"
- `feat_00000013` Chord Progression Generator: availability `planned` → `available` (term unchanged) — 2 strings
  - `onboarding:plan_features.chord_progression_generator` (`locales/*/onboarding.json:169`)
    - en-US: "Chord Progression Generator"
    - es-ES: "Generador de progresiones de acordes"
  - `dashboard:nav.chord_progression` (`locales/*/dashboard.json:16`)
    - en-US: "Chord Progression"
    - es-ES: "Progresiones de acordes"
- `feat_00000016` Comment & Marker: availability `not_available` → `available` (term unchanged) — 1 string
  - `onboarding:plan_features.comments_markers` (`locales/*/onboarding.json:180`)
    - en-US: "Comments & Markers"
    - es-ES: "Comentarios y marcadores"
- `feat_00000017` Version History: availability `planned` → `available` (term unchanged) — 1 string
  - `onboarding:plan_features.version_history` (`locales/*/onboarding.json:179`)
    - en-US: "Version History"
    - es-ES: "Historial de versiones"
- `feat_00000019` Loudness Analyzer: status `pending` → `approved` (term unchanged) — 2 strings
  - `onboarding:plan_features.loudness_analyzer` (`locales/*/onboarding.json:167`)
    - en-US: "Loudness Analyzer"
    - es-ES: "Analizador de loudness"
  - `export:export.loudness_check_title` (`locales/*/export.json:17`)
    - en-US: "Loudness Analyzer"
    - es-ES: "Analizador de loudness"
- `feat_00000020` One-Click Distribution: status `pending` → `approved` (term unchanged) — 2 strings
  - `onboarding:plan_features.one_click_distribution` (`locales/*/onboarding.json:174`)
    - en-US: "One-Click Distribution"
    - es-ES: "Distribución con un clic"
  - `export:export.distribution_cta` (`locales/*/export.json:24`)
    - en-US: "Release with One-Click Distribution"
    - es-ES: "Distribuir con un clic"
- `feat_00000272` AI Composition: status `pending` → `approved`, availability `not_set` → `available` (term unchanged) — 3 strings
  - `dashboard:nav.ai_composition` (`locales/*/dashboard.json:17`)
    - en-US: "AI Composition"
    - es-ES: "Composición con IA"
  - `dashboard:studio.ai_composition_label` (`locales/*/dashboard.json:130`)
    - en-US: "AI Composition"
    - es-ES: "Composición con IA"
  - `sample:sample_strings.track_type_midi_description` (`locales/*/sample.json:14`)
    - en-US: "Add a MIDI track when you want to program notes with the AI composition tools instead of recording live audio."
    - es-ES: "Añade una pista MIDI para programar notas con las herramientas de Composición con IA en vez de grabar audio en directo."
- `plan_00000004` Studio Starter: availability `planned` → `available` — 2 strings
  - `onboarding:plans.studio_starter_name` (`locales/*/onboarding.json:136`)
    - en-US: "Studio Starter"
    - es-ES: "Studio Starter"
  - `onboarding:plan_features.feature_includes_studio_pro` (`locales/*/onboarding.json:187`)
    - en-US: "Everything in Studio Starter, plus:"
    - es-ES: "Todo lo incluido en Studio Starter y además:"
- `plan_00000005` Studio Pro: availability `planned` → `available` — 2 strings
  - `onboarding:plans.studio_pro_name` (`locales/*/onboarding.json:138`)
    - en-US: "Studio Pro"
    - es-ES: "Studio Pro"
  - `onboarding:plan_features.feature_includes_studio_pro_all` (`locales/*/onboarding.json:190`)
    - en-US: "Everything in Studio Pro, plus:"
    - es-ES: "Todo lo incluido en Studio Pro y además:"
- `plan_00000006` Studio Max: availability `planned` → `available` — 1 string
  - `onboarding:plans.studio_max_name` (`locales/*/onboarding.json:140`)
    - en-US: "Studio Max"
    - es-ES: "Studio Max"
- `prod_00000002` Studio: availability `planned` → `available` — 1 string
  - `onboarding:plan_selection.audience_tab_studio` (`locales/*/onboarding.json:107`)
    - en-US: "Studio"
    - es-ES: "Studio"
- `feat_00000269` Stem Separation: es-es term null → "separación de stems" (approved, availability `not_set`) — 0 strings
  - No strings affected.
- `feat_00000270` Smart Mix Assistant: es-es term null → "asistente de mezcla inteligente" (pending, `not_set`) — 0 strings
  - No strings affected.
- `feat_00000271` Lyric Assistant: es-es term null → "asistente de letras" (pending, `not_set`) — 0 strings
  - No strings affected.
- `feat_00000273` Stem Export: **new concept** (es-es "exportación de stems", pending, `not_set`) — 3 strings use it
  - `export:export.stems_option` (`locales/*/export.json:20`)
    - en-US: "Export stems"
    - es-ES: "Exportar stems"
  - `export:export.stems_count_singular` (`locales/*/export.json:21`)
    - en-US: "{count} stem ready"
    - es-ES: "{count} stem listo"
  - `export:export.stems_count_plural` (`locales/*/export.json:22`)
    - en-US: "{count} stems ready"
    - es-ES: "{count} stems listos"
  - Note: strings use the verb form "Exportar stems" / "stem(s) listo(s)"; the term is the noun "exportación de stems". Judged not a mismatch; terminologist may confirm.
- `feat_00000274` Freeze Track: new concept, no es-es term yet (null) — No strings affected. Nothing proposed.
- `feat_00000275` Tempo Map: new concept ("mapa de tempo", approved, `not_set`) — No strings affected (its Black Ice note references a `mix_tools` namespace that does not exist in `locales/`).
- `feat_00000268` Scale Assistant: **no longer in the Black Ice ontology** (was "asistente de escalas", pending). Now ungoverned; resubmitted as a new-concept candidate — 1 string
  - `onboarding:plan_features.scale_assistant` (`locales/*/onboarding.json:183`)
    - en-US: "Scale Assistant"
    - es-ES: "Asistente de escalas"

## Resolved since last audit

All availability findings from the previous report are resolved because Black Ice availability changed to `available` (not a string edit):

- `feat_00000013` Chord Progression Generator (was `planned`): `onboarding:plan_features.chord_progression_generator`, `dashboard:nav.chord_progression`
- `feat_00000016` Comment & Marker (was `not_available`): `onboarding:plan_features.comments_markers`
- `feat_00000017` Version History (was `planned`): `onboarding:plan_features.version_history`
- `prod_00000002` Studio (was `planned`): `onboarding:plan_selection.audience_tab_studio`
- `plan_00000004` Studio Starter (was `planned`): `onboarding:plans.studio_starter_name`, `onboarding:plan_features.feature_includes_studio_pro`
- `plan_00000005` Studio Pro (was `planned`): `onboarding:plans.studio_pro_name`, `onboarding:plan_features.feature_includes_studio_pro_all`
- `plan_00000006` Studio Max (was `planned`): `onboarding:plans.studio_max_name`
- Unknown-availability list: `feat_00000272` AI Composition is now `available`; `feat_00000268` Scale Assistant left the ontology (see above).
- Candidate "Interactive Lessons" etc. are unchanged (see candidates).

## Status changes

See "New since last audit" — 14 concept changes plus 1 removed concept, each with affected strings listed there.

## Term match

- `feat_00000266` Punch-In Recording — es-ES "Grabación con punch-in" vs approved "grabación con Punch-In" (case only; carried over, unchanged) — 1 string
  - `onboarding:plan_features.punch_in_recording` (`locales/*/onboarding.json:157`)
    - en-US: "Punch-In Recording"
    - es-ES: "Grabación con punch-in"

## Forbidden variants

None. 55 strings validated: 0 `forbidden`, 0 `info`. No concept has allowed/forbidden variants defined.

## Market availability

No `not_available` or `planned` concepts remain in the strings.

Unknown availability (`not_set`), listed once: `feat_00000273` Stem Export (3 strings above; shown as a "Export stems" option, not an offer list), `feat_00000269` Stem Separation, `feat_00000270` Smart Mix Assistant, `feat_00000271` Lyric Assistant, `feat_00000275` Tempo Map (no strings).

## Target labels proposed

None. `feat_00000274` Freeze Track has no es-es term but appears in no string, so there is no shipped wording to propose.

## New-concept candidates

Response: `added: 0`, `counted_as_repeats: 5`, `hidden_previously_rejected: 3`, `resurfaced_for_review: 0`, no errors. (The response does not say which 3 were hidden.)

- Sound Design — "Diseño de sonido", 3
- Metronome — "Metrónomo", 2
- Key — "Tonalidad", 4
- Drum Pattern Generator — "Generador de patrones de batería", 2
- Audio Comping — "Comping de audio", 1
- Chord Explorer — "Explorador de acordes", 1
- Scale Assistant — "Asistente de escalas", 1 (newly ungoverned)
- Interactive Lessons — "Lecciones interactivas", 1

## Other observations (carried over)

- `onboarding:profile_setup.field_role_option_sound_designer` (`onboarding.json:86`): "Diseño de sonido" names the discipline, not the role.
- `onboarding:plan_features.mastering_chain` (`onboarding.json:166`): market profile says "UI: master"; ontology term is "cadena de masterización".
- `onboarding.json:196` en-US note says Style Transfer "Do not translate"; ontology es-es term is translated.
- Baseline: `feat_00000010` keeps `en_previous_terms` ["Melody Composer"]; no string uses it.

## Affected string IDs

1. Needs a string fix
```
onboarding:plan_features.punch_in_recording  feat_00000266  term-match
```
2. Needs a product or terminology decision
```
export:export.stems_count_plural  feat_00000273  new-concept (pending term, verb/noun form)
export:export.stems_count_singular  feat_00000273  new-concept (pending term, verb/noun form)
export:export.stems_option  feat_00000273  new-concept (pending term, verb/noun form)
onboarding:plan_features.scale_assistant  feat_00000268  removed-from-ontology
```
3. Changed in Black Ice, strings already in sync
```
dashboard:nav.ai_composition  feat_00000272  status-change
dashboard:nav.chord_progression  feat_00000013  status-change
dashboard:studio.ai_composition_label  feat_00000272  status-change
export:export.distribution_cta  feat_00000020  status-change
export:export.loudness_check_title  feat_00000019  status-change
onboarding:plan_features.chord_progression_generator  feat_00000013  status-change
onboarding:plan_features.comments_markers  feat_00000016  status-change
onboarding:plan_features.feature_includes_studio_pro  plan_00000004  status-change
onboarding:plan_features.feature_includes_studio_pro_all  plan_00000005  status-change
onboarding:plan_features.loudness_analyzer  feat_00000019  status-change
onboarding:plan_features.one_click_distribution  feat_00000020  status-change
onboarding:plan_features.piano_roll  feat_00000006  status-change
onboarding:plan_features.version_history  feat_00000017  status-change
onboarding:plan_selection.audience_tab_studio  prod_00000002  status-change
onboarding:plans.studio_max_name  plan_00000006  status-change
onboarding:plans.studio_pro_name  plan_00000005  status-change
onboarding:plans.studio_starter_name  plan_00000004  status-change
sample:sample_strings.track_type_midi_description  feat_00000272  status-change
```
