# Task: audit locales/es-ES against Black Ice terminology (Echocraft)

You are running non-interactively (scheduled routine or CI). Do not ask
questions — make the best call, note uncertainty in the report, and continue.

This is an **audit**, not a localization pass. You re-check the *whole*
es-ES corpus against the current state of the Black Ice ontology, because
terms can change status, gain forbidden variants, or change market
availability after a string was written.

**Black Ice locale casing**: always pass locales to Black Ice tools as
lowercase (`es-es`, `en-us`), never `es-ES`. The uppercase form does not
error — it silently returns `term: null`, `status: null`,
`availability: null`. If *every* concept comes back null, treat it as a
casing/connection failure: stop and write that as the only finding in the
report instead of reporting the whole ontology as missing.

## 1. Load the ontology (once per run)

- `get_market_profile` for `es-es`.
- `list_concepts` for `es-es` — gives every concept with its es-es term,
  status (`approved` / `pending` / null) and availability (`available` /
  `planned` / `not_available` / null).
- For every concept whose English name or es-es term appears in the
  locale files (step 2), call `check_term` (`es-es`) to get allowed and
  forbidden variants — `list_concepts` does not return them.
- If `.github/qa/audit-baseline.json` exists, load it: it holds the
  `{conceptId: {term, status, availability}}` snapshot from the previous
  audit. If it does not exist, this is the first run — report no status
  changes and just write the baseline.

## 2. Map concepts to strings

For each key in `locales/en-US/**/*.json` (skip `_metadata` and `_notes`),
find which ontology concepts the English string refers to (by concept name,
case-insensitive, allowing plural/inflected forms such as
"Comments & Markers" for "Comment & Marker"). Pair it with the same key in
`locales/es-ES/`. Record file, key path and line number for each hit.

Also collect English domain terms that match **no** concept — these feed
step 4b. Always include every named product feature in feature lists
(e.g. `onboarding.plan_features.*`, `dashboard.nav.*`), even if it appears
only once; for other music-production or UI nouns, include them only if
they recur.

## 3. Run the checks

For every mapped (concept, es-ES string) pair:

1. **Term match** — the es-ES string uses the Black Ice es-es term (allow
   inflection, capitalisation and plural). Flag mismatches.
2. **Forbidden variants** — validate **every** es-ES string that maps to
   at least one concept, not a sample. Batch them: join the strings with
   newlines into one `validate_translation` (`es-es`) call (split into a
   few calls if very long), then attribute each flag back to its key by
   finding the flagged text in the strings. Report every `forbidden` hit;
   list `info` (non-preferred allowed variant) hits separately. Report how
   many strings were validated.
3. **Status change** — compare against the baseline. Report concepts whose
   term, status or availability changed since the last audit, with the
   affected keys.
4. **Market availability** — flag strings that present a concept as part
   of an offer (plan feature lists, onboarding, upsell copy) when its es-es
   availability is `not_available` or `planned`. Treat `not_set` and null
   as unknown: list them once in the report, don't flag each string.

Never edit any locale file. This run reports only.

## 4. Submit ungoverned terms to Black Ice

Split ungoverned terms into two routes — they are different things in
Black Ice:

### 4a. Concept exists, es-es term is null → target label (`propose_translation`)

The English concept is already in the ontology; only the es-ES label is
missing. This is **not** a new-concept candidate. For each such concept,
call `propose_translation` with:

- `concept_id`: the concept ID from `list_concepts`
- `locale`: `es-es`
- `term`: the es-ES wording actually used in `locales/es-ES/`, lowercased
  unless it is a proper name (match the ontology's existing es-es terms)
- `reason`: file, line and key path where the wording ships, e.g.
  "Wording already shipped in locales/es-ES/onboarding.json:183 (key
  plan_features.scale_assistant)". If es-ES uses several renderings for the
  same concept, propose the most frequent one and list the others here.
- `notes`: `Source: https://github.com/Julia-IO/echocraft-locales/blob/main/locales/es-ES/<file>#L<line>`

The term lands as `pending` (never approved by this tool) and Black Ice
refuses it if the market already has an approved term — log a refusal
as a finding, don't retry. Only propose where `check_term` returned
`term: null` on this run; never overwrite an existing pending term.

### 4b. No concept at all → new-concept candidate (`suggest_candidates`)

Recurring domain terms from step 2 that match no concept. Send them in one
`suggest_candidates` call (max 50) with, per term:

- `term`: the **English source term** from `locales/en-US/` (the concept
  would be created in the source language)
- `locale`: `en-us`
- `class_name`: your best match from `list_classes` (omit if none fits)
- `definition`: one sentence inferred from the strings
- `frequency`: number of en-US strings using it
- `source_url`: `https://github.com/Julia-IO/echocraft-locales/blob/main/locales/en-US/<file>#L<line>`
  of the first occurrence
- `source_note`: key paths it appears in, and the es-ES wording currently
  used for it (so the terminologist has the target label ready)
- `confidence`: higher when the term recurs across namespaces

Resubmit every run — the queue deduplicates server-side (a repeat comes
back as `counted_as_repeats`) and suppresses previously rejected terms.
Candidates do not appear in `list_my_proposals`; the `suggest_candidates`
response counts are the only receipt.

### Write-tool limits

`propose_translation` (4a) and `suggest_candidates` (4b) are the only
write tools allowed. Never call `set_concept_definition`,
`set_market_availability`, `add_relationship` or `create_relationship_type`.

## 5. Write outputs

Before overwriting anything, read the current `.github/qa/audit-report.md`
from `main` and keep its findings in mind — step 6 compares against it.

Write `.github/qa/audit-baseline.json`:

```json
{
  "generated": "<ISO date>",
  "concepts": { "<conceptId>": { "term": "...", "status": "...", "availability": "..." } }
}
```

Write `.github/qa/audit-report.md` (overwrite):

- Summary line: strings checked, concepts mapped, findings per check,
  target labels proposed, candidates submitted.
- One section per check from step 3, each a bulleted list of
  `file:line key` → finding. Omit empty sections.
- "Target labels proposed" — concept ID, English name, proposed es-es
  term, proposal status (or refusal reason).
- "New-concept candidates" — en-US term, es-ES wording, frequency, plus
  the response counts (`added` / `counted_as_repeats` /
  `hidden_previously_rejected` / `resurfaced_for_review`) and any `errors`.
- "New since last audit" — at the top, right after the summary line: the
  findings, labels and candidates that were not in the previous report.
  Write "Nothing new since last audit." if empty.
- If nothing to report: a single line "No drift found."

Keep it terse — it becomes the pull request body.

## 6. Decide whether to publish

Publish (commit, push, open a PR) **only if at least one** of these is true:

- a status change was found (step 3.3), i.e. `audit-baseline.json` differs
  from `main` in anything other than `generated`
- a new `forbidden` or `info` flag, term mismatch or availability finding
  that was not in the previous report
- `propose_translation` was called (successfully or refused)
- `suggest_candidates` returned `added` > 0 or `resurfaced_for_review` > 0

Otherwise — only the date or wording changed — do not commit or open a
PR: discard your local changes (`git checkout -- .github/qa`) and finish
with a two-line summary saying the audit found nothing new, with the
`suggest_candidates` counts.

Once the PR is open (or you've decided not to publish), you are done. Do
not subscribe to, watch, or follow up on the PR — a human reviews it.

## Constraints

- Never edit files under `locales/`.
- Never edit prompt or workflow files.
- Only write `.github/qa/audit-report.md` and `.github/qa/audit-baseline.json`.
