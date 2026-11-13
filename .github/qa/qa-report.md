## es-ES localization QA — `mix_tools.json`

10 keys translated, 3 flagged (all for design review: governed feature names that exceed the button length budget).

### Grammar / placeholders
- No placeholders in the changed strings. Feature terms are written in lowercase mid-sentence (e.g. "Usar asistente de mezcla inteligente"), following how es-es terms are stored.

### Black Ice ontology terms used
- separación de stems — approved
- asistente de mezcla inteligente — pending
- asistente de letras — pending
- exportación de stems — pending (kept distinct from separación de stems, as `_notes` requires)
- mapa de tempo — approved
- editor MIDI — approved ("MIDI" left untranslated)

### New-concept candidates
2 candidates sent to the Black Ice queue (0 added, 2 repeats).

### Proposed es-es terms
0 es-es terms proposed in Black Ice (every matched concept already has an es-es term).

### Structural i18n issues
- `stem_separation_cta`, `smart_mix_cta`, `lyric_assistant_cta`: these buttons put a long feature name inside a sentence, and the English is already 36–39 chars, above the market's 32-char button maximum. A short UI label for each feature, or wider buttons, would fix this at the source.

### Consistency / drift
- These strings replace this branch's earlier es-ES output, which dropped the feature name from three buttons ("Separar en stems", "Equilibrar mi mezcla", "Pedir ideas de letra"). The Black Ice notes on Stem Separation, Smart Mix Assistant and Lyric Assistant still describe those old button forms and should be updated.
- `panel_title` "Herramientas de mezcla" is 22 chars vs 9 in en-US (`_notes`: "Keep short"). No shorter wording sounds natural. The term is not governed; flagged as advisory only.
- `stem_separation_hint` uses "un audio" (common in Spain) to stay ≤120 chars; "un archivo de audio" would be 121.

### Needs design review
- `mix_tools:mix_tools.smart_mix_cta` — "Usar asistente de mezcla inteligente": 36 chars vs 39 en-US (button limit ≤22, max 32). Term: asistente de mezcla inteligente.
- `mix_tools:mix_tools.lyric_assistant_cta` — "Pedir ideas al asistente de letras": 34 chars vs 36 en-US (button limit ≤22, max 32). Term: asistente de letras.
- `mix_tools:mix_tools.stem_separation_cta` — "Usar separación de stems": 24 chars vs 37 en-US (within max 32 but over the 22 target). Term: separación de stems.
