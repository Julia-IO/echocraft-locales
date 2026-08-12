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
  calques, literal English syntax, and region-specific slang (no Spain-only
  or Latam-only idioms — stay neutral/international es-ES).
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
   natural neutral-Spanish equivalent and flag it in the QA report as a new
   term candidate.
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

## 5. Write the QA report

Create `.github/qa/qa-report.md` (overwrite any previous run) with:

- A short summary line: how many keys translated, how many flagged.
- A bulleted list of grammar/placeholder-agreement concerns from step 3.4.
- A bulleted list of new term candidates (no approved Black Ice term found)
  from step 3.2.
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
