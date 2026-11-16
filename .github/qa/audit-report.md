# es-ES terminology audit — 2026-11-16

**56 mapped es-ES strings checked across 31 of 38 concepts (check_term on all 38 concepts: 37 with an es-es term, 1 without (`feat_00000274` Freeze Track); 0 have variants defined); all 56 validated in `validate_translation` (1 call): 0 forbidden, 0 info. Findings: 2 string-level term issues (1 carried over, 1 new judgment call), 14 status changes (11 with strings), 0 English label changes, 0 availability issues, 1 concept removed, 3 new concepts. 0 target labels proposed, 9 candidates submitted (0 added, 6 repeats, 3 previously rejected).**

## New since last audit

- Large Black Ice update: es-es availability moved to `available` for every previously `planned` / `not_available` concept, so **all 9 availability findings from the last report no longer apply** (see Resolved).
- Status changes (11 concepts with strings, 3 without):
- `feat_00000006` Piano Roll: status `pending` → `approved` (es-es term unchanged: "piano roll") — 1 string
  - `onboarding:plan_features.piano_roll` (`locales/*/onboarding.json:150`)
    - en-US: "Piano Roll"
    - es-ES: "Piano roll"
- `feat_00000013` Chord Progression Generator: availability `planned` → `available` (es-es term unchanged: "generador de progresiones de acordes") — 2 strings
  - `onboarding:plan_features.chord_progression_generator` (`locales/*/onboarding.json:169`)
    - en-US: "Chord Progression Generator"
    - es-ES: "Generador de progresiones de acordes"
  - `dashboard:nav.chord_progression` (`locales/*/dashboard.json:16`) — judgment call: short nav label read as this concept
    - en-US: "Chord Progression"
    - es-ES: "Progresiones de acordes"
- `feat_00000016` Comment & Marker: availability `not_available` → `available` (es-es term unchanged: "comentario y marcador") — 1 string
  - `onboarding:plan_features.comments_markers` (`locales/*/onboarding.json:180`)
    - en-US: "Comments & Markers"
    - es-ES: "Comentarios y marcadores"
- `feat_00000017` Version History: availability `planned` → `available` (es-es term unchanged: "historial de versiones") — 1 string
  - `onboarding:plan_features.version_history` (`locales/*/onboarding.json:179`)
    - en-US: "Version History"
    - es-ES: "Historial de versiones"
- `feat_00000019` Loudness Analyzer: status `pending` → `approved` (es-es term unchanged: "analizador de loudness") — 2 strings
  - `onboarding:plan_features.loudness_analyzer` (`locales/*/onboarding.json:167`)
    - en-US: "Loudness Analyzer"
    - es-ES: "Analizador de loudness"
  - `export:export.loudness_check_title` (`locales/*/export.json:17`)
    - en-US: "Loudness Analyzer"
    - es-ES: "Analizador de loudness"
- `feat_00000020` One-Click Distribution: status `pending` → `approved` (es-es term unchanged: "distribución con un clic") — 2 strings
  - `onboarding:plan_features.one_click_distribution` (`locales/*/onboarding.json:174`)
    - en-US: "One-Click Distribution"
    - es-ES: "Distribución con un clic"
  - `export:export.distribution_cta` (`locales/*/export.json:24`)
    - en-US: "Release with One-Click Distribution"
    - es-ES: "Distribuir con un clic"
- `feat_00000272` AI Composition: status `pending` → `approved`, availability `not_set` → `available` (es-es term unchanged: "composición con IA") — 3 strings
  - `dashboard:nav.ai_composition` (`locales/*/dashboard.json:17`)
    - en-US: "AI Composition"
    - es-ES: "Composición con IA"
  - `dashboard:studio.ai_composition_label` (`locales/*/dashboard.json:130`)
    - en-US: "AI Composition"
    - es-ES: "Composición con IA"
  - `sample:sample_strings.track_type_midi_description` (`locales/*/sample.json:14`)
    - en-US: "Add a MIDI track when you want to program notes with the AI composition tools instead of recording live audio."
    - es-ES: "Añade una pista MIDI para programar notas con las herramientas de Composición con IA en vez de grabar audio en directo."
