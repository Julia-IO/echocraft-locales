# Transcreation Report — es-ES

**Date**: 2026-03-06
**Locale**: Spanish (Spain) — `es-ES`
**Files produced**:
- `locales/es-ES/dashboard.json`
- `locales/es-ES/errors.json`
- `locales/es-ES/onboarding.json`
- `locales/es-ES/validation.json`

---

## Ontology Version

Last commit: `207b4002d5df14cccc59540c9c268b49a43ec54a` — 2026-02-27
Status at session start: **Already up to date.**

---

## Terminology Decisions

| Source Term | Target Term | Ontology File | Decision |
|---|---|---|---|
| MIDI Editor | Editor MIDI | feat_00000001 | Ontology-approved term. Capitalised for list display. |
| Pattern Sequencer | Secuenciador por patrones | feat_00000002 | Ontology-approved term. Capitalised for display. |
| Virtual Instrument(s) | instrumento(s) virtual(es) | feat_00000003 | Ontology-approved term. Count prepended as per source string pattern. |
| Export MP3 | Exportar en MP3 | feat_00000005 | Ontology term 'exportar en mp3' — MP3 capitalised for display consistency. |
| Piano Roll | Piano Roll | feat_00000006 | Ontology-approved anglicism. Kept as-is. |
| Arrangement Timeline | Línea de arreglos | feat_00000007 | Ontology-approved term. Capitalised for display. |
| Sample Library | Librería de samples | feat_00000008 | Ontology-approved term. Capitalised for display. |
| Multitrack Recording | Grabación multipista | feat_00000009 | Ontology-approved term. Track count appended per source pattern. |
| Effects Rack | Rack de efectos | feat_00000010 | Ontology-approved term. Capitalised for display. |
| Melody Generator | Generador de melodías | feat_00000011 | Ontology-approved term. Capitalised for display. |
| Mastering Chain | Cadena de mástering | feat_00000012 | Ontology-approved term. Note: ontology marks es-ES availability as `not_available` — see flags below. |
| Style Transfer | Transferencia de estilos | feat_00000013 | Ontology-approved term. Note: ontology marks es-ES availability as `planned`. |
| Chord Progression Generator | Generador de progresiones de acordes | feat_00000014 | Ontology-approved term. Capitalised for display. |
| Export WAV/FLAC | Exportar en WAV/FLAC | feat_00000015 | Ontology term 'exportar en wav/flac' — WAV/FLAC capitalised for display consistency. |
| Creator (Plan Group) | Creator | plan_00000001 | Ontology-approved, status: approved. Not translated. |
| Creator Starter | Creator Starter | plan_00000002 | Ontology-approved, status: approved. Not translated. |
| Creator Pro | Creator Pro | plan_00000003 | Brand plan name. Not translated per policy. |
| Creator Max | Creator Max | plan_00000004 | Brand plan name. Not translated per policy. |
| track | pista | markets/es-es.md | Standard es-ES market term. |
| mix / Mixer | mezcla / Mezclador | markets/es-es.md | 'Mezclador' used for the UI panel label. |
| AI | IA | markets/es-es.md | Standard Spanish abbreviation. Used throughout. |
| cloud | la nube | markets/es-es.md | Standard es-ES market term. |
| sound design | Sound design | markets/es-es.md (note) | Source note flags anglicism preferred. Not confirmed in ontology — flagged [REVIEW]. |
| Jam Sessions | sesiones jam | markets/es-es.md | Anglicism standard in es-ES music production contexts. |
| Loudness Analyzer | Analizador de sonoridad | — (not in ontology) | 'Sonoridad' is the ITU/EBU standard Spanish term for loudness. Flagged [REVIEW]. |
| Drum Pattern Generator | Generador de patrones de batería | — (not in ontology) | Direct, natural es-ES rendering. Flagged [REVIEW]. |
| Audio Comping | Comping de audio | — (not in ontology) | Partial anglicism common in es-ES DAW contexts. Flagged [REVIEW]. |
| Punch-In Recording | Grabación punch-in | — (not in ontology) | Anglicism retained per source note guidance. Flagged [REVIEW]. |

---

## Strings Flagged [REVIEW]

