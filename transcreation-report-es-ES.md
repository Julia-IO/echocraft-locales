# Transcreation Report — es-ES
**Product**: ECHOCRAFT
**Locale**: Spanish (Spain) — es-ES
**Date**: 2026-03-06
**Files produced**: `locales/es-ES/onboarding.json`, `locales/es-ES/dashboard.json`, `locales/es-ES/errors.json`, `locales/es-ES/validation.json`

---

## Ontology Note

The CLAUDE.md references the ontology at `~/Desktop/echocraft-course/echocraft-ontology`, but the repository was found at `~/echocraft-ontology`. Ontology was already up to date (`git pull` returned "Already up to date."). All terminology decisions below were drawn from the ontology at `~/echocraft-ontology`.

---

## Terminology Decisions

| Source Term | es-ES Term Used | Ontology Source | Decision |
|---|---|---|---|
| MIDI Editor | editor MIDI | feat_00000001 (pending) | Approved ontology term |
| Piano Roll | Piano Roll | feat_00000006 (pending) | Anglicism preserved per ontology |
| Pattern Sequencer | secuenciador por patrones | feat_00000002 (pending) | Approved ontology term |
| Arrangement Timeline | línea de arreglos | feat_00000007 (pending) | Approved ontology term |
| Multitrack Recording | grabación multipista | feat_00000009 (pending) | Approved ontology term |
| Sample Library | librería de samples | feat_00000008 (pending) | Approved ontology term |
| Effects Rack | rack de efectos | feat_00000010 (pending) | Approved ontology term |
| Melody Generator | generador de melodías | feat_00000011 (pending) | Approved ontology term |
| Chord Progression Generator | generador de progresiones de acordes | feat_00000014 (pending) | Approved ontology term |
| Style Transfer | transferencia de estilos | feat_00000013 (pending) | Approved ontology term — **availability: planned** |
| Mastering Chain | cadena de mástering | feat_00000012 (pending) | Approved ontology term — **availability: not_available** |
| Export MP3 | Exportar en MP3 | feat_00000005 (pending) | Approved ontology term |
| Export WAV/FLAC | Exportar en WAV/FLAC | feat_00000015 (pending) | Approved ontology term |
| Virtual Instruments | instrumentos virtuales | feat_00000003 (pending) | Approved ontology term |
| Creator | Creator | plan_00000001 (approved) | Approved — do not translate |
| Creator Starter | Creator Starter | plan_00000002 (approved) | Approved — do not translate |
| Creator Pro | Creator Pro | plan_00000003 (pending) | Kept per ontology — do not translate |
| Creator Max | Creator Max | plan_00000004 (pending) | Kept per ontology — do not translate |
| track | pista | es-ES market guide | Market-required term |
| mix / mixer | mezcla / mezclador | es-ES market guide | Market-required term |
| cloud | la nube | es-ES market guide | Market-required term |
| AI | IA | es-ES market guide | Standard Spanish abbreviation |

---

## Voice & Transcreation Decisions

| String | Decision |
|---|---|
| `signin.page_title` "Welcome back" → "Hola de nuevo" | Avoided gendered `bienvenido/a` conflict by using a gender-neutral warm greeting per es-ES voice DNA (cercana, motivadora). |
| `dashboard.studio.ai_composition_hint` | Added "Tú decides qué se queda" — mandatory per es-ES market guide AI transparency rule: any AI mention requires a user-control/agency cue. |
| `dashboard.projects.project_card_key_label` "Key" → "Clave" | `Clave` (5 chars) chosen over `Tonalidad` (9 chars) for tight label budget. Clave is correct for musical key in Spain usage. |
| `dashboard.studio.toolbar_save_status_saved` "All changes saved" → "Todo guardado" | Shorter than English (13 vs 17 chars). Idiomatic and status-bar appropriate. |
| `onboarding.signin.submit_button` / `nav.sign_in` | Both use "Iniciar sesión" for cross-namespace consistency. |
| `onboarding.plans.creator_pro_tagline` "Full songwriting workflow" → "Composición al completo" | Concision priority — 23 chars, direct, brand voice aligned (clara, motivadora). |
| `dashboard.new_project_modal.template_singer_songwriter` "Singer-songwriter" → "Cantautor" | Established Spanish equivalent — shorter than English source. |
| `dashboard.new_project_modal.template_film_score` "Film score" → "Banda sonora" | Standard Spanish term for a film's musical score. |
| `onboarding.confirmation.page_title` "You're all set, {name}!" → "¡Todo listo, {name}!" | Fixed idiomatic phrase avoids gendered adjective agreement. |
| `dashboard.studio.toolbar_loop` | "Loop" kept as anglicism — universally understood in Spain music production contexts. |
| `dashboard.new_project_modal.template_beatmaker` | "Beatmaker" kept as anglicism — common in Spain music community. |

---

## Strings Flagged for Review

### [REVIEW] — Ontology gaps (no approved es-ES term)

| String key | Source term | Term used | Reason |
|---|---|---|---|
| `plan_features.audio_comping` | Audio Comping | selección de tomas | Not in ontology. Descriptive translation of the comping workflow. Confirm with localization lead. |
| `plan_features.punch_in_recording` | Punch-In Recording | grabación punch-in | Not in ontology. En-US notes suggest anglicism preferred. Confirm. |
| `plan_features.loudness_analyzer` | Loudness Analyzer | analizador de loudness | Not in ontology. "Loudness" kept as technical anglicism (LUFS/professional audio context). Confirm. |
| `plan_features.drum_pattern_generator` | Drum Pattern Generator | generador de patrones de batería | Not in ontology. Named following the approved pattern of melody_generator and chord_progression_generator. Confirm. |
| `plan_features.chord_explorer` | Chord Explorer | explorador de acordes | Not in ontology. Confirm with localization lead. |
| `plan_features.scale_assistant` | Scale Assistant | asistente de escalas | Not in ontology. Confirm with localization lead. |
| `plan_selection.audience_tab_studio` / `plans.studio_*_name` | Studio (plan group) | Studio | No approved es-ES ontology entry. Kept in English. Confirm with localization lead. |
| `new_project_modal.template_sound_design` | Sound design | Sound design | En-US notes say anglicism preferred but ontology has no approved term. Kept in English. Confirm. |

### [PRODUCT] — Availability flags

| String key | Feature | Issue |
|---|---|---|
| `plan_features.mastering_chain` | Mastering Chain | feat_00000012 `availability: not_available` for es-ES. Feature may not display in es-ES UI — coordinate with product and engineering before publishing. |
| `plan_features.style_transfer` | Style Transfer | feat_00000013 `availability: planned` for es-ES. Feature not yet released in this market — confirm display behaviour (hidden, greyed out, coming-soon badge). |

### [GENDER HOOK] — Design review needed

| String key | Issue |
|---|---|
| `profile_setup.field_role_option_mixing_engineer` | Masculine default ("Ingeniero de mezclas") used. If gender-inclusive forms are required, flag for design review (e.g. "Ingeniero/a de mezclas"). |
| `profile_setup.field_role_option_sound_designer` | Same consideration as mixing_engineer above. |