- `plan_00000004` Studio Starter: availability `planned` → `available` (es-es term unchanged: "Studio Starter") — 2 strings
  - `onboarding:plans.studio_starter_name` (`locales/*/onboarding.json:136`)
    - en-US: "Studio Starter"
    - es-ES: "Studio Starter"
  - `onboarding:plan_features.feature_includes_studio_pro` (`locales/*/onboarding.json:187`)
    - en-US: "Everything in Studio Starter, plus:"
    - es-ES: "Todo lo incluido en Studio Starter y además:"
- `plan_00000005` Studio Pro: availability `planned` → `available` (es-es term unchanged: "Studio Pro") — 2 strings
  - `onboarding:plans.studio_pro_name` (`locales/*/onboarding.json:138`)
    - en-US: "Studio Pro"
    - es-ES: "Studio Pro"
  - `onboarding:plan_features.feature_includes_studio_pro_all` (`locales/*/onboarding.json:190`)
    - en-US: "Everything in Studio Pro, plus:"
    - es-ES: "Todo lo incluido en Studio Pro y además:"
- `plan_00000006` Studio Max: availability `planned` → `available` (es-es term unchanged: "Studio Max") — 1 string
  - `onboarding:plans.studio_max_name` (`locales/*/onboarding.json:140`)
    - en-US: "Studio Max"
    - es-ES: "Studio Max"
- `prod_00000002` Studio: availability `planned` → `available` (es-es term unchanged: "Studio") — 1 string
  - `onboarding:plan_selection.audience_tab_studio` (`locales/*/onboarding.json:107`)
    - en-US: "Studio"
    - es-ES: "Studio"
- `feat_00000269` Stem Separation: es-es term (none) → "separación de stems" (approved), availability null → `not_set` — no strings affected
- `feat_00000270` Smart Mix Assistant: es-es term (none) → "asistente de mezcla inteligente" (pending), availability null → `not_set` — no strings affected
- `feat_00000271` Lyric Assistant: es-es term (none) → "asistente de letras" (pending), availability null → `not_set` — no strings affected
- New concepts since baseline: `feat_00000273` Stem Export (es-es "exportación de stems", pending, `not_set`), `feat_00000274` Freeze Track (no es-es term; used in no string, so no target label proposed — No strings affected), `feat_00000275` Tempo Map (es-es "mapa de tempo", approved, `not_set`; No strings affected — en-US has only "Tempo (BPM)").
- Concept removed from Black Ice: `feat_00000268` Scale Assistant (baseline es-es "asistente de escalas", pending, `not_set`) — `check_term` returns not found. Possibly unintentional; submitted as a new-concept candidate for review. 1 string
  - `onboarding:plan_features.scale_assistant` (`locales/*/onboarding.json:183`)
    - en-US: "Scale Assistant"
    - es-ES: "Asistente de escalas"
- Term mismatch (new, judgment call): `feat_00000273` — 1 string
  - `export:export.stems_option` (`locales/*/export.json:20`) — `_notes` say it refers to Stem Export
    - en-US: "Export stems"
    - es-ES: "Exportar stems" (Black Ice term: "exportación de stems", pending)

## Resolved since last audit

- `feat_00000013`, `onboarding:plan_features.chord_progression_generator`, `dashboard:nav.chord_progression`: availability now `available`, no longer a market-availability finding.
- `feat_00000016` `onboarding:plan_features.comments_markers`: `not_available` → `available`.
- `feat_00000017` `onboarding:plan_features.version_history`: `planned` → `available`.
- `prod_00000002` `onboarding:plan_selection.audience_tab_studio`; `plan_00000004` `onboarding:plans.studio_starter_name`, `onboarding:plan_features.feature_includes_studio_pro`; `plan_00000005` `onboarding:plans.studio_pro_name`, `onboarding:plan_features.feature_includes_studio_pro_all`; `plan_00000006` `onboarding:plans.studio_max_name`: `planned` → `available`.
- `feat_00000268` Scale Assistant and `feat_00000272` AI Composition no longer listed under unknown availability (concept removed / now `available`). `onboarding:plan_features.scale_assistant` is now an ungoverned string (candidate).
- `feat_00000267` Arrangement Timeline: was "new" last week; unchanged this week.
- Previous "Studio Starter/Pro/Max" and "Studio" availability items: resolved as above.

## Status changes

