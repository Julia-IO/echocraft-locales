# es-ES sync QA — `locales/en-US/demo.json` → `locales/es-ES/demo.json`

**5 strings translated (new file), 0 blocked, 5 items flagged.** All drafts passed
`validate_translation` (es-es) with zero flags on the first attempt.

## Grammar / placeholder concerns

- `track_count_summary` / `_plural` — `{count}` (integer) carried once into each
  form, kept in leading position (natural in Spanish). Singular renders
  "1 pista en este proyecto"; no gender agreement depends on the slot.
- No positional (`%s` / `%1$s`) placeholders in this namespace.

## Black Ice ontology terms used

- **Studio Max** (`plan_00000006`, Plan) — `pending` / availability **`planned`**.
  Left untranslated as a brand identifier, matching
  `onboarding.plans.studio_max_name`. See availability flag below.
- **Melody Generator** → "generador de melodías" (`pending` / `available`) —
  consulted for `ai_melody_disclaimer`; the feature name is not surfaced in the
  string, so the profile's AI vocabulary ("sugerencias", "IA") was used instead.
- **Creator Max** (`plan_00000003`) — `pending` / `available`; checked as the
  market-available alternative to Studio Max.
- Note: every es-es concept except **MIDI Editor** (`feat_00000001`) is
  `status: pending`, so no term used here is formally approved.
- `check_market_availability` and `list_classes` were not permitted in this run;
  availability reads come from `check_term` / `list_concepts` instead.

## New term candidates (no Black Ice concept found)

- **track** → "pista" — `check_term` no match; market-profile terminology rule,
  consistent with existing es-ES.
- **mix** → "mezcla" — no match; profile rule + golden example "Exportar mezcla".
- **cloud** → "la nube" — no match; profile rule.
- **stem** → "stems" — no match. Profile allows "stems o pistas separadas" and
  asks for a gloss on first mention; the gloss was dropped to keep the upsell
  within button/banner length. Worth registering as a concept.
- **AI suggestions** → "sugerencias con IA" — no match; profile AI vocabulary.

## Structural i18n issues in the en-US source

- **Market availability mismatch (highest priority).** `studio_max_upsell`
  promotes Studio Max, which Black Ice reports as `availability: planned` for
  es-es — as is the whole **Studio** product line (`prod_00000002`). Only
  **Creator** is `available` in this market. Translated as written, but shipping
  it to es-ES likely advertises a plan Spanish users cannot buy. Recommend
  gating by market or retargeting to **Creator Max**.
- **Plural handling is key-suffix, not ICU.** Two sibling keys
  (`track_count_summary` / `_plural`) rather than an ICU `plural` message. It
  happens to work for Spanish (same one/other split as English) so the es-ES
  output is correct, but there is no zero form and it is not plural-safe for
  other locales.
- **Inconsistent plural key naming.** `dashboard.json` uses explicit
  `_singular` / `_plural` pairs; here the singular is the bare key, which reads
  as a non-plural string to tooling.
- **English token in localized copy.** "stems" is retained (industry-standard in
  ES audio work, profile-permitted) but is untranslated English in an es-ES file.
- **No `_notes` block.** Every other namespace ships translator notes marking
  placeholder types, expansion risk and gender hooks; `demo.json` has none, so
  `{count}`'s type and each string's UI surface were inferred from key names.
- **Terse English source.** "Your project exported to the cloud." omits the
  auxiliary — reads like assembled/truncated copy. Rendered as a proper Spanish
  success toast rather than mirrored literally.

## Consistency / drift

- `ai_melody_disclaimer` reuses the wording already established in
  `es-ES/dashboard.json` → `studio.ai_composition_hint` ("Tú eliges qué se
  queda."), keeping the AI-authorship message identical across namespaces.
- "pista" / "pistas" matches `dashboard.projects.project_card_tracks_*`;
  "Exportar mezcla" matches the profile's verb+object button pattern (15 chars,
  within the ≤22-char limit).
- **Register:** the brief asked for neutral/international Spanish; the es-es
  market profile mandates Spanish of Spain (`tú`/`vosotros`, no LatAm
  vocabulary). Followed the profile, which also keeps this file consistent with
  the existing es-ES corpus. Nothing written is region-marked slang.
- `project_exported_toast` follows the profile's success pattern ("Listo. …")
  instead of the English sentence shape — intentional, per golden examples.
