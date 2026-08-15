# es-ES sync QA report

6 keys translated in `locales/es-ES/demo.json` (new file), 0 blocked, 5 flagged for review.
All 6 drafts passed `validate_translation` (es-es) with zero governance flags on the first attempt.

## Blocking-ish: invalid source JSON

- `locales/en-US/demo.json` has a **trailing comma** after `"export_mix_button"` (line 16), making the
  file invalid JSON. It parsed here only by manual reading. The es-ES output is valid JSON and does
  not reproduce it. Fix needed in en-US — out of scope for this run (constraint: never edit en-US).

## Market availability

- **`studio_max_upsell` promotes a plan that is not available in this market.** Black Ice reports
  `Studio Max` (`plan_00000006`) as `availability: planned` for es-es — as is the whole `Studio`
  product line (`prod_00000002`). Every `Creator` tier is `available`. Shipping this upsell to es-ES
  users advertises a plan they cannot buy. Recommend gating the key by market, or retargeting it to
  `Creator Max`. Translated as-is so the key is not left empty.

## Grammar / placeholder concerns

- `track_count_summary` / `_plural`: `{count}` resolves to an integer. Kept in leading position —
  matches the established es-ES pattern in `dashboard.projects.project_card_tracks_singular`
  (`"{count} pista"`). No gender agreement risk (`pista` is fixed, feminine).
- `studio_max_upsell`: `"pistas y stems ilimitados"` mixes feminine (`pistas`) and masculine (`stems`)
  nouns; masculine plural agreement on the adjective is correct standard Spanish here, but it reads
  slightly asymmetrically. Acceptable; noted in case a reviewer prefers a recast.

## Black Ice ontology terms used

- `Studio Max` (`plan_00000006`) — status **pending**, availability **planned**. Kept untranslated as
  a brand plan identifier, consistent with `onboarding.plans.studio_max_name`. See availability flag above.
- Market-profile mandated terms (governed by `terminologyRules`, not by an ontology concept):
  **pista** (track), **mezcla** (mix), **la nube** (cloud), **exportar**, **IA**, **stems**.
- `Melody Generator` (`feat_00000010`, "generador de melodías") — checked for `ai_melody_disclaimer`;
  not used, since the source string is a generic AI disclaimer, not a reference to that feature.

## New term candidates (no approved Black Ice term found)

- **track** → `pista` — no ontology concept; taken from the market profile's terminology rules and
  existing es-ES usage.
- **mix** → `mezcla` — same; also matches the profile's UX microcopy example "Exportar mezcla".
- **project** → `proyecto` — no concept; matches existing es-ES files.
- **cloud** → `la nube` — no `Cloud Sync` concept; mandated by profile terminology rules.
- **stems** → `stems` — no `Stem Separation` concept. Profile says "stems o pistas separadas (aclarar
  en primera mención)". Used the bare anglicism here for length; the golden example uses the
  clarifying form "pistas separadas (stems)". Worth registering as a concept.
- **AI suggestions** → `sugerencias con IA` — no `AI Assistant` concept; `sugerencias` is an
  explicitly sanctioned IA word in the profile.

## Structural i18n issues in the en-US source

- **`track_count_summary` uses a suffix-key plural, not ICU.** The `_plural` sibling convention gives
  only two forms. It works for es-ES (which also has 2 categories), but it is not plural-aware
  infrastructure — it will break for locales with `few`/`many` (pl, ru, ar). Every other namespace in
  this repo uses the same `_singular`/`_plural` pattern, so this is a repo-wide design issue, not new
  here. Recommend ICU `plural{}` selects.
- **`track_count_summary` (singular) hardcodes `{count}` for a value that is always 1.** English and
  Spanish both tolerate "1 pista", but the `_notes` in `dashboard.json` for the parallel key say ES
  should read "una nueva notificación" for the singular — i.e. the existing convention is
  inconsistent with itself. I kept `{count}` to match what `dashboard.json` actually ships.
- **`demo.json` has no `_notes` block**, unlike every other namespace in the repo. Placeholder
  semantics for `{count}` had to be inferred. Adding `_notes` would make future locale syncs safer.
- No concatenated/assembled strings and no hard-coded English inside placeholder values detected.

## Consistency / drift

- `ai_melody_disclaimer` deliberately reuses the exact sentence "Tú eliges qué se queda." already
  shipped in `dashboard.studio.ai_composition_hint`, preserving the profile's required AI-control
  signal and keeping one voice for AI authorship messaging across namespaces.
- `export_mix_button` = "Exportar mezcla" (15 chars, within the ≤22-char button ceiling) and is
  consistent with `dashboard.projects.project_card_export` ("Exportar").
- `project_exported_toast` follows the profile's success-toast shape ("Listo. …", cf. "Listo. Ya
  puedes descargarlo.") rather than translating the English literally — the English is a bare
  statement with no confirmation beat, which reads flat as a Spanish toast.
- Register: `tú` throughout, matching all existing es-ES files and the profile default.
