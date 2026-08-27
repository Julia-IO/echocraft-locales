# es-ES locale sync — QA report

**4 keys translated, 5 flagged.** One new file: `locales/es-ES/sample.json` (mirrors `locales/en-US/sample.json`). All 4 strings passed `validate_translation` with zero governance flags on the first attempt.

## Grammar / placeholder concerns

- `sample_strings.project_card_bpm_summary` — `{bpm}` is the only placeholder in the changed set; carried once, position unchanged (it reads naturally in the same slot in Spanish). Assumed to resolve to a **bare integer**, matching `validation.bpm_out_of_range` where `{min}`/`{max}` are documented as integers. If `{bpm}` can resolve to a decimal, es-ES uses comma decimals (`128,5`) per the market profile — that formatting is upstream of this string and unverified here.
- Unlike every other en-US namespace, `sample.json` ships **no `_notes` block**, so no placeholder documentation was available to confirm the above. Adding one would remove the guesswork on future syncs.

## Black Ice ontology terms used

- **Melody Generator** → *generador de melodías* — status `pending`, available. No forbidden variants.
- **MIDI Editor** (`editor MIDI`) → status `approved`, available. Consulted for MIDI casing; the string itself uses *pista MIDI*, matching `dashboard.studio.track_type_midi`.

## New term candidates (no approved Black Ice term)

- **Sound Design** → used *Diseño de sonido*, reusing `dashboard.new_project_modal.template_sound_design`. Note: that key's own `_notes` say "Anglicism preferred in ES and DE — confirm with Black Ice ontology", but no concept exists. Needs an ontology decision.
- **Metronome** → used *metrónomo*, matching `dashboard.studio.toolbar_metronome`.
- **AI Composition** → used *Composición con IA*, matching `dashboard.studio.ai_composition_label` (flagged there as a pillar name requiring an exact match).

## Structural i18n issues in the en-US source

- `template_sound_design_description` embeds the template's display name inline ("a Sound Design template"), duplicating `dashboard.new_project_modal.template_sound_design`. If that label is renamed, this description silently drifts in every locale. A placeholder or a shared key would be safer.
- The whole `sample` namespace duplicates concepts that already live in `dashboard.json` (project-card BPM, key-field helper, sound-design template, MIDI track type). `errors.json` and `validation.json` both carry an explicit `scope_note` against duplicating strings into feature namespaces; these four look like they belong in `dashboard.json`.

No plural-handling or concatenation issues in the changed keys — none of the four embed a count or look fragment-assembled.

## Consistency / drift

- No drift found. Reused terms verbatim from existing es-ES files: *tonalidad* (`field_key_label`), *generador de melodías* (`nav.melody_generator`), *Diseño de sonido*, *Composición con IA*, *pista MIDI*, *metrónomo*. `BPM` kept untranslated per the established note on `project_card_bpm_label`.
- Register is `tú` throughout, imperative-led for actions, consistent with the market profile and the rest of `locales/es-ES/`.
