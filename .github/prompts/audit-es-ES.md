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
- `list_concepts` for `en-us` — its `term` is each concept's current
  **English label** (the wording en-US strings should use). Match concepts
  across the two calls by `conceptId`, never by name: the ID is stable when
  a concept is renamed, the label is not.
- Call `check_term` (`es-es`) on **every** concept returned by
  `list_concepts` — not a sample, and regardless of whether it appears in
  the locale files (calls can run in parallel). This is the only source of
  allowed/forbidden variants and notes; `list_concepts` does not return
  them, and `validate_translation` only scans approved terms. Report in the
  summary how many concepts were checked and how many have variants
  defined. Use the variants in step 3.1/3.2: an es-ES string containing a
  forbidden variant is a finding even if `validate_translation` missed it.
- If `.github/qa/audit-baseline.json` exists, load it: it holds the
  `{conceptId: {en_term, en_previous_terms, term, status, availability}}`
  snapshot from the previous audit. If it does not exist, this is the first
  run — report no status changes and just write the baseline. If a concept
  in the baseline has no `en_term` yet, record the current one and report
  no English label change for it this run.

## 2. Map concepts to strings

For each key in `locales/en-US/**/*.json` (skip `_metadata` and `_notes`),
find which ontology concepts the English string refers to (by the current
en-us term or concept name, case-insensitive, allowing plural/inflected
forms such as "Comments & Markers" for "Comment & Marker"). Also match the
concept's **retired English labels**: its `en_previous_terms` in the
baseline, plus the baseline `en_term` if it differs from the current one.
A string that uses a retired label still maps to the concept, so its es-ES
pair keeps being checked; record which label it matched for step 3.5.
Pair it with the same key in `locales/es-ES/`. For each hit record the
**string ID**, file and line number.

**String ID** = `<namespace>:<full.key.path>` — the namespace is the file
name without `.json` (it matches `_metadata.namespace`), and the key path
is the complete dot-joined path from the JSON root, including every parent
object: `sample:sample_strings.field_key_helper`, never `field_key_helper`
or `sample.json:12`. Derive IDs mechanically by parsing the JSON (e.g. a
short Python script that walks every file and prints ID, line and value),
not by reading lines by eye, and check each reported ID exists in both
`locales/en-US/` and `locales/es-ES/`. The same ID identifies the en-US
string and its es-ES pair.

Also collect English domain terms that match **no** concept — these feed
step 4b. Always include every named product feature in feature lists
(e.g. `onboarding.plan_features.*`, `dashboard.nav.*`), even if it appears
only once; for other music-production or UI nouns, include them only if
they recur. A term that matches a retired English label is **not**
ungoverned — it belongs to that concept and never goes to step 4b.

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
   es-es term, status or availability changed since the last audit, with
   the affected keys. Report concepts that are new since the baseline
   once, as "new concept" (not a change).
4. **Market availability** — flag strings that present a concept as part
   of an offer (plan feature lists, onboarding, upsell copy) when its es-es
   availability is `not_available` or `planned`. Treat `not_set` and null
   as unknown: list them once in the report, don't flag each string.

Then, once per concept (not per es-ES string):

5. **English label change** — if the current en-us term differs from the
   baseline `en_term`, the concept was renamed in Black Ice. Report it as
   `conceptId: "old label" → "new label"`, then list every string that
   uses the concept in the affected-string format (step 5), marking each
   one **stale** (still uses a retired label) or **in sync** (uses the
   current label). If no string uses the concept, write "No strings
   affected." Retired labels are every label in `en_previous_terms`; the
   current `en_term` is never retired, even if it was retired before (a
   revert moves it back out of the list). Keep
   reporting those keys on every run until en-US stops using the retired
   label — the rename is the news only the first time, but the stale
   strings are a finding each run. Do not judge whether the es-es term
   should change too; note "es-es term unchanged: <term>" so a
   terminologist can decide.

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

