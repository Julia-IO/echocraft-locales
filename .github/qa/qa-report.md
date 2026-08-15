# es-ES locale sync — QA report

**5 keys translated** (`locales/es-ES/demo.json`, new file), **4 flagged**. All 6 drafts passed `validate_translation` (0 governance flags, no revisions needed).

## Grammar / placeholder concerns

- `track_count_summary` / `_plural` — `{count}` resolves to an integer and stays in initial position; es-ES word order matches en-US here, so no reorder needed. Note the singular form renders as "1 pista en este proyecto"; native es-ES microcopy often prefers "Una pista en este proyecto" when count is literally 1, but that would drop the placeholder, so the numeral form was kept.
- `studio_max_upsell` — "ilimitados" agrees with the mixed-gender coordination "pistas (f.) y stems (m.)"; masculine plural is correct and intentional, not a typo for "ilimitadas".

## Black Ice ontology terms used

- **Studio Max** (`plan_00000006`) — status `pending`, availability **`planned`**. Kept untranslated as a brand plan name (matches `onboarding.plans.studio_max_name`). See structural flag below re: availability.
- **Multitrack Recording** → *pista* (`feat_00000004`, `pending`) — profile terminology rule "pista (track)" applied; consistent with `dashboard.projects.project_card_tracks_*`.
- No ontology concept exists for *track*, *stems*, *mix*, or *cloud* as standalone entries; the market profile's `terminologyRules` (pista / mezcla / la nube / exportar / IA, "stems o pistas separadas — aclarar en primera mención") was used as the governing source instead.

## New term candidates (no approved Black Ice term)

- **stems** → *stems (pistas separadas)*. No ontology concept; drawn from the profile's terminology rule and golden example "Exportar pistas separadas (stems)". Glossed on first mention per profile. Worth promoting to a Black Ice concept.
- **cloud** → *la nube*. Profile rule only, no concept entry.
- **mix** → *mezcla*. Profile rule only, no concept entry.

## Structural i18n issues in the en-US source

- **Manual plural pair, not ICU** — `track_count_summary` / `track_count_summary_plural` encode plurals as two sibling keys with a `_plural` suffix rather than an ICU `plural{}` structure. es-ES happens to share en-US's one/other split so the output is correct here, but the pattern won't survive locales with more plural categories, and it leaves the zero case (`0 tracks`) dependent on runtime branching that isn't visible in the file. Same pattern already exists in `dashboard.json` (`project_card_tracks_*`, `notifications_new_*`), so this is a repo-wide convention, not a regression.
- **`studio_max_upsell` promotes a plan marked `planned`, not `available`, in es-es** — Black Ice reports Studio Max availability as `planned` for this market (all Studio-line plans and the `Studio` product line are `planned`; only Creator-line plans are `available`). Shipping this upsell to es-ES users may surface a plan they cannot buy. Product/market decision, not a translation fix — string was written as specified. (`check_market_availability` was not reachable in this run — permission not granted in CI — so this is based on `check_term`/`list_concepts` availability fields.)
- **No `_notes` block in the en-US source** — unlike every other namespace in this repo, `demo.json` ships no translator notes, so placeholder semantics for `{count}` had to be inferred from key naming. Low risk here; worth adding for consistency.

## Consistency / drift

- `ai_melody_disclaimer` was aligned to the existing es-ES control-signal phrasing "Tú eliges qué se queda." (`dashboard.studio.ai_composition_hint`) rather than a fresh rendering, keeping the AI-as-assistant messaging identical across namespaces.
- `export_mix_button` uses "Exportar mezcla" (15 chars, within the ≤22 button budget) — matches the profile's UX microcopy example and the verb+object pattern of `dashboard.projects.project_card_export` ("Exportar").
- **Register tension, resolved toward the profile**: the task brief asked for "neutral/international es-ES", but the Black Ice market profile mandates *español de España únicamente*, `tú`/`vosotros`, and explicitly forbids Latin-American vocabulary. Existing `locales/es-ES/**` is uniformly Spain-Spanish with `tú`. Followed the profile and the existing corpus; the copy avoids region-specific slang either way, so the two requirements only conflict in principle, not in the delivered strings.
