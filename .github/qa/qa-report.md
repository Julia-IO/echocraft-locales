# es-ES sync — QA report

**2 keys translated, 2 flagged.** Scope: `locales/en-US/dashboard.json` → `locales/es-ES/dashboard.json` (`projects.project_card_collaborators_singular` / `_plural`). Both drafts passed `validate_translation` (es-es) with zero flags on the first pass.

| Key | en-US | es-ES |
| --- | --- | --- |
| `projects.project_card_collaborators_singular` | `{count} collaborator` | `{count} colaborador` |
| `projects.project_card_collaborators_plural` | `{count} collaborators` | `{count} colaboradores` |

## New term candidates (no approved Black Ice term)

- **collaborator → `colaborador` / `colaboradores`.** `check_term` returned `found: false` for `Collaborator`, `Collaboration`, and `Real-Time Collaboration` in `es-es`; the ontology has no person-role concept for this. Nearest governed neighbour is `Shared Project` = *proyecto compartido* (`feat_00000015`, status `pending`). Chose `colaborador` to match the wording family already shipping in es-ES (`nav.collaboration` = "Colaboración", `onboarding.subheadline` "Crea, colabora y distribuye…"). **Recommend adding a `Collaborator` concept** so this and `nav.collaboration` stop being ungoverned.

## Grammar / placeholder concerns

- `{count}` resolves to an integer and is carried once per string, kept sentence-initial as in the source — natural in Spanish here and consistent with the sibling `project_card_tracks_*` pair. No reordering needed.
- `colaborador/colaboradores` uses generic masculine. A project whose collaborators are all women will still render the masculine form. Standard es-ES practice and unavoidable without a count-aware gender hook, but noting it because the file already carries a `[GENDER HOOK]` flag on `header.greeting_morning` — if the product decides to address that hook, this key belongs in the same sweep.

## Structural i18n issues in the en-US source

- **Split plural keys vs. ICU.** The source note says "Apply ICU plural rules", but the strings ship as two sibling keys (`_singular` / `_plural`) rather than one ICU message (`{count, plural, one{…} other{…}}`). en-US and es-ES both have exactly two plural categories, so this pair is safe — but the pattern will break for locales with `zero`/`few`/`many` (pl-PL, ru-RU, ar) and can't express the es-ES habit of spelling the singular ("un colaborador" instead of "1 colaborador"). Same shape as the pre-existing `project_card_tracks_*` and `notifications_new_*` pairs; flagging as a namespace-wide structural note, not a blocker for this change.

## Consistency / drift

- **Pre-existing, not from this change:** `header._notes.notifications_new_singular` prescribes ES "una nueva notificación", but the shipped es-ES string is `{count} notificación nueva`. The note and the string disagree. The shipped form is the better card/badge copy — suggest correcting the note rather than the string.
- Adjective/noun order in the new keys follows the shipped `{count} pista(s)` pattern, so the card renders consistently across both metrics.
- No length risk: "12 colaboradores" is the same width as "12 collaborators"; no expansion pressure on the project card.

## Note on instructions

The run brief asked for "neutral/international es-ES", while the Black Ice `es-es` market profile mandates español de España (tú/vosotros, no Latam vocabulary). `colaborador` is identical under both readings, so nothing in this change turns on it — the market profile was treated as authoritative.
