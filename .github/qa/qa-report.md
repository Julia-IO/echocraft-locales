# es-ES sync QA report — `locales/en-US/demo.json`

**6 keys translated, 0 blocked, 6 flagged for review.** All drafts passed
`validate_translation` (es-es) with zero governance flags on the first attempt.

## Grammar / placeholder concerns

- `track_count_summary` / `track_count_summary_plural` — `{count}` resolves to an
  integer and is carried once into each form, in the same leading position
  (natural in Spanish). Singular renders "1 pista en este proyecto", which is
  correct. No reordering needed; no gendered agreement depends on the slot.
- No positional (`%s` / `%1$s`) placeholders in this namespace.

## Black Ice ontology terms used

- **Studio Max** (`plan_00000006`, Plan) — status `pending`, availability
  **`planned`**. Kept untranslated as a brand plan identifier, consistent with
  `onboarding.plans.studio_max_name`. See market-availability flag below.
- **Studio** (`prod_00000002`, ProductLine) — status `pending`, availability
  `planned`.
- Reference terms confirmed for consistency, not newly introduced:
  **Multitrack Recording** → "grabación multipista" (`pending` / `available`),
  **WAV/FLAC Export** → "exportación WAV/FLAC" (`pending` / `available`),
  **Melody Generator** → "generador de melodías" (`pending` / `available`).
- Note: every concept in the es-es ontology except **MIDI Editor**
  (`feat_00000001`) is still `status: pending`, so no term used here is
  formally approved.

## New term candidates (no approved Black Ice term)

- **track** → "pista" — no ontology concept; taken from the market profile's
  terminology rules and already used consistently across es-ES.
- **mix** → "mezcla" — no ontology concept; market-profile term, matches the
  profile's own golden example "Exportar mezcla".
- **cloud** → "la nube" — no ontology concept; market-profile term.
- **stem** → "stems (pistas separadas)" — `check_term` returned no match. The
  market profile allows "stems o pistas separadas" and asks for a gloss on
  first mention, which is what the upsell string does. Worth registering as a
  concept.
- **AI suggestions** → "sugerencias con IA" — no ontology concept;
  market-profile approved AI vocabulary ("sugerencias", "IA").

## Structural i18n issues in the en-US source

- **Market availability mismatch (highest priority).** `studio_max_upsell`
  promotes Studio Max, which Black Ice reports as `availability: planned` for
  es-es — as is the whole **Studio** product line. Only the **Creator** line is
  `available` in this market. The string has been translated as written, but
  shipping it to es-ES likely advertises a plan Spanish users cannot buy.
  Recommend gating this key by market, or retargeting it to **Creator Max**
  (`plan_00000003`, `available`). Could not confirm via
  `check_market_availability` — that tool was not permitted in this run, so the
  read comes from `check_term` availability fields.
- **Plural handling is key-suffix, not ICU.** `track_count_summary` /
  `track_count_summary_plural` encode plurals as two sibling keys. This happens
  to work for Spanish (two forms, same split as English), so es-ES output is
  correct — but it is not a plural-safe structure for the wider locale set, and
  there is no zero form. Every other namespace in this repo uses ICU-oriented
  `_notes` guidance; consider migrating to real ICU `plural` messages.
- **Inconsistent plural key naming.** The pair is `track_count_summary` /
  `track_count_summary_plural`, whereas `dashboard.json` uses explicit
  `_singular` / `_plural` pairs (`project_card_tracks_singular` /
  `_plural`). The bare singular key reads like a non-plural string to tooling.
- **Hard-coded English inside the copy.** "stems" is an English term carried
  into the Spanish string. Retained deliberately (industry-standard in ES audio
  work, and the profile permits it) with a Spanish gloss on first mention, but
  it is an untranslated English token in a localized file.
- **No `_notes` block.** Every other namespace in `locales/en-US/` ships
  translator notes marking placeholders, expansion risk and gender hooks.
  `demo.json` has none, so `{count}`'s type and the surface for each string had
  to be inferred from key names.

## Consistency / drift

- `ai_melody_disclaimer` was written to reuse the exact wording already
  established in `es-ES/dashboard.json` → `studio.ai_composition_hint`
  ("Tú eliges qué se queda."), so the AI-authorship message stays identical
  across namespaces.
- "pista" / "pistas" matches `dashboard.projects.project_card_tracks_*`;
  "Exportar mezcla" matches the `project_card_export` / profile button pattern
  (verb + object, 15 chars, within the ≤22-char button limit).
- **Register conflict, resolved toward the market profile.** The run brief asked
  for "neutral/international" Spanish; the es-es market profile mandates Spanish
  *of Spain* (`tú`/`vosotros`, no Latin American vocabulary). The profile won,
  which also keeps this file consistent with the existing es-ES corpus. Nothing
  written here is region-marked slang, so it reads fine either way.
- `project_exported_toast` follows the profile's success-toast pattern
  ("Listo. …") rather than mirroring the English sentence shape; this is
  intentional and matches the profile's golden examples.
