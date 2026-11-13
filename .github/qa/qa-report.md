**10 keys translated (`mix_tools.json`, new file), 3 flagged.**

**Black Ice ontology terms used**
- editor MIDI (MIDI Editor): approved
- separación de stems (Stem Separation): no es-es term; proposed. Helper text only, the button uses "Separar en stems".
- exportación de stems (Stem Export): no es-es term; proposed. Matches the pattern of "exportación MP3" / "exportación WAV/FLAC".
- asistente de mezcla inteligente (Smart Mix Assistant): no es-es term; proposed. It doesn't appear in the UI; the button uses the action form.
- asistente de letras (Lyric Assistant): no es-es term; proposed. It doesn't appear in the UI; the button uses the action form.

**New-concept candidates:** 3 candidates sent to the Black Ice queue (2 added, 1 repeat).

**Proposed es-es terms:** 4 es-es terms proposed in Black Ice (4 accepted, returned status "applied" rather than "pending"; please confirm they were not auto-approved).

**Consistency / drift**
- `smart_mix_cta` / `lyric_assistant_cta` / `stem_separation_cta`: to stay within the 22-character button limit, the buttons use verb + object ("Equilibrar mi mezcla", "Pedir ideas de letra", "Separar en stems") and drop the feature name the English source includes. Check whether the product wants the feature name visible.
- `stem_separation_hint`: the profile asks for "stems" to be explained on first mention ("pistas separadas"). It was left out for length. "Tú eliges qué conservar." was added as the AI control signal.
- `panel_title`: the en-US scope says "Mix & AI tools", but the header reads only "Herramientas de mezcla", following the source "Mix tools".
