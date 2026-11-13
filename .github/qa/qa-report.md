**es-ES sync:** 1 key retranslated (`export.stems_option`), 3 flagged. The other 14 `export.*` keys were already synced and are unchanged. `validate_translation`: 0 violations.

### Black Ice ontology terms used
- Stem Export (feat_00000273): no es-ES term (`term`/`status` null; queried as `es-es`). Used "stems".

### New term candidates
- Stem Export (feat_00000273): proposed "exportación de stems" (feature name) and "Exportar stems" (UI action). The market profile golden example "Exportar pistas separadas (stems)" is 33 chars, which is over the 32-char maximum and nearly 3× the 12-char EN source on an [EXPANSION RISK] checkbox, so I used the short form.

### Structural i18n issues
- `export.stems_count_singular` / `_plural` (carried over): these are still two separate keys, not one ICU `{count, plural, …}` message. Spanish's one/other split works for now, but please migrate.

### Consistency / drift
- `export.stems_option`: the change from "Exportar stems con separación de stems" to "Exportar stems" drops the wrong Stem Separation concept and matches `stems_count_*` ("stem listo/stems listos").
- The terminology rules ask for "stems" to be clarified as "pistas separadas" on first mention. There's no room for that in this checkbox. Consider a tooltip ("Exporta cada pista o bus como un archivo de audio independiente."). Avoid "separación" wording here so it doesn't get confused with Stem Separation.