- `feat_00000006` Piano Roll: status `pending` → `approved` (es-es term unchanged: "piano roll") — 1 string
  - `onboarding:plan_features.piano_roll` (`locales/*/onboarding.json:150`)
    - en-US: "Piano Roll"
    - es-ES: "Piano roll"
- `feat_00000013` Chord Progression Generator: availability `planned` → `available` (es-es term unchanged: "generador de progresiones de acordes") — 2 strings
  - `onboarding:plan_features.chord_progression_generator` (`locales/*/onboarding.json:169`)
    - en-US: "Chord Progression Generator"
    - es-ES: "Generador de progresiones de acordes"
  - `dashboard:nav.chord_progression` (`locales/*/dashboard.json:16`) — judgment call: short nav label read as this concept
    - en-US: "Chord Progression"
    - es-ES: "Progresiones de acordes"
- `feat_00000016` Comment & Marker: availability `not_available` → `available` (es-es term unchanged: "comentario y marcador") — 1 string
  - `onboarding:plan_features.comments_markers` (`locales/*/onboarding.json:180`)
    - en-US: "Comments & Markers"
    - es-ES: "Comentarios y marcadores"
- `feat_00000017` Version History: availability `planned` → `available` (es-es term unchanged: "historial de versiones") — 1 string
  - `onboarding:plan_features.version_history` (`locales/*/onboarding.json:179`)
    - en-US: "Version History"
    - es-ES: "Historial de versiones"
- `feat_00000019` Loudness Analyzer: status `pending` → `approved` (es-es term unchanged: "analizador de loudness") — 2 strings
  - `onboarding:plan_features.loudness_analyzer` (`locales/*/onboarding.json:167`)
    - en-US: "Loudness Analyzer"
    - es-ES: "Analizador de loudness"
  - `export:export.loudness_check_title` (`locales/*/export.json:17`)
    - en-US: "Loudness Analyzer"
    - es-ES: "Analizador de loudness"
- `feat_00000020` One-Click Distribution: status `pending` → `approved` (es-es term unchanged: "distribución con un clic") — 2 strings
  - `onboarding:plan_features.one_click_distribution` (`locales/*/onboarding.json:174`)
    - en-US: "One-Click Distribution"
    - es-ES: "Distribución con un clic"
  - `export:export.distribution_cta` (`locales/*/export.json:24`)
    - en-US: "Release with One-Click Distribution"
    - es-ES: "Distribuir con un clic"
- `feat_00000272` AI Composition: status `pending` → `approved`, availability `not_set` → `available` (es-es term unchanged: "composición con IA") — 3 strings
  - `dashboard:nav.ai_composition` (`locales/*/dashboard.json:17`)
    - en-US: "AI Composition"
    - es-ES: "Composición con IA"
  - `dashboard:studio.ai_composition_label` (`locales/*/dashboard.json:130`)
    - en-US: "AI Composition"
    - es-ES: "Composición con IA"
  - `sample:sample_strings.track_type_midi_description` (`locales/*/sample.json:14`)
    - en-US: "Add a MIDI track when you want to program notes with the AI composition tools instead of recording live audio."
    - es-ES: "Añade una pista MIDI para programar notas con las herramientas de Composición con IA en vez de grabar audio en directo."
- `plan_00000004` Studio Starter: availability `planned` → `available` (es-es term unchanged: "Studio Starter") — 2 strings
  - `onboarding:plans.studio_starter_name` (`locales/*/onboarding.json:136`)
    - en-US: "Studio Starter"
    - es-ES: "Studio Starter"
  - `onboarding:plan_features.feature_includes_studio_pro` (`locales/*/onboarding.json:187`)
    - en-US: "Everything in Studio Starter, plus:"
    - es-ES: "Todo lo incluido en Studio Starter y además:"
- `plan_00000005` Studio Pro: availability `planned` → `available` (es-es term unchanged: "Studio Pro") — 2 strings
  - `onboarding:plans.studio_pro_name` (`locales/*/onboarding.json:138`)
    - en-US: "Studio Pro"
    - es-ES: "Studio Pro"
  - `onboarding:plan_features.feature_includes_studio_pro_all` (`locales/*/onboarding.json:190`)
    - en-US: "Everything in Studio Pro, plus:"
    - es-ES: "Todo lo incluido en Studio Pro y además:"
