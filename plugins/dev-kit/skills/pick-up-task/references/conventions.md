# Team conventions

Edit this file to change team-wide defaults. The skill reads it on every run.

| Setting | Value |
|---|---|
| Ticket language | Hebrew. UI and technical tokens stay as they appear — see "Hebrew writing rules" in SKILL.md |
| Tracker | Linear |
| Linear team | `MARI` (SMART MARINE AI) |
| Ticket number | Linear's issue identifier (e.g. `MARI-42`). Linear assigns it on creation — never invent one |
| Branch naming | Linear's git branch name for the issue. It contains the identifier, so the PR links back to the ticket |

## Environments

Edit to match yours. The tester picks one; if it isn't clear from the report, ask.

- `production` — the live app
- `staging` — the test environment
- `local` — a developer's machine

## Types

Every ticket has exactly one type. If a finding fits none, ask the tester which to use.

| Type in ticket | Linear label | Means |
|---|---|---|
| באג | `Bug` | The app does something wrong |
| פיצ׳ר | `Feature` | The app works as built, but a behavior is missing or should change |

## Priority

Every ticket has exactly one priority. Never default to דחוף. Show the chosen level with a one-line reason.

| Priority in ticket | Linear priority | Bugs | Features |
|---|---|---|---|
| דחוף | Urgent (1) | קריסה או זרימה מרכזית חסומה בלי מעקף ב-production, אובדן או השחתת נתונים, חשיפת מידע, טעות בכסף | חוסם שחרור או לקוח עכשיו |
| גבוהה | High (2) | זרימה מרכזית שבורה אבל יש מעקף, או פוגע בהרבה משתמשים | נדרש בסייקל הנוכחי |
| בינונית | Medium (3) | זרימה משנית שבורה, או בעיה ויזואלית שמטעה את המשתמש | מתוכנן, בלי לחץ זמן |
| נמוכה | Low (4) | קוסמטי: יישור, טקסט, טעות כתיב | Nice to have |

Linear sends a notification to the assignee for Urgent issues — keep דחוף for real emergencies.
