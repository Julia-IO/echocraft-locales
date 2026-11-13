# Task: sync locales/es-ES from locales/en-US using Black Ice MCP (Echocraft)

You are running non-interactively in CI. Do not ask questions — make the best
call, note uncertainty in the QA report, and continue.

**Black Ice locale casing**: always pass the locale to Black Ice tools
(`get_market_profile`, `check_term`, `list_concepts`, and any other call that
takes a locale) as lowercase `es-es`, never `es-ES`. The uppercase form does
not error — it silently returns empty fields (`term: null`, `status: null`,
`availability: null`), which would translate with zero terminology
governance without any signal that something's wrong. `locales/es-ES/` file
paths and prose elsewhere in this doc keep the mixed-case form; only the
locale argument passed *into Black Ice tool calls* must be lowercase.

## 1. Scope the change

- Diff `locales/en-US/**/*.json` against the base branch to find new or
  changed keys. Ignore keys that are unchanged.
- For each changed file `locales/en-US/<path>.json`, the target is
  `locales/es-ES/<path>.json` (create the file/dirs if missing, mirroring
  en-US structure exactly — same keys, same nesting).

## 2. Load market context (once per run)

- Call `get_market_profile` on Black Ice for locale `es-es` (lowercase —
  see the locale-casing note above), product Echocraft. Keep the brand
  voice, formality/register, and any market-availability notes in mind
  for every string you write.
- Call `list_concepts` (optionally `list_classes`) for the Echocraft
  ontology if you need to see what domain terms exist before translating.

## 3. Produce each changed string

You are not doing a literal translation. For every changed key, produce a
copy that:

- reads as **native, neutral Spanish** — the kind a Spanish-speaking user
  would recognize as written for them, not translated at them. Avoid
  calques, literal English syntax, and region-specific slang (stay neutral/international es-ES).
- is **original to the English intent**, not to its literal wording. Start
  from what the string is trying to accomplish for the user in that UI
  moment, then write the Spanish that accomplishes the same thing.
- **keeps reference to key terminology already established in the Echocraft
  ontology** — see below.
- **fits the UI it will surface in.** Infer the surface from the key path
  and string content (button, label, toast, error, tooltip, empty state,
  onboarding copy...). Spanish is typically 20-30% longer than English —
  budget for that. For length-constrained surfaces (buttons, tabs, nav
  labels, badges), prioritize a short, natural phrase over a padded literal
  one; when in doubt, look at the character count of the English source as
  a rough ceiling and write to fit it, not past it.

Steps:

1. Identify candidate domain terms in the source string (product features,
   UI actions, Echocraft-specific nouns).
2. Call `check_term` (locale `es-es`, lowercase) on each candidate term to
   get the approved es-ES term, its status, and any forbidden alternatives.
   Never use a term marked
   forbidden or deprecated. Where no approved term exists, choose the most
   natural neutral-Spanish equivalent and sort the term into one of two
   buckets (see step 4b):
   - **Concept exists, no es-es term** (`check_term`/`list_concepts` finds
     the concept but `term` is null): propose your wording with
     `propose_translation` (step 4b). Do **not** send it to
     `suggest_candidates`. A concept with a missing target label is a
     translation gap, not a new concept.
   - **No concept at all** (no match on any concept name or English
     label): this is a new-concept candidate for step 4b.
3. Draft the copy per the criteria above, respecting the market profile's
   register/formality.
4. **Placeholders**: locate every placeholder in the source
   (`{count}`, `{name}`, `%s`, `%1$s`, etc.) and carry every one of them
   into the draft exactly once each — never add, drop, or rename a
   placeholder token. Before drafting, think through how each placeholder
   actually resolves at runtime (a name, a number, a date, a pluralizable
   count) — that's what tells you the natural Spanish word order, since
   Spanish sentence structure around a resolved value often differs from
   English. **Reorder placeholders when Spanish grammar calls for it** —
   the position of `{name}` or `{count}` in the source is not binding, only
   its presence and what it resolves to are. Two cases:
   - **Named placeholders** (`{count}`, `{name}`) can simply be moved to
     wherever they read naturally in the Spanish sentence.
   - **Positional placeholders** (`%s`, `%d`) can only be reordered if the
     format supports explicit positional indices (`%1$s`, `%2$s`); a bare
     `%s`/`%s` pair has no positional syntax to reorder with, so if the
     natural Spanish order would need to swap them, use the indexed form
     instead if the platform supports it, and flag it in the QA report if
     you're not sure the runtime string-formatting call supports indexed
     substitution.
   Once placeholders are placed, make sure the surrounding Spanish grammar
   agrees with what will be substituted there — gender/number agreement
   around a `{name}` or `{count}` placeholder, verb conjugation that
   depends on what fills the slot. If you're genuinely unsure how a
   placeholder resolves at runtime (so you can't judge the right word order
   or agreement), flag it in the QA report rather than guessing silently.
5. Call `validate_translation` on the draft. If it flags a governance
   violation, revise and re-validate (max 2 revision attempts). If it still
   fails after that, write the best available draft anyway, and log it in
   the QA report under "Needs human review" with the reason — never leave
   the key untranslated or block the run.
6. Write the final string into `locales/es-ES/<path>.json`.

## 4. QA / drift pass (after all keys are translated)