- `plan_00000006` Studio Max: availability `planned` → `available` (es-es term unchanged: "Studio Max") — 1 string
  - `onboarding:plans.studio_max_name` (`locales/*/onboarding.json:140`)
    - en-US: "Studio Max"
    - es-ES: "Studio Max"
- `prod_00000002` Studio: availability `planned` → `available` (es-es term unchanged: "Studio") — 1 string
  - `onboarding:plan_selection.audience_tab_studio` (`locales/*/onboarding.json:107`)
    - en-US: "Studio"
    - es-ES: "Studio"
- `feat_00000269` Stem Separation: es-es term (none) → "separación de stems" (approved), availability null → `not_set` — no strings affected
- `feat_00000270` Smart Mix Assistant: es-es term (none) → "asistente de mezcla inteligente" (pending), availability null → `not_set` — no strings affected
- `feat_00000271` Lyric Assistant: es-es term (none) → "asistente de letras" (pending), availability null → `not_set` — no strings affected

## Term match

- `feat_00000266` Punch-In Recording — es-ES "Grabación con punch-in" vs approved "grabación con Punch-In" (case only; carried over) — 1 string
  - `onboarding:plan_features.punch_in_recording` (`locales/*/onboarding.json:157`)
    - en-US: "Punch-In Recording"
    - es-ES: "Grabación con punch-in"
- `feat_00000273` Stem Export (new concept, es-es term "exportación de stems", pending) — es-ES uses verb form "Exportar stems"; judgment call, likely acceptable inflection — 1 string
  - `export:export.stems_option` (`locales/*/export.json:20`)
    - en-US: "Export stems"
    - es-ES: "Exportar stems"

## Forbidden variants

None. 0 `forbidden`, 0 `info` across 56 strings. No concept has allowed/forbidden variants defined (38 concepts checked, 0 with variants).

## Market availability

None. All mapped concepts are `available` in es-es. Unknown availability (`not_set`), listed once; none of these concepts is used in an offer string: `feat_00000269`, `feat_00000270`, `feat_00000271`, `feat_00000273` (1 string, shown above, UI checkbox not offer copy), `feat_00000275`. No strings affected except Stem Export above.

## Target labels proposed

None. `feat_00000274` Freeze Track has no es-es term and appears in no string. `propose_translation` was not called.

## New-concept candidates

Response: `added: 0`, `counted_as_repeats: 6`, `hidden_previously_rejected: 3`, `resurfaced_for_review: 0`, no errors. 9 submitted (the 7 from last week plus Scale Assistant and EQ & Compression; which 3 were hidden as previously rejected is not reported by Black Ice).

- Sound Design — "Diseño de sonido", 3
- Metronome — "Metrónomo", 2
- Key — "Tonalidad", 4
- Drum Pattern Generator — "Generador de patrones de batería", 2
- Audio Comping — "Comping de audio", 1
- Chord Explorer — "Explorador de acordes", 1
- Interactive Lessons — "Lecciones interactivas", 1
- Scale Assistant — "Asistente de escalas", 1 (concept removed from Black Ice)
- EQ & Compression — "EQ y compresión", 1 (named feature in a feature list)

## Other observations (carried over)

- `onboarding:profile_setup.field_role_option_sound_designer` (`onboarding.json:86`): "Diseño de sonido" names the discipline, not the role.
- `onboarding:plan_features.mastering_chain` (`onboarding.json:166`): market profile says "UI: master"; ontology term is "cadena de masterización".
- `onboarding.json:196` en-US note says Style Transfer "Do not translate"; ontology es-es term is translated.
- `export:export.distribution_cta` "Distribuir con un clic" read as a verb form of "distribución con un clic" (judgment).
- `mix_tools` namespace is referenced in Black Ice notes but not present in `locales/` on `main`.
- The en-US status of several concepts also changed (e.g. Melody Generator now approved in en-us); es-es status for `feat_00000010` remains pending.

## Affected string IDs

1. Needs a string fix
```
onboarding:plan_features.punch_in_recording  feat_00000266  term-match
```
2. Needs a product or terminology decision
```
export:export.stems_option  feat_00000273  term-match (pending term)
onboarding:plan_features.scale_assistant  feat_00000268  concept-removed
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
