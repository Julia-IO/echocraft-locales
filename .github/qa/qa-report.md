# es-ES locale sync — QA report

**6 keys translated, 5 flagged.** Source diff vs `origin/main`: one added file, `locales/en-US/onboard.json` (6 translatable keys). Created `locales/es-ES/onboard.json` mirroring the en-US structure. All 6 drafts passed `validate_translation` (es-es) with zero flags on the first attempt.

## Grammar / placeholder concerns

- **`track_count_summary` / `_plural`** — `{count}` carried once each, position unchanged (Spanish takes the numeral first here too, same as EN). Assumed to resolve to a formatted integer; per the market profile, thousands should use a space separator (`1 000`) — that's the formatter's job, not the string's, so confirm the runtime number formatter is locale-aware.
- **`studio_max_upsell`** — "pistas" (fem.) + "stems" (masc. loan) coordinate into a mixed-gender plural, so the adjective is masculine plural: "ilimitad**os**". Intentional and grammatically correct, but it reads as agreeing only with "stems"; flagging so a reviewer doesn't "fix" it to "ilimitadas".

## New term candidates (no approved Black Ice term)

- **track** — `check_term` (es-es) returned no match. Used **"pista"** per the market profile `terminologyRules` and consistent with existing `dashboard.json` (`project_card_tracks_*`).
- **mix** — no `check_term` match. Used **"mezcla"**; the profile's `uxMicrocopyRules` gives "Exportar mezcla" verbatim as a button example, so this is effectively governed but not in the ontology.
- **stem** — no `check_term` match. Used **"stems"** per `terminologyRules` ("stems o pistas separadas"). See structural note below re: first mention.
- **project / export / cloud** — no `check_term` matches despite the en-US `_notes` calling them "ontology-approved". Used "proyecto", "exportar", "la nube" from the profile's `terminologyRules`. These three look like genuine ontology gaps worth adding as concepts.

## Structural i18n issues

- **`_metadata.namespace` in the new en-US file says `"dashboard"`, not `"onboard"`/`"onboarding"`.** Mirrored as-is (never edited en-US), but this is likely a copy-paste error at source — it will collide with `dashboard.json`'s namespace if the loader keys off that field. Fix belongs in en-US.
- **Plural handling is a two-key hack, not ICU.** `track_count_summary` / `track_count_summary_plural` mirrors the existing `dashboard.json` pattern, so it's consistent — but a bare singular/plural pair can't express es-ES plural rules properly and gives no room for a `count = 0` form ("Ningún…" vs. "0 pistas"). Same latent issue as `project_card_tracks_*` and `notifications_new_*`; worth migrating the whole repo to ICU `plural {}` at some point.
- **`studio_max_upsell` promotes a plan that is not yet available in this market.** `check_term` (es-es) reports `Studio Max` with `availability: "planned"` (all three `Studio *` plans are `planned`; `Creator *` are `available`). Copy shipped as written, but a Spanish user may see an upsell for something they can't buy. `check_market_availability` could not be called in this run (permission not granted in CI), so this is based on `check_term` metadata only — needs a human call on whether to gate the key.
- **"stems" appears here for the first time in `locales/es-ES/`.** The profile says to clarify it on first mention ("pistas separadas (stems)"), and the golden example does exactly that. Left uncontracted for length — the string is an upsell banner and the parenthetical pushes it to ~65 chars. Flagging as a deliberate deviation.
- **`project_exported_toast` reads as a completed-state toast in EN but is phrased as a bare declarative** ("Your project exported to the cloud."). Rendered with the profile's success pattern ("Listo. …"), which adds a word EN doesn't have. Intentional; not a literal match.

## Consistency / drift

- **"Tú eliges qué se queda"** in `ai_melody_disclaimer` reuses the exact phrasing already in `es-ES/dashboard.json → studio.ai_composition_hint`, and matches the profile's AI-framing golden example. Deliberate — same concept, same wording.
- **"{count} pista(s)"** matches `es-ES/dashboard.json → projects.project_card_tracks_singular/_plural` exactly.
- No contradictions found with existing `es-ES` messaging. `Studio Max` left untranslated, consistent with `onboarding.json → plans.studio_max_name`.
- `_notes` blocks kept in English verbatim, consistent with how `es-ES/onboarding.json` and `es-ES/dashboard.json` handle them.
