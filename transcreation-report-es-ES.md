# Transcreation Report — es-ES

**Date**: 2026-03-12
**Locale**: Spanish (Spain) — es-ES
**Files produced**: `locales/es-ES/onboarding.json`, `locales/es-ES/errors.json`, `locales/es-ES/dashboard.json`, `locales/es-ES/validation.json`

---

## Ontology Version

- **Commit**: `207b4002d5df14cccc59540c9c268b49a43ec54a`
- **Date of last commit**: 2026-02-27
- **Status at pull**: Already up to date

---

## Terminology Decisions

| Source Term | Target Term | Ontology File | Decision |
|---|---|---|---|
| MIDI Editor | editor MIDI | feat_00000001 | Approved ontology term used (status: pending) |
| Pattern Sequencer | secuenciador por patrones | feat_00000002 | Approved ontology term used (status: pending) |
| Virtual Instruments | instrumentos virtuales | feat_00000003 | Approved ontology term used (status: pending) |
| Export MP3 | exportar en MP3 | feat_00000005 | Approved ontology term used (status: pending) |
| Piano Roll | Piano Roll | feat_00000006 | Anglicism kept — ontology approved (status: pending) |
| Arrangement Timeline | línea de arreglos | feat_00000007 | Approved ontology term used (status: pending) |
| Sample Library | librería de samples | feat_00000008 | Approved ontology term used (status: pending) |
| Multitrack Recording | grabación multipista | feat_00000009 | Approved ontology term used (status: pending) |
| Effects Rack | rack de efectos | feat_00000010 | Approved ontology term used (status: pending) |
| Melody Generator | generador de melodías | feat_00000011 | Approved ontology term used (status: pending) |
| Mastering Chain | cadena de mástering | feat_00000012 | Ontology term used (status: pending) — availability: not_available in es-es; see flags below |
| Style Transfer | transferencia de estilos | feat_00000013 | Ontology term used (status: pending) — availability: planned in es-es; see flags below |
| Chord Progression Generator | generador de progresiones de acordes | feat_00000014 | Approved ontology term used (status: pending) |
| Export WAV/FLAC | exportar en WAV/FLAC | feat_00000015 | Approved ontology term used (status: pending) |
| Creator (Plan Group) | Creator | plan_00000001 | Not translated — ontology approved (status: approved) |
| Creator Starter | Creator Starter | plan_00000002 | Not translated — ontology approved (status: approved) |
| Creator Pro | Creator Pro | plan_00000003 | Not translated — ontology approved (status: pending) |
| Creator Max | Creator Max | plan_00000004 | Not translated — ontology approved (status: pending) |
| track | pista | markets/es-es.md | Market-preferred term |
| mix | mezcla | markets/es-es.md | Market-preferred term |
| cloud | la nube | markets/es-es.md | Market-preferred term |
| collaborate | colaborar | markets/es-es.md | Market-preferred term |
| AI | IA | markets/es-es.md | Market-preferred abbreviation |
| plugin | plugin | markets/es-es.md | Acceptable anglicism per market guide |
| Mixer | Mezclador | — | Standard DAW translation; 'mixer' avoided per market guide (prefer Spanish in UI labels where natural) |
| Time signature | Compás | — | Standard music theory term in Spanish |
| Sound Design | Diseño de sonido | — | Localised (see REVIEW flag) |
| Loop | Loop | — | Anglicism maintained (see REVIEW flag) |

---

## Strings Flagged [REVIEW]

