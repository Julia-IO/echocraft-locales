**es-ES sync:** 15 keys translated (`export.json`, new file), 8 flagged. `validate_translation`: 0 violations.

### Grammar / placeholder agreement
- `export.loudness_result`: `{lufs}`/`{target_lufs}` must render with a decimal comma in es-ES (`-14,0`, not `-14.0`). Please confirm the runtime number formatting is locale-aware. "Loudness" is treated as masculine ("Loudness integrado"), following common Spanish audio usage.
- `export.progress_label`: wrote `{percent} %` with a space before the sign, per RAE/es-ES convention. `{track_name}` is user content and is left untranslated.
- `export.stems_count_*`: "stem" is treated as masculine ("listo/listos").

### Black Ice ontology terms used
- WAV/FLAC Export → exportación WAV/FLAC (pending)
- MP3 Export → exportación MP3 (approved)
- Mastering Chain → cadena de masterización (pending). The toggle label is 31 chars against 21 in EN, so it may not fit the limited-width toggle row.
- Loudness Analyzer → analizador de loudness (approved)
- Track Metadata Editor → editor de metadatos de pista (pending)
- One-Click Distribution → distribución con un clic (approved). The fixed-width button uses the verb form "Distribuir con un clic" (22 chars). Please confirm this adaptation is acceptable.

### New term candidates
- Stem Separation (feat_00000269): no es-ES term. Used "separación de stems".
- Stem Export (feat_00000273): no es-ES term. Not used directly, but likely the correct concept for `stems_option` (see below).

### Structural i18n issues
- `export.stems_count_singular` / `_plural`: these are two separate keys, not one ICU plural message. Spanish works here because it has the same one/other split, but please migrate to an ICU `{count, plural, …}` message.
- `export.stems_option`: "Export stems with Stem Separation" uses the Stem Separation concept (AI split of a single audio file) in the export dialog. Stem Export (per-track/bus export) seems more likely. The es-ES text "Exportar stems con separación de stems" is redundant and longer than EN (38 vs 33 chars, [EXPANSION RISK]). **Needs human review** of both the source concept and the copy.

### Consistency / drift
- The terminology rules say "stems" should be clarified on first mention ("pistas separadas (stems)"). There's no room for that in the checkbox, so bare "stems" is used.
- `export.metadata_cta` changed from "Edit details in…" to "Abrir editor de metadatos de pista" to avoid repeating "editar … editor".