Recurring domain terms from step 2 that match no concept (current or
retired English label). Send them in one
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
  "concepts": {
    "<conceptId>": {
      "en_term": "...",
      "en_previous_terms": ["..."],
      "term": "...",
      "status": "...",
      "availability": "..."
    }
  }
}
```

`en_term` is the current en-us term. `en_previous_terms` carries forward
from the previous baseline; when `en_term` changed, append the old value to
it (no duplicates; omit the field while it is empty). Never drop a retired
label — it is how step 2 keeps recognising stale en-US strings.

Write `.github/qa/audit-report.md` (overwrite):

- Summary line: strings checked, concepts mapped, findings per check,
  target labels proposed, candidates submitted.
- One section per check from step 3 (including "English label changes"),
  each listing its findings in the **affected-string format** below. Omit
  empty sections.
- "Target labels proposed" — concept ID, English name, proposed es-es
  term, proposal status (or refusal reason).
- "New-concept candidates" — en-US term, es-ES wording, frequency, plus
  the response counts (`added` / `counted_as_repeats` /
  `hidden_previously_rejected` / `resurfaced_for_review`) and any `errors`.
- "New since last audit" — at the top, right after the summary line: the
  findings, labels and candidates that were not in the previous report.
  Each new finding lists its affected strings here in full too — never
  "see below" or "the keys above". Write "Nothing new since last audit."
  if empty.
- "Resolved since last audit" — right after "New since last audit": every
  finding or flagged string ID in the previous report that is no longer
  flagged, each with a one-line reason (string edited, Black Ice term or
  availability changed back, judged not to apply on review, etc.). Never
  drop a previous finding silently. If the reason is a judgment call,
  say so, so a reviewer can disagree. Omit the section if nothing was
  resolved.
- If nothing to report: a single line "No drift found."

### Affected-string format (mandatory)

Every finding about a concept or label — term mismatch, forbidden or
`info` variant, status change, English label change, new concept used in
strings, market availability, target label proposed — must name **each
affected string individually**, so a reviewer can fix it without opening
the files to find it:

```
- `feat_00000010` Melody Generator → Melody Composer — 3 strings
  - `dashboard:nav.melody_generator` (`locales/*/dashboard.json:15`)
    - en-US: "Melody Generator"
    - es-ES: "Generador de melodías" (expected term: "compositor de melodías")
```

- One bullet per string, **led by its string ID** (step 2), followed by
  the file and line. State how many strings each finding affects.
- Quote the current string text verbatim: the en-US string for English
  label findings, the es-ES string for es-es findings, both when the
  finding concerns the pair. Quote the whole string if it is under ~120
  characters; otherwise quote the sentence containing the term.
- State the term that matched (old label, forbidden variant, etc.) and
  the expected Black Ice term when there is one.
- Never group or abbreviate strings: no `*` wildcards in keys, no
  `136/138/140`, no "and N more", no "see below". Repeat the bullets in
  every section the finding appears in.
- Mentions only in `_notes` are listed the same way, marked `(note)`.
- A finding that affects no string (e.g. a new concept used nowhere)
  says "No strings affected." explicitly.

End the report with **"Affected string IDs"**, split by what each string
needs. Each group is one deduplicated, sorted code block, one ID per line,
followed by the concept IDs and checks that put it there, e.g.
`dashboard:nav.melody_generator  feat_00000010  label-change, term-match`.
Write "None." for an empty group. A string goes in the first group that
applies:

1. **Needs a string fix** — the en-US or es-ES text should change: term
   mismatch against an **approved** term, forbidden variant, stale en-US
   string using a retired label.
2. **Needs a product or terminology decision** — no string edit until
   someone decides: availability findings (`not_available` / `planned`),
   mismatches against a `pending` term, `info` variants, anything where
   Black Ice itself may be wrong (e.g. a likely typo in a term).
3. **Changed in Black Ice, strings already in sync** — listed for
   traceability only, no action: status changes, reverts and newly
   applied labels where the strings already use the current term.

Unknown availability (`not_set` / null) goes in group 2 only if the
string presents the concept as part of an offer. Don't put a string in a
group just because its concept was mentioned elsewhere in the report.

Keep everything else terse — the report becomes the pull request body.

## 6. Decide whether to publish

Publish (commit, push, open a PR) **only if at least one** of these is true:

- a status change, new concept or English label change was found (steps
  3.3 and 3.5), i.e. `audit-baseline.json` differs from `main` in anything
  other than `generated`
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
