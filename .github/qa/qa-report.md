# es-ES locale sync — QA report

**1 key translated** (`errors.plan_upgrade_hey`), **1 flagged**. Draft passed `validate_translation` with zero governance flags. Key parity with en-US holds.

`"¿Por qué demonios gastamos días y miles de euros en la fase de traducción?"`

## ⚠️ Source string does not look shippable

- **`errors.plan_upgrade_hey` is not user-facing copy.** "Why on earth are we spending days and thousands of bucks on translation step?" is a rhetorical internal aside, not an error message. It was translated as instructed (the run never blocks), but it should almost certainly be **deleted from `locales/en-US/errors.json` rather than localized**. Reasons:
  - `errors` is a shared namespace whose `_metadata.scope_note` says it is consumed by both onboarding and dashboard — a key here is reachable from live UI, and the `plan_upgrade_*` prefix places it next to a real billing error.
  - It contradicts the es-es profile's error pattern (*explicación + acción + tranquilidad*) and the "confianza práctica / cercana pero no informal" voice: no explanation, no next step, no reassurance.
  - No `_notes` entry accompanies it, unlike every other non-trivial key in the file.
- The English is also grammatically incomplete — "on translation step" is missing an article ("the translation step"). Translated as *la fase de traducción*, assuming a pipeline stage is meant.

## Wording decisions worth a second look

- **"bucks" → "euros"** (*miles de euros*). Read as idiomatic "a lot of money" rather than a figure, and localized per the profile's currency convention (`9,99 €`). **If this refers to actual USD spend, this changes the meaning** — switch to *miles de dólares*.
- **"why on earth" → "por qué demonios"** to preserve the rhetorical force. Pan-Hispanic and non-vulgar, so it carries no regional slang, but it sits at the informal edge of the profile's "cercana pero no informal" register. A flatter *¿Por qué dedicamos días y miles de euros a la fase de traducción?* is available if the intensifier is unwanted.
- Used *gastamos* (not *invertimos*) because the source frames the spend as waste.

## New term candidates (no approved Black Ice term)

- `upgrade`, `plan`, and `translation` all returned `found: false`. The ontology holds only `Feature`, `Plan`, and `ProductLine` classes — no billing or localization-process concepts. *fase de traducción* is a free choice, not a governed term.
- Existing es-ES precedent reused for the surrounding namespace: `plan_upgrade_failed` already renders upgrade as *la mejora de tu plan*; nothing in the new string needed to restate it.

## Structural i18n

- No placeholders in the source, so nothing to carry, reorder, or agree with. No plural forms, no concatenation fragments, no English-valued placeholders.
- Length: 74 chars vs. 78 in English — within the profile's 180-char error-body limit, no expansion risk.

## Consistency / drift

- **Brief/profile conflict, resolved toward the profile:** the brief asked for *neutral/international* Spanish, while the Black Ice `es-es` profile mandates *"español de España únicamente · sin vocabulario latinoamericano · tú/vosotros"*. Followed the profile (governing artifact for the locale) and matched the file's existing Spain conventions (*Introduce*, *Comprueba*, *vuelve a intentarlo*), choosing vocabulary that is Spain-correct but not Spain-exclusive.
- `_notes` and `_metadata` untouched; no new note added, mirroring en-US.
