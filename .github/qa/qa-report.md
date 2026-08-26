# es-ES locale sync — QA report

**4 keys translated** (new file `locales/es-ES/sample.json`), **0 blocked**, 6 items flagged for review. All 4 drafts passed `validate_translation` (es-es) with no flags on the first attempt.

## Grammar / placeholder concerns

- `sample_strings.project_card_bpm_summary` — `{bpm}` is the only placeholder in the changed set; carried over once, kept before the invariant unit `BPM` ("va a {bpm} BPM"), so no gender/number agreement is triggered. Assumed it resolves to a formatted number produced upstream; if it is formatted client-side, es-ES needs a comma decimal separator (`128,5`), not a period.
- Register: the Black Ice market profile for `es-es` specifies **español de España, tú/vosotros**, which conflicts with the brief's "neutral/international" instruction. Followed the market profile (and existing `locales/es-ES/*`, which are all `tú`). No Latin-American vocabulary used.

## Black Ice ontology terms used

- **MIDI Editor** → `editor MIDI` — status `approved`, available. Surfaced here as "pista MIDI" (matches `dashboard.studio.track_type_midi`).
- **Melody Generator** → `generador de melodías` — status `pending`, available. Matches `dashboard.nav.melody_generator`.

## New term candidates (no Black Ice concept found)

- **Sound Design** — `check_term` returned no concept. Used `Diseño de sonido`, consistent with `dashboard.new_project_modal.template_sound_design` and `onboarding.profile_setup.field_role_option_sound_designer`. Note: `dashboard._notes.template_sound_design` says the anglicism is preferred in ES and asks to confirm with the ontology — the existing es-ES string does *not* use the anglicism, so the note and the shipped copy already disagree. Worth an ontology entry to settle it.
- **AI Composition** — no concept found. Used `composición con IA`, matching `dashboard.studio.ai_composition_label` and `dashboard.nav.ai_composition`.
- **Metronome** / **Key (musical)** — no concepts. Used `metrónomo` and `tonalidad`, both already established in `dashboard.json`.

## Structural i18n issues in the en-US source

- `locales/en-US/sample.json` declares `"namespace": "dashboard"` but ships as a separate file whose keys shadow concepts already in `dashboard.json` (`project_card_*`, `field_key_*`, `template_sound_design_*`, `track_type_midi_*`). Two files owning the same namespace is a standing drift risk; consider folding these into `dashboard.json`.
- No `_notes` block, unlike every other en-US file. The placeholder contract for `{bpm}` (integer vs. formatted decimal) is therefore undocumented — see above.
- `field_key_helper` uses an em dash as a sentence connector. Rendered as a colon in es-ES, which is the natural es-ES equivalent; flagging only because a mechanical diff will show the punctuation change.

## Consistency / drift

- Terminology aligned with existing es-ES: `pista MIDI`, `tonalidad`, `Diseño de sonido`, `generador de melodías`, `composición con IA`, `metrónomo`, `BPM` (untranslated, per `dashboard._notes.project_card_bpm_label`).
- `track_type_midi_description` (113 chars) sits just inside the profile's 120-char tooltip ceiling. If this surface is narrower than a tooltip, it will need trimming.
