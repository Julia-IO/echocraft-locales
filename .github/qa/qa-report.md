# es-ES localization QA report

**228 strings translated** across 4 files (`dashboard` 83, `onboarding` 131, `errors` 10, `validation` 4). `locales/es-ES/` did not exist, so all en-US keys were treated as new. **31 items flagged.** No governance violations: `validate_translation` returned zero flags on all 6 batches.

Structure mirrors en-US exactly (keys, nesting, order). `_notes` and `_metadata.scope_note` kept in English — they are translator/engineering metadata, not user-facing; `_metadata.locale` set to `es-ES`. Key and placeholder parity verified by manual inspection (Bash was not approved in this run, so no scripted parity check ran).

## ⚠️ Pipeline bug — terminology silently empty on `es-ES`

`check_term` and `list_concepts` return `term: null, status: null, availability: null` for locale **`es-ES`** but full records for **`es-es`**. Uppercase does not 404, it returns empty fields — so a run that passes the locale as written in the path would translate with **zero terminology governance and never know**. All lookups here were redone with `es-es`. Recommend the workflow lowercase the locale before calling Black Ice.

## Market availability (translated, but should not ship to es-ES yet)

- **`Studio` product line + `Studio Starter` / `Studio Pro` / `Studio Max` → `planned`.** All of `plan_selection.audience_tab_studio*` and `plans.studio_*` advertise a tier not yet available in this market.
- **`Comment & Marker` → `not_available`.** `plan_features.comments_markers` promises a feature that is not available in es-ES.
- **`Version History` → `planned`.** `plan_features.version_history`.
- 17 of 18 matched ontology terms are status **`pending`** — only `editor MIDI` is `approved`. Terminology may still shift under this whole file set.

## Grammar / placeholder concerns

- **`confirmation.checklist_plan`** — `{plan_name}` reordered: `"Plan {plan_name} activado"`. Spanish puts the brand name after the noun; `activado` agrees with `Plan` (m.sg.), so it is safe for every plan name.
- **`errors.upload_file_too_large`** — `{max_size}` reordered after `límite de`. Named placeholder, no format constraint.
- **`header.notifications_new_singular`** — the en-US `_notes` recommend ES `"una nueva notificación"`, which **drops `{count}`**. Kept `"{count} notificación nueva"` to preserve placeholder integrity. If the ICU rule genuinely wants the literal word, the source note and the key contract disagree — needs a decision.
- **`welcome.legal_note`** — dropped the possessive/article (`"aceptas {terms_link} y {privacy_link}"`). `{terms_link}` resolves to m.pl. (*Términos…*) and `{privacy_link}` to f.sg. (*Política…*); no single determiner can agree with both.
- **`errors.email_already_registered`** — Spanish needs the opening `¿` **outside** the link: `"¿{signin_link}?"`. Confirm the anchor renders correctly inside `¿…?` and that the `¿` is not visually orphaned from the hyperlink.
- **`projects.storage_upgrade_prompt`** — `{upgrade_link}` now **begins a sentence** in ES. Its resolved text must be capitalized, or the sentence starts lowercase.
- **`projects.project_card_last_edited`** — `"Editado {time_ago}"` assumes the date library emits `"hace 2 horas"` (standard `Intl` es output). If it emits a bare duration (`"2 horas"`), the string reads broken.
- **`errors.password_too_short`, `validation.display_name_too_short/too_long`** — `caracteres` is hard-plural; wrong if `{min_length}`/`{max_length}` is ever `1`.
- **`header.greeting_evening`** — the EN morning/afternoon/evening split does not map onto Spanish day divisions: *Buenas tardes* runs until ~21:00. `"Buenas noches"` will read too early unless the evening boundary is late. Verify the time thresholds, not just the string.
- **Gender — user never gendered.** `signin.page_title` → `"Hola de nuevo"` (not *Bienvenido*), `signin.signup_prompt` → `"¿Es tu primera vez en ECHOCRAFT?"` (not *¿Nuevo…?*), `confirmation.page_title` → `"¡Todo listo, {name}!"`. This resolves the `[GENDER HOOK]` notes on both greeting keys without `/a` forms.
- **`profile_setup.field_role_*` restructured** — options changed from role nouns to activity nouns (`"Producción"`, not *Productor*) with the label as `"Trabajo principalmente en…"`, so no option carries masculine-generic gender. **Needs sign-off**: if these option values are rendered anywhere else as standalone role labels, the grammar of that surface changes too.

## New term candidates (no ontology entry)