- For each newly written string, compare it against existing es-ES strings
  in the same file (and, where relevant, other locale files) for
  terminology and tone consistency — same concept should use the same
  Spanish term every time it appears.
- Check new strings don't contradict established Echocraft product
  messaging already present elsewhere in `locales/es-ES/`.
- **Scan the changed en-US source (not just the es-ES output) for
  structural i18n issues that a straight per-key translation can't fix on
  its own**, including:
  - **Missing plural handling**: a string that embeds a count and has only
    one form (`"{count} song added"`) instead of a plural-aware structure —
    Spanish plural rules don't map 1:1 onto English, so a singular-only
    source key will produce a wrong or awkward es-ES string no matter how
    it's translated.
  - **Concatenated/assembled strings**: source keys that look like they're
    built by joining fragments at runtime (e.g. a sentence split across
    `key.part1` / `key.part2`, or a string with a trailing/leading space
    suggesting concatenation). Flag these — word order and grammatical
    agreement in Spanish often can't reuse the same fragment boundaries as
    English.
  - **Hard-coded English inside a placeholder's expected value** (e.g. a
    placeholder that's documented or named as always resolving to an
    English word/unit).
  - Any placeholder mismatch or word-order concern already caught in step
    3.4.
- This is advisory only. Never fail the build or refuse to write files
  because of a QA finding — log it.

## 4b. Write terminology gaps back to Black Ice

After the QA pass, write both buckets from step 3.2 back to Black Ice, so
nothing stays only in the report. Use the same wording you wrote into
`locales/es-ES/`. Where the UI string uses a verb or shortened form
(e.g. a button), propose the noun/feature-name form as the term and
mention the UI form in the notes.

### Concept exists, no es-es term → `propose_translation`

One call per concept:

- `concept_id`: the concept ID from `check_term`/`list_concepts`
- `locale`: `es-es`
- `term`: your es-ES term (lowercase unless it is a proper name, matching
  how other es-es terms are stored)
- `reason`: "Missing es-es term; used in <string IDs> (localize-es run)"
- `notes`: UI context (surface, length constraint, any short UI form used)

The term is added as PENDING. Black Ice never approves it automatically
and refuses markets that already have an approved term; a refusal is
fine, just count it.

### No concept at all → `suggest_candidates`

Send every term from this bucket in **one** `suggest_candidates` call
(max 50), with, per term:

- `term`: the **English source term** as it appears in `locales/en-US/`
  (the concept would be created in the source language)
- `locale`: `en-us`
- `class_name`: your best match from `list_classes` (omit if none fits)
- `definition`: one sentence inferred from the strings
- `frequency`: number of changed en-US strings using it
- `source_url`: `https://github.com/Julia-IO/echocraft-locales/blob/main/locales/en-US/<file>`
- `translations`: `[{ "locale": "es-es", "term": "<your es-ES wording>",
  "notes": "Context: <UI surface / string IDs>" }]`, so the concept and
  its translation can be approved together. If the tool's schema has no
  `translations` field, leave it out and put the es-ES wording in
  `source_note` instead.
- `source_note`: the string IDs it appears in (`<namespace>:<key.path>`)
- `confidence`: higher when the term recurs across keys or files

Rules:
- Only domain terms (product features, Echocraft-specific nouns, DAW/audio
  concepts). Never send generic UI words ("search", "download", "ready").
- Skip the call entirely if the bucket is empty.
- Repeats are fine: the queue deduplicates server-side and suppresses
  previously rejected terms. The response counts are the only receipt.
- If the call fails (permission, network, validation), do not retry more
  than once and never block the run: list the terms in the QA report under
  "Needs human review" with the error, so nothing is lost.
- The same failure rule applies to `propose_translation`: list the
  concept under "Needs human review" with the error.
- `propose_translation` and `suggest_candidates` are the only Black Ice
  write tools you may call. Never call `set_concept_definition`,
  `set_market_availability`, `add_relationship` or
  `create_relationship_type`.

## 5. Write the QA report

Create `.github/qa/qa-report.md` (overwrite any previous run) with:

- A short summary line: how many keys translated, how many flagged.
- A bulleted list of grammar/placeholder-agreement concerns from step 3.4.
- A bulleted list of the Black Ice ontology terms used listing each term, the status and any brief note if relevant.
- **New-concept candidates**: one line only, from the `suggest_candidates`
  response: how many terms were sent to the Black Ice Candidates queue and
  the counts it returned (added / repeats / previously rejected), e.g.
  "3 candidates sent to the Black Ice queue (2 added, 1 repeat)". Do not
  list the terms. Only if the call failed, list them under "Needs human
  review" with the error.
- **Proposed es-es terms**: one line only: how many `propose_translation`
  calls were made and how many were accepted (pending) or refused, e.g.
  "2 es-es terms proposed in Black Ice (2 pending)". Do not list them,
  except failed calls under "Needs human review".
- A bulleted list of structural i18n issues (plurals, concatenation, etc.)
  from step 4.
- A bulleted list of consistency/drift concerns from step 4.
- If a section has nothing to flag, omit it. If nothing to flag anywhere,
  write a single line: "No issues found."

Keep it terse — this becomes a PR comment, not a report.

## Constraints

- Never edit files under `locales/en-US/`.
- Never edit this prompt file or the workflow file.
- Only write within `locales/es-ES/` and `.github/qa/qa-report.md`.
