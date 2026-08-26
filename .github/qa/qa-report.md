# es-ES locale sync — QA report

**1 key translated, 1 flagged.** Changed source: `locales/en-US/dashboard.json` → `nav.get_test` ("Say hello") → `locales/es-ES/dashboard.json` → `"Saluda"`.

## Grammar / placeholder concerns

- None — the changed string contains no placeholders.

## Black Ice ontology terms used

- None. No domain concept from the Echocraft ontology appears in "Say hello"; `validate_translation` on the draft returned 0 flags for `es-es`.

## New term candidates

- None.

## Structural i18n issues (en-US source)

- `nav.get_test` — **ambiguous UI intent.** "Say hello" in a nav bar is idiomatically a *Contact us* link in marketing navs, but the key name (`get_test`, mirroring the existing scaffold key `new_project_modal.hello_test` = "Hello") reads as a test/placeholder string. Translated as a literal greeting imperative (`"Saluda"`, tú register, 6 chars — well inside the ≤22-char button/nav ceiling). If the intent is actually a contact link, `"Hablemos"` is the natural es-ES equivalent and the string should be re-issued.
- `nav.get_test` — no `_notes` entry, unlike most other keys in `dashboard.json` which carry `[PLACEHOLDER]` / `[EXPANSION RISK]` translator guidance. The key name is also non-descriptive of its surface, which is what forced the guess above.

## Consistency / drift

- Register is consistent with the rest of `locales/es-ES/dashboard.json` and the es-es market profile: tú-form imperative, matching `nav.get_started` ("Empezar gratis"), `nav.download` ("Descargar"), and `new_project_modal.hello_test` ("Hola"). No hype vocabulary, no LatAm forms.
- No contradiction with existing Echocraft messaging elsewhere in `locales/es-ES/`.
