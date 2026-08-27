# es-ES sync — QA report

**4 keys translated** (new file `locales/es-ES/sample.json`), **0 governance violations** (all 4 passed `validate_translation` on first attempt), **7 items flagged for review.**

## Grammar / placeholder concerns

- `sample_strings.project_card_bpm_summary` — `{bpm}` is the only placeholder in the changeset, carried once, position unchanged. Assumed to resolve to a bare integer (matching `validation.bpm_out_of_range`, where `{min}`/`{max}` are integers). `sample.json` ships **no `_notes` block**, unlike every other en-US namespace, so this is inferred rather than documented. If `{bpm}` ever resolves to a pre-formatted string that already includes the unit (e.g. `"120 BPM"`), the es-ES string would render "a 120 BPM BPM". Same risk exists in en-US.
- `sample_strings.track_type_midi_description` — es-ES is 119 characters against a market-profile tooltip ceiling of 120. Fits, but with no headroom; if this surface is a tooltip and the copy is ever edited, it will overflow immediately.

## Black Ice ontology terms used

- **MIDI Editor** → `editor MIDI` — status **approved**, available. Used as the modifier `pista MIDI`, matching the shipped `dashboard.studio.track_type_midi`.
- **Melody Generator** → `generador de melodías` — status *pending*, available. Matches `dashboard.nav.melody_generator` and `onboarding.plan_features.melody_generator`.
- **Multitrack Recording** → `grabación multipista` — status *pending*, available. Consulted for the "recording live audio" phrasing; rendered as the verb `grabar`, not the feature noun, since the source refers to the act, not the feature.
- **Pattern Sequencer** → `secuenciador de patrones` — status *pending*. Consulted, not used (source doesn't reference it).

## New term candidates (no approved Black Ice term)

- **Metronome** — no concept in the es-es ontology. Used `metrónomo`, matching the shipped `dashboard.studio.toolbar_metronome`.
- **Sound Design** — no concept in the es-es ontology. Used `Diseño de sonido`, matching the shipped `dashboard.new_project_modal.template_sound_design`. Note the en-US `_notes` for that key say *"Anglicism preferred in ES and DE — confirm with Black Ice ontology"*, which **contradicts the string already shipped in es-ES**. Followed the shipped string for consistency; needs a governance decision either way.
- **AI Composition** — no concept in the es-es ontology, despite being a named product pillar. Used `Composición con IA`, matching `dashboard.studio.ai_composition_label` (whose `_notes` require exact pillar-name match). Strong candidate for promotion into the ontology.
- **Arrangement** — no concept. Used `arreglo`, consistent with `onboarding.plan_features.arrangement_timeline` ("Línea de tiempo de arreglos").

## Structural i18n issues in the en-US source

- **Namespace duplication / two sources of truth.** All four new keys restate concepts that already exist in `dashboard.json`: `project_card_bpm_label`, `field_key_label`, `template_sound_design`, `track_type_midi`. Both `errors.json` and `validation.json` carry an explicit `_metadata.scope_note` — *"Do not duplicate strings into feature namespaces — always reference \* keys"* — and this new namespace cuts against that convention. Terminology now has to be kept in sync manually across two files per locale.
- **No `_notes` block.** Every other en-US namespace documents placeholder types, expansion risk, and do-not-translate terms. `sample.json` documents none, so `{bpm}`'s runtime type, the intended UI surface, and the BPM/MIDI do-not-translate rules all had to be inferred from neighbouring files.
- **Key names don't match copy shape.** `project_card_bpm_summary` sits under a `project_card_*` name (a dense card surface elsewhere in `dashboard.json` — `{count} pista`, `Editado {time_ago}`) but carries a full two-clause instructional sentence with an imperative. Likewise `field_key_helper` reads as helper text, `*_description` keys as tooltips. If these really do render on a project card, the en-US source is already over budget and es-ES will be worse.
- **Em dash as a clause joiner** in `field_key_helper` ("...your project is in — this sets..."). Rendered as a colon in es-ES, which is the natural Spanish equivalent; flagged only because a mechanical downstream locale pass may try to preserve the dash.
- No plural-sensitive counts, no concatenated/assembled fragments, and no hard-coded English inside a placeholder value in this changeset.

## Consistency / drift

- `field_key_helper` uses **`Elige`** where the adjacent `dashboard.new_project_modal.field_key_placeholder` uses **`Selecciona una tonalidad`**. Deliberate — the two render side by side and repeating the same verb reads redundant — but it is a mild verb-choice inconsistency if the style guide wants one canonical "choose".
- `tonalidad` (not `clave`) used for musical *key*, matching `field_key_label` / `project_card_key_label`. Consistent.
- `pista` used for *track* throughout, per the market profile's terminology rules. Consistent with `dashboard.studio.*` and `plan_features.*`.
- Market profile requires AI copy to always carry a control signal and never present the IA as the author. `track_type_midi_description` keeps the user as the grammatical actor (*"Añade una pista MIDI para programar notas con las herramientas de…"*), so authorship stays with the user; no explicit "puedes ajustar / descarta" hedge was added, since the sentence is descriptive rather than generative. Worth a reviewer's eye if the rule is meant to be applied literally to every string mentioning IA.
