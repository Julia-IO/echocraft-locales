# es-ES locale sync — QA report

**1 key translated, 2 flagged.** Source diff vs `main`: one added key, `dashboard.json → new_project_modal.hello_test` ("Hello" → "Hola"). `validate_translation` (es-es) returned no flags.

## New term candidates (no approved Black Ice term)

- **"Hello"** — `check_term` (es-es) returned no match; not a domain concept. Rendered as **"Hola"**, which is register-neutral and consistent with the market profile's `tú` default. No governance term applies.

## Structural i18n issues

- **`new_project_modal.hello_test` looks like a test/debug key in a shipping namespace.** It sits between `cancel_button` and `_notes` with no `_notes` entry, so there's no indication of the surface it renders on. Translated as a standalone greeting; if it's actually a scaffold for a longer string (or a leftover), it should be removed from en-US rather than localised. Worth a human confirming intent.
- **No placeholders** in the changed string, so no placeholder-agreement or word-order concerns for this run.

## Consistency / drift

- No drift. `new_project_modal` contains no other greeting, and the existing `header.greeting_*` strings use a different pattern (time-of-day + `{name}`, e.g. "Buenos días, {name}."), so "Hola" doesn't compete with or contradict them. Terminology elsewhere in `locales/es-ES/` is untouched.