| Key | String | Reason |
|---|---|---|
| `dashboard.new_project_modal.template_sound_design` | Sound design | Anglicism preferred per source note, but term not confirmed in ontology. Confirm with localization lead. |
| `dashboard.new_project_modal.template_singer_songwriter` | Cantautor | Masculine default used. If the UI supports gender-adaptive content, expose feminine variant (Cantautora). |
| `onboarding.signin.page_title` | Bienvenido de nuevo | [GENDER HOOK] Masculine default. Consider 'Bienvenido/a de nuevo' if the platform supports gender-adaptive strings. |
| `onboarding.profile_setup.field_role_option_producer` | Productor | [GENDER HOOK] All four role options (Productor, Compositor, Ingeniero de mezclas, Diseñador de sonido) use masculine default. Recommend exposing feminine variants (Productora, Compositora, etc.) if the platform supports it. |
| `onboarding.plan_features.audio_comping` | Comping de audio | Term not in ontology. Confirm with localization lead. |
| `onboarding.plan_features.punch_in_recording` | Grabación punch-in | Term not in ontology. Source note flags anglicism likely preferred; confirm. |
| `onboarding.plan_features.loudness_analyzer` | Analizador de sonoridad | Term not in ontology. 'Sonoridad' is the standard ITU/EBU Spanish translation of 'loudness'. Confirm with localization lead. |
| `onboarding.plan_features.drum_pattern_generator` | Generador de patrones de batería | Term not in ontology. Natural es-ES rendering. Confirm with localization lead. |
| `onboarding.plan_features.mastering_chain` | Cadena de mástering | Ontology term confirmed (feat_00000012), but ontology marks es-ES availability as `not_available`. Flag for product team — string is provided for UI completeness. |
| `onboarding.plan_features.style_transfer` | Transferencia de estilos | Ontology term confirmed (feat_00000013), but ontology marks es-ES availability as `planned`. Flag for product team. |

---

## Strings Flagged [LENGTH]

No strings exceeded acceptable length targets. The following were monitored closely:

| Key | es-ES String | Char Count | Note |
|---|---|---|---|
| `dashboard.projects.storage_almost_full` | Almacenamiento casi lleno — mejora tu plan | 42 | English: 34. Slight expansion — acceptable for status bar. Monitor on mobile. |
| `onboarding.plan_selection.tier_badge_popular` | El más popular | 14 | English: 12. Expansion within badge tolerance. |
| `onboarding.plans.creator_pro_tagline` | Flujo completo de composición | 29 | Shortened from literal to manage expansion risk. Meaning preserved. |
| `dashboard.studio.ai_composition_hint` | Genera melodías, progresiones de acordes y patrones de batería con la IA de ECHOCRAFT. Tú decides qué usas. | 105 | Agency cue added per market guide. Monitor body copy container. |

---

## Step-by-Step Summary

1. **Pulled ontology** — `git -C ~/echocraft-ontology pull`. Already up to date. Last commit: `207b4002` (2026-02-27).
2. **Read ontology** — `classes/README.md`, `markets/es-es.md`, `relationships/README.md`, and all 18 terminology files (15 feature files + 3 plan files). No feat_00000004 file found (ID gap in sequence — not referenced in relationships graph).
3. **Read source files** — all four `locales/en-US/*.json` files read in full.
4. **Applied es-ES market guide** — voice (cercana, experta, motivadora, clara), tú/vosotros pronouns, Spain-specific vocabulary (ordenador, móvil, archivo), ¿? / ¡! punctuation, imperative verbs for UI actions.
5. **Applied ontology terminology** — 14 ontology-approved terms used exactly as specified. 4 terms not in ontology were flagged [REVIEW].
6. **Applied AI transparency rule** — wherever AI features are mentioned, a control/agency cue was added or preserved (e.g., `ai_composition_hint` ends with "Tú decides qué usas.").
7. **Applied character budget discipline** — button text kept to 2–3 words; status strings shortened where needed; no string sacrificed meaning for length without flagging.
8. **Wrote four locale files** — `dashboard.json`, `errors.json`, `onboarding.json`, `validation.json` under `locales/es-ES/`.
9. **Saved this report** — `transcreation-report-es-ES.md` in repo root.