| Concept | Proposed es-ES |
|---|---|
| Arrangement Timeline | Línea de tiempo de arreglos |
| Audio Comping | Comping de audio |
| Punch-In Recording | Grabación con punch-in |
| EQ & Compression | EQ y compresión |
| Drum Pattern Generator | Generador de patrones de batería |
| Interactive Lessons | Lecciones interactivas |
| Chord Explorer | Explorador de acordes |
| Scale Assistant | Asistente de escalas |
| AI Composition | Composición con IA |
| Mixer | Mezclador |
| Loop (transport) | Bucle |
| Key (musical) | Tonalidad |
| Time signature | Compás |
| Film score | Banda sonora |
| Sound design | Diseño de sonido |

- **`Sound design` needs a ruling.** The en-US note says "anglicism preferred in ES", the ontology has no entry, and the market profile says *"sin spanglish innecesario"*. Chose `"Diseño de sonido"` (fully established professional usage) — reverse it if the anglicism is the brand position.
- **`Mastering Chain` — conflict.** Ontology says `cadena de masterización`; the profile's terminology rules say UI prefers *master* over *masterización*. Followed the ontology term.

## Structural i18n issues in the en-US source

- **Manual singular/plural key pairs** instead of ICU plural: `header.notifications_new_singular`/`_plural`, `projects.project_card_tracks_singular`/`_plural`. ES needs only one/other so it survives, but the pattern will not hold for locales with more plural categories, and the source's own ES example breaks the placeholder contract (above).
- **Counts and sizes baked into strings**: `multitrack_recording_8/32/64`, `virtual_instruments_10/40`, `sample_library_20gb/100gb/200gb`. Not parameterized, so every tier change is a new translation, and the number cannot be locale-formatted.
- **Pre-formatted size values will use the wrong decimal separator.** `projects.storage_used_label` (`{used}`/`{total}`, note example `'18.3 GB'`) and `errors.upload_file_too_large` (`{max_size}`). The profile requires a decimal **comma** and thin-space thousands (`18,3 GB`, `1 000`). If these are formatted en-US upstream, the es-ES UI shows `18.3 GB` regardless of this file.
- **Inconsistent unit handling**: `profile_setup.avatar_upload_hint` has `MB` hard-coded *outside* `{max_size}`, while `errors.upload_file_too_large` expects the unit *inside* `{max_size}`. Two contracts for the same concept.
- **Duplicate source keys**: `plan_features.feature_includes_starter` and `feature_includes_studio_starter` hold identical EN text (`"All Creator Starter features"`). Two keys, one string — they will drift.
- **Assembled fragments**: `feature_includes_pro` / `_studio_pro` / `_studio_pro_all` are sentence fragments ending in `:` that only work joined to the feature list rendered after them. ES handles the colon+list shape here, but the fragment boundary is not reusable if that list rendering changes.
- **Link text supplied out of band**: `welcome.legal_note`, `signup.signin_prompt`, `signin.signup_prompt`, `projects.storage_upgrade_prompt`. ES needs gender, number and capitalization agreement with text this file cannot see.

## Consistency / drift

- **Register conflict, resolved toward the market profile.** The task brief asked for *neutral international* Spanish with no region-specific vocabulary; the es-ES profile mandates *español de España*, `tú`/`vosotros`, and explicitly forbids Latin-American vocabulary. Followed the profile: `Ajustes`, `Añadir pista`, `Comprueba`, `vuelve a intentarlo`, `ha caducado`. These are correct for Spain and will read as regional if this file is ever reused as a pan-Hispanic base.
- Repeated concepts use one term throughout, verified across all four files: `Iniciar sesión` (`nav.sign_in`, `signin.submit_button`, `errors.session_expired`), `pista`, `mezcla`, `la nube`, `exportar`, `IA`, `Tonalidad` (card label + modal field), `Diseño de sonido` (template + role option), `Nombre visible` (`profile_setup` + both `validation` messages).
- Strings the source declares must match do match: all three `"Start Creating Free"` → `"Empezar a crear gratis"`; both `"Get Started Free"` → `"Empezar gratis"`; `nav.ai_composition` = `studio.ai_composition_label` = `"Composición con IA"`.
- Profile constraints respected: buttons ≤ 22 chars (longest: `"Empezar a crear gratis"`, 22); `studio.ai_composition_hint` 109 chars vs. 120 tooltip cap; longest error body 89 chars vs. 180 cap; no hype vocabulary; `ECHOCRAFT` left uppercase everywhere.
- **AI framing**: `ai_composition_hint` carries the required control signal (`"Tú eliges qué se queda."`), and `nav.ai_composition` uses *Composición **con** IA* — AI as copilot, never author, per the profile's culture rules.
