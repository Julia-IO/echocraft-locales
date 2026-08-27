# es-ES locale sync — QA report

**4 keys translated, 0 blocked, 7 flagged (advisory).** Source: `locales/en-US/sample.json` (new file). All 4 drafts passed `validate_translation` (es-es) with zero governance flags on the first attempt. The re-derived output matched the existing `locales/es-ES/sample.json` byte-for-byte, so the file is unchanged.

## Grammar / placeholder concerns

- `project_card_bpm_summary` — `{bpm}` is the only placeholder; carried over once, position unchanged. The en-US file ships **no `_notes` block** (every other en-US namespace has one), so `{bpm}`'s runtime type is undocumented. Assumed an unformatted integer immediately preceding the invariable unit "BPM" — no gender/number agreement is triggered either way. If it can resolve to a decimal, es-ES needs a comma decimal separator (`128,5`) per the market profile's locale conventions; confirm with the formatting layer.

## Black Ice ontology terms used

- **Melody Generator** → `generador de melodías` (status: pending, available) — used in `field_key_helper`; matches `onboarding.plan_features.melody_generator` and `dashboard.nav.melody_generator`.
- **MIDI Editor** → `editor MIDI` (status: **approved**, available) — not surfaced verbatim, but its "MIDI untranslated + Spanish head noun" pattern governs `pista MIDI` in `track_type_midi_description`.
- **Multitrack Recording** → `grabación multipista` (status: pending, available) — consulted for the recording/`pista` register in strings 1 and 4; not surfaced verbatim.

## New term candidates (no approved Black Ice term)

- **Sound Design** — `check_term` returns no match. Rendered `Diseño de sonido`, matching `dashboard.new_project_modal.template_sound_design` and `onboarding.profile_setup.field_role_option_sound_designer`. Note the conflict: the en-US `_notes` for that key say "Anglicism preferred in ES and DE — confirm with Black Ice ontology," but the shipped es-ES corpus is fully translated. Corpus consistency won. Worth an ontology entry to settle it.
- **AI Composition** — no match. Rendered `Composición con IA`, matching `dashboard.studio.ai_composition_label` (whose note calls it a pillar name requiring exact match). Consistent with the market profile's mandated `IA`.
- **Metronome** — no match. Rendered `metrónomo`, matching `dashboard.studio.toolbar_metronome`.
- **Key (musical)** — no match. Rendered `tonalidad`, matching `dashboard.projects.project_card_key_label` and `new_project_modal.field_key_label`.

## Structural i18n issues in the en-US source

- `template_sound_design_description` embeds the template name "Sound Design" inline, duplicating `dashboard.new_project_modal.template_sound_design`. If the UI ever assembles this description from the template label at runtime, the two will drift independently per locale. Prefer a placeholder (`{template_name}`).
- `track_type_midi_description` likewise embeds the pillar name "AI composition tools" inline, duplicating `dashboard.studio.ai_composition_label`. Same drift risk, and that key is explicitly marked as a single-source-of-truth pillar name.
- `locales/en-US/sample.json` has no `_notes` block at all, unlike every other en-US namespace. Placeholder types, expansion risk, and do-not-translate markers all had to be inferred from key paths and the sibling namespaces.

No plural or concatenation problems: none of the 4 keys embeds a count, and no fragment boundaries or edge whitespace suggest runtime assembly.

## Consistency / drift

- No contradictions with existing es-ES messaging. `pista`, `mezcla`, `exportar`, `la nube`, `IA` usage follows the market profile's mandatory terminology; `tú` register and imperative UI verbs (`Elige`, `Empieza`, `Añade`, `sincroniza`) match the rest of the corpus.
- `template_sound_design_description` opens with `Empieza con la plantilla…`, aligned with `new_project_modal.template_section_title` ("Empezar con una plantilla").
- Length: all 4 land within ~8% of the English character count, well inside the profile's 120-char tooltip ceiling — no expansion risk on these surfaces.
