# es-ES locale sync — QA report

**12 keys translated** (new file `locales/es-ES/settings.json`), **6 flagged**. All 12 drafts passed `validate_translation` with zero governance flags.

## ⚠️ Blocking-severity source issue

- **`locales/en-US/settings.json` at HEAD is corrupted — it is not valid JSON.** Commit `d821c0c` re-added the file with dropped byte ranges: unterminated string literals (`"page_title": "Settings`, `"section_billing": "Bil`), missing key/value separators (`"section_notifications"`, `"delete_account_button"`), and two keys mashed together (`"connected_devices_plurvices"`, `"delete_account_confirmdisplay_name}? This cannot be undone."`). Any parser consuming this file will throw.
- **Recovery used:** the intact original survives at commit `d5baf83` ("Add new settings namespace to en-US locale"). All 12 keys were translated from that version, since translating the corrupted text would have produced nonsense (e.g. `"Bil"`). The en-US file itself was left untouched per the run constraints — **it still needs repair before merge**; `git show d5baf83:locales/en-US/settings.json` is a byte-clean source to restore from.

## New term candidates (no approved Black Ice term)

The Echocraft ontology covers only `Feature`, `Plan`, and `ProductLine` classes — it has **no account/settings domain concepts at all**. Every term below returned `found: false` and was chosen from existing `locales/es-ES/` precedent instead:

- Settings → **Ajustes** (matches `dashboard.nav.settings`)
- Account → **Cuenta** · Billing → **Facturación** · Notifications → **Notificaciones**
- Email address → **Correo electrónico** · Password → **Contraseña**
- Connected device → **dispositivo conectado**
- Danger zone → **Zona de peligro** — lowest-confidence pick. Chose the conventional settings-UI rendering for recognizability over the softer "Zona de riesgo", which sits closer to the profile's no-drama tone. Worth a terminologist's call.

Recommend adding a settings/account class to the ontology before the next sync, or these 12 strings will keep re-deciding themselves.

## Structural i18n issues in the en-US source

- **`connected_devices_singular` / `_plural` are two flat keys, not an ICU plural structure**, despite the `_notes` instructing "Apply ICU plural rules". Spanish is one/other like English so the two-key shape happens to survive here, but **zero must route to the plural key** (`0 dispositivos conectados`, not `0 dispositivo conectado`). If the runtime selects singular for `count == 1` only and falls through to plural otherwise, this is correct as written; if it does `count === 1 ? sing : plural` the zero case is already right. Flagging because the source shape can't express the rule itself. Matches the existing `dashboard.projects.project_card_tracks_*` pattern, so this is a repo-wide convention, not a new defect.
- **`delete_account_confirm` embeds a vocative name**: `Delete your account, {display_name}?` The Spanish keeps `{display_name}` in direct address after a comma, which needs no gender agreement — the `[GENDER HOOK]` risk noted on similar keys (`onboarding.confirmation.page_title`, `dashboard.header.greeting_*`) does **not** apply here. No adjective agrees with the name in this phrasing.

## Placeholders

- All placeholders carried 1:1: `{count}` ×2, `{display_name}` ×1. None added, dropped, renamed, or reordered — Spanish word order matched the source in every case, so no positional-index concerns arose.

## Consistency / drift

- Anchored to existing es-ES precedent rather than re-translating: `Ajustes` ← `dashboard.nav.settings`; `Correo electrónico` ← `onboarding.signup.field_email_label`; `Contraseña` ← `onboarding.signup.field_password_label`; `Notificaciones` ← `dashboard.header.notifications_label`; `Eliminar` ← `dashboard.projects.project_card_delete`.
- `delete_account_confirm` deliberately reuses the established destructive-confirm cadence `¿Eliminar …? Esta acción no se puede deshacer.` from `dashboard.projects.project_card_delete_confirm`.
- **Brief/profile conflict, resolved toward the profile:** the run brief asked for *neutral/international* Spanish avoiding Spain-only vocabulary, but the Black Ice `es-es` profile mandates *"español de España únicamente · sin vocabulario latinoamericano · tú/vosotros por defecto"*. Followed the profile (it is the governing artifact for this locale) while picking vocabulary that is Spain-correct yet not Spain-exclusive, so nothing here reads as regional slang. Called out in case the brief's neutrality goal was the intended one.
- `_notes` and `_metadata` mirror en-US structure; notes left in English, consistent with all four existing es-ES files.
