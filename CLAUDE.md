# ECHOCRAFT Localization Agent

## Ontology
The terminology ontology for this project lives at:
~/echocraft-ontology/

Before any localization task, pull the latest version:
git -C ~/echocraft-ontology pull

Then read the full ontology:
- classes/README.md — concept class definitions
- markets/ — one file per market with locale guidelines  
- terminology/ — one file per concept with approved terms
- relationships/README.md — semantic relationship graph

## String Files
Source strings live in locales/en-US/
Localized versions live in locales/{locale}/
using identical file names and keys.

Locale folder naming follows BCP 47 conventions:
- es-ES — Spanish as used in Spain
- de-DE — German as used in Germany
- fr-FR — French as used in France
- pt-BR — Portuguese as used in Brazil

Always use the exact BCP 47 locale code as the folder name.
Never use shorthand (es, de, fr) — always the full language-region tag.
When a new locale is requested, confirm the correct BCP 47 code
from the markets/ file before creating the folder.

## This Is Not Translation

Do not translate. Transcreate.

The English source string communicates an intent —
a feeling, an action, a relationship with the user.
Your job is to produce copy that achieves that same
intent for the target market, written as if it were
conceived in that language from the start.

Ask: what would a user in this market read here and
feel exactly the right thing? Write that.

## Market
Read the relevant file in markets/ before writing a single string.
That file defines the voice, register, cultural assumptions,
and communication patterns for that market. Apply them throughout.

## Terminology
Before writing any DAW term, AI feature name, product term,
or brand element, look it up in terminology/.
- If the ontology has an approved target term — use it exactly
- If the ontology marks a term as anglicism-preferred — keep it in the source language
- If the ontology marks a term as forbidden — never use it
- If a term is not in the ontology — flag it with [REVIEW] in _notes

## Character Budget
Every string has a display context. Use the string key and
_notes to infer where it appears:
- Badge labels, button text, nav items — tight budget,
  aim for same length or shorter than English
- Card titles, taglines — moderate budget, up to ~30% expansion
- Body copy, hints, legal — generous budget, focus on naturalness

Never sacrifice meaning for length. If a string cannot fit
naturally, flag it with [LENGTH] in _notes for design review.

## Rules
- Never translate JSON keys
- Never translate: ECHOCRAFT, Starter, Pro, Max, MIDI, BPM,
  WAV, FLAC, MP3 — unless ontology explicitly provides a target form
- Keep all placeholders unchanged: {name}, {count}, {plan_name}
- Keep all _notes entries in English
- After completing all files, provide a full report of every
  terminology decision made and every string flagged for review

## Reporting
After completing any localization task, always save a report 
as transcreation-report-{locale}.md in the root of this repo.

The report must include:
- Ontology version pulled (date of last commit)
- A table of every terminology decision made, with columns:
  Source Term | Target Term | Ontology File | Decision
- A list of every string flagged with [REVIEW] and why
- A list of every string flagged with [LENGTH] and the 
  recommended design action
- A step-by-step summary of actions taken in the session

## Committing to GitHub
After saving the transcreation report, ask the user:

"All files are ready. Do you want me to commit and push 
everything to GitHub now? (yes/no)"

If yes, run:
git add .
git commit -m "feat: add {locale} transcreated string files and report"
git push

If no, let the user know they can commit manually when ready.
