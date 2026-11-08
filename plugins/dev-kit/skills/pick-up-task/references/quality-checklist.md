# Ticket quality gate

Run every check. **Blocking** checks must pass before handoff. Non-blocking failures are reported to the tester but don't stop delivery.

| # | Check | Blocking |
|---|---|---|
| 1 | Title says what happens or what's missing, in Hebrew, at most 70 characters | No |
| 2 | Type is exactly one of the types in `conventions.md` | Yes |
| 3 | Priority follows the rubric in `conventions.md`, with a one-line reason. דחוף is justified in the Goal | Yes |
| 4 | One finding per ticket | Yes |
| 5 | Goal says who is affected and how | Yes |
| 6 | Location: screen or flow, plus URL or route when there is one | Yes |
| 7 | Environment, device, browser or app version, and user role are filled | Yes (bugs) |
| 8 | Bug: starting point, numbered steps, expected, actual, and frequency | Yes (bugs) |
| 9 | Expected behavior is decided by the tester or a named owner, never left to the agent | Yes |
| 10 | Error messages and UI text are verbatim in backticks; every screenshot is described in words | No |
| 11 | No causes, files, or functions presented as fact; the tester's hypothesis is labeled as unverified | Yes |
| 12 | In scope is filled; Out of scope is filled or explicitly "אין" | Yes |
| 13 | Every acceptance criterion is binary and observable in the app | Yes |
| 14 | Edge cases are listed, or marked "אין רלוונטיים" with a reason | No |
| 15 | No open questions remain | Yes |
| 16 | No secrets, passwords, or real customer data in the text or the screenshots | Yes |
| 17 | Self-contained: an engineer who wasn't in this conversation can reproduce and fix from the ticket alone | Yes |
| 18 | Duplicate check done when a Linear tool is available; Hebrew writing rules followed; no ticket number invented | No |

## How to report

One line in Hebrew, then details only for failures:

```
בדיקת איכות: 16/18 ✅
❌ #8 תדירות — לא ידוע אם זה קורה כל פעם; נשאל המדווח
❌ #14 מקרי קצה — לא פורטו (לא חוסם)
```
