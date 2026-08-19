# es-ES sync QA report — `locales/es-ES/demo.json`

**5 keys translated, 6 flagged.** Source: `locales/en-US/demo.json` (new file vs `origin/main`). Target file was previously deleted and has been recreated mirroring en-US structure. All 5 strings passed `validate_translation` (es-es) with zero flags on the first attempt.

## Grammar / placeholder concerns

- `track_count_summary` / `_plural` — `{count}` resolves to an integer and is carried once into each form, in leading position (natural in Spanish, no reorder needed). Spanish uses the plural form for `0` (`0 pistas`), so the runtime plural selector must not route `0` to the singular key; if it currently branches on `count === 1` this is correct, if it branches on `count <= 1` the es-ES output will be wrong.
- No other placeholders in this namespace; no gender-agreement hooks (no `{name}`-style human-referent placeholders).

## Black Ice ontology terms used

- **Studio Max** (`plan_00000006`) — status `pending`, availability **`planned`**. Used untranslated per brand-tier convention (matches `onboarding.plans.studio_max_name`). See market-availability flag below.
- **Melody Generator** (`feat_00000010`) — status `pending`, term `generador de melodías`. Consulted for `ai_melody_disclaimer`; the approved term itself is not surfaced in the string (the source is a generic AI disclaimer, not a feature label), so no term was inserted.
- **Studio** (`prod_00000002`, ProductLine) — status `pending`, availability `planned`. Referenced only as part of the plan name.
- No forbidden or deprecated variants were returned for any term, and none appear in the output.

## New term candidates (no ontology concept found)

- **track → `pista`** — `check_term` returned no concept for "Track". Governed only by the market profile's terminology rules (`pista (track)`); worth promoting to a first-class ontology concept since it appears across `dashboard`, `validation` and now `demo`.
- **mix → `mezcla`** — no concept. Profile-governed (`mezcla (mix)`) and an explicit UX-microcopy example (`"Exportar mezcla"`).
- **cloud → `la nube`** — no concept. Profile-governed (`la nube (cloud)`).
- **stem → `stems` / `pistas separadas`** — no concept. Profile requires clarifying on first mention (golden example: `Exportar pistas separadas (stems)`); rendered here as `stems (pistas separadas)`. Needs an ontology entry to fix which of the two forms is primary in UI vs docs.

## Structural i18n issues in the en-US source

- **Market availability vs. upsell copy**: `studio_max_upsell` promotes Studio Max, which Black Ice reports as `availability: "planned"` for es-es (as is the whole `Studio` product line). Shipping this string to Spain advertises a plan that is not yet purchasable there. Product/marketing call — the string was written as specified, not suppressed.
- **Ad-hoc plural structure**: `track_count_summary` + `track_count_summary_plural` is a suffix-pair convention rather than an ICU `plural{}` structure, and there is no zero form. It happens to survive Spanish (2 cardinal forms), but it will break for locales with 3+ forms and it pushes the `count === 1` decision into application code. Recommend migrating the namespace to ICU plurals.
- **`stems` as an untranslated loanword in source**: the source assumes the reader knows "stems". The es-ES market profile mandates a first-mention gloss, which is why the target string is ~18% longer than the English. If this surfaces in a width-constrained upsell banner, the gloss is the first thing to drop — confirm the surface.
- **Missing `_notes` block**: every other namespace in this repo documents placeholders and expansion risk under `_notes`. `demo.json` has none, so `{count}`'s runtime type and the upsell's surface had to be inferred from the key path.
- **Em dash in `ai_melody_disclaimer`**: the source uses ` — ` as a soft break; es-ES renders it as a colon, which is the natural Spanish equivalent. Intentional, not a dropped character.

## Consistency / drift

- `ai_melody_disclaimer` reuses the exact clause `tú eliges qué se queda` already established in `es-ES/dashboard.json` → `studio.ai_composition_hint`, and aligns with the profile's golden example (`…pero tú decides qué se queda`). Same concept, same wording.
- `export_mix_button` uses `Exportar mezcla`, matching the profile's verbatim UX-microcopy example and the existing `dashboard.projects.project_card_export` (`Exportar`) verb choice. 15 chars, within the ≤22 button budget.
- `project_exported_toast` follows the profile's success-toast pattern (`Listo. …`) rather than the English's bare declarative.
- `pista`/`pistas` matches `dashboard.projects.project_card_tracks_*` and `dashboard.studio.track_add_button`.
- **Note on the brief**: the task asked for "neutral/international" Spanish, but the Black Ice es-es profile mandates *español de España only* — `tú`/`vosotros`, no Latin American vocabulary. The profile was treated as authoritative. No string in this batch actually forces the choice (none use second-person plural or region-split vocabulary), so the output is safe either way.