| String Key | File | Reason |
|---|---|---|
| `plan_features.audio_comping` | onboarding.json | "Audio Comping" not found in ontology. Anglicism maintained. Requires decision: keep anglicism or propose Spanish equivalent (e.g., "toma compuesta"). |
| `plan_features.punch_in_recording` | onboarding.json | "Punch-In Recording" not found in ontology. Anglicism maintained. Requires decision from localization lead. |
| `plan_features.loudness_analyzer` | onboarding.json | Not in ontology. Proposed "Analizador de loudness" (tech anglicism common in Spanish audio engineering). Alternative: "Analizador de nivel". Requires review. |
| `plan_features.drum_pattern_generator` | onboarding.json | Not in ontology. Proposed "generador de patrones de batería". Requires review. |
| `plan_features.chord_explorer` | onboarding.json | Not in ontology. Proposed "Explorador de acordes". Requires review. |
| `plan_features.scale_assistant` | onboarding.json | Not in ontology. Proposed "Asistente de escalas". Requires review. |
| `plan_features.real_time_jam_sessions` / `unlimited_jam_sessions` | onboarding.json | "Jam sessions" not in ontology. Kept as established anglicism in Spanish music culture. Requires confirmation. |
| `new_project_modal.template_sound_design` | dashboard.json | Ontology notes "anglicism preferred in ES". Localized as "Diseño de sonido" for high-level template label — requires confirmation from localization lead. |
| `studio.toolbar_loop` | dashboard.json | "Loop" not in ontology. Kept as anglicism. Requires confirmation. |
| `plan_features.mastering_chain` | onboarding.json | Feature availability marked `not_available` in es-es (feat_00000012). String is transcreated ("cadena de mástering") but product team should confirm whether to display or suppress this feature row in ES market. |
| `plan_features.style_transfer` | onboarding.json | Feature availability marked `planned` in es-es (feat_00000013). String is transcreated ("transferencia de estilos") but product team should confirm display treatment (e.g., "próximamente"). |

---

## Strings Flagged [LENGTH]

| String Key | File | Issue | Recommended Action |
|---|---|---|---|
| `plan_selection.tier_badge_popular` | onboarding.json | EN: "Most Popular" (12 chars) → ES: "Más popular" (11 chars). Fits well. No action needed. | — |
| `plans.creator_pro_tagline` | onboarding.json | EN: "Full songwriting workflow" → ES: "Flujo de trabajo completo para componer" (39 chars). Moderate expansion. | Design: verify card tagline container allows ~40 chars. |
| `studio.ai_composition_hint` | dashboard.json | Added agency cue "Tú decides qué se queda" per es-ES market guide AI transparency rule. Full string longer than EN source. | Design: verify hint text area accommodates the extra sentence. |
| `studio.toolbar_save_status_saved` | dashboard.json | EN: "All changes saved" → ES: "Todo guardado" (14 chars). Shorter than EN — no issue. | — |
| `plan_selection.cta_contact_sales` | onboarding.json | EN: "Contact Sales" (13 chars) → ES: "Contactar con ventas" (20 chars). | Design: verify button width in plan selection grid. |
| `one_click_distribution` | onboarding.json | EN: "One-Click Distribution" → ES: "Distribución con un clic" (24 chars). | Design: verify feature list item width. |

---

## Step-by-Step Summary of Actions

1. **Pulled ontology**: `git -C ~/echocraft-ontology pull` — already up to date (commit `207b4002`, 2026-02-27).
2. **Read ontology**: `classes/README.md`, `markets/es-es.md`, `terminology/README.md`, all 18 terminology files, `relationships/README.md`.
3. **Read source files**: All four en-US string files (`onboarding.json`, `errors.json`, `dashboard.json`, `validation.json`).
4. **Applied market guide (es-ES)**:
   - Voice: cercana, experta, motivadora, clara.
   - Pronouns: tú/vosotros (no usted/ustedes except legal).
   - Buttons: imperative verb + object (Crear, Grabar, Añadir, Exportar…).
   - Consistency: pista, mezcla, exportar, la nube, IA throughout.
   - AI framing: "asistente / copiloto creativo"; every AI mention includes an authorship/control cue ("Tú decides qué se queda").
5. **Applied ontology terminology**: Used approved es-ES terms for all 14 features and 4 plan names found in the ontology. Flagged all terms not in the ontology with [REVIEW].
6. **Handled gender**: Used slash notation (Productor/a, Compositor/a, Ingeniero/a, Diseñador/a, Cantautor/a) for role selectors and template labels where gender agreement is required. Used gender-neutral constructions for headlines where possible (e.g., "¡Todo listo, {name}!" instead of "¡Listo, {name}!").
7. **Handled product availability flags**: Noted `mastering_chain` (not_available) and `style_transfer` (planned) in _notes and in this report for product team coordination.
8. **Created files**: `locales/es-ES/onboarding.json`, `locales/es-ES/errors.json`, `locales/es-ES/dashboard.json`, `locales/es-ES/validation.json`.
9. **Saved this report** as `transcreation-report-es-ES.md` in repo root.
