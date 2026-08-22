# es-ES sync QA report

5 keys translated in `locales/es-ES/demo.json` (new file); 6 items flagged. All drafts passed `validate_translation` (es-es) with zero governance flags — no revisions needed.

## Grammar / placeholder concerns

- `track_count_summary` / `_plural`: `{count}` carried once each, kept in leading position (natural in ES). Assumed to resolve to an integer. No gender agreement risk ("pista" is feminine and fixed).
- `studio_max_upsell`: mixed-gender noun list ("pistas" f. + "stems" m.) takes masculine plural agreement — "ilimitados" is correct, not "ilimitadas". Noted in case a reviewer reads it as a typo.

## Black Ice ontology terms used

- **Studio Max** (`plan_00000006`) — status `pending`, availability **`planned`** in es-ES. Brand tier name, kept untranslated.
- **Melody Generator** (`feat_00000010`) — status `pending`, term "generador de melodías". Not surfaced literally; `ai_melody_disclaimer` refers to the feature generically as "Sugerencias con IA" per the profile's AI framing rules.
- Market-profile terminology rules (not ontology concepts) applied verbatim: **pista**, **mezcla**, **la nube**, **exportar**, **IA**, **stems**.

## New term candidates (no approved Black Ice term)

- **track** → "pista" — `check_term` returns no concept; term comes from the market profile's terminology rules and existing es-ES files. Worth promoting to the ontology.
- **stem** → "stems" — no concept. Profile says "stems o pistas separadas (aclarar en primera mención)". Kept as "stems" for length in an upsell line; see drift note below.
- **mix** → "mezcla", **export** → "exportar", **cloud** → "la nube", **project** → "proyecto" — all profile-governed, none present as ontology concepts.

## Structural i18n issues in the en-US source

- **Plural handling**: `track_count_summary` / `track_count_summary_plural` uses the suffix convention rather than an ICU plural structure. It happens to map onto Spanish (one/other), but it's fragile — locales with more than two plural categories will break, and the source carries no `[PLURAL]` note.
- **Missing `_notes` block**: unlike every other namespace in this repo, `demo.json` ships no `_notes`. Translators get no `[PLACEHOLDER]` / `[PLURAL]` / `[EXPANSION RISK]` guidance; `{count}`'s runtime type is inferred, not documented.
- **Market availability mismatch**: `studio_max_upsell` promotes Studio Max, which Black Ice reports as `availability: planned` for es-es. Shipping this string in Spain may advertise a plan users can't buy yet — gate it or confirm launch timing.

## Consistency / drift

- `ai_melody_disclaimer` uses "tú decides qué se queda", matching the Black Ice golden example verbatim. The already-shipped `es-ES/dashboard.json → studio.ai_composition_hint` uses "Tú eliges qué se queda". Same concept, two verbs. I aligned the new string to the governance source; recommend converging dashboard onto "decides" (out of scope for this run).
- "stems" appears bare here, while the profile's golden export example clarifies it as "pistas separadas (stems)". This is the first mention of stems anywhere in `locales/es-ES/`. Left bare to respect upsell line length; flag if a fuller first-mention gloss is preferred.
- `export_mix_button` → "Exportar mezcla" matches the profile's UX microcopy example exactly and the verb+object button pattern (15 chars, under the 22-char button ceiling).
