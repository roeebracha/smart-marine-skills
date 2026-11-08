---
name: pick-up-task
description: Turn what a teammate found while testing the app — a bug, a broken flow, or a missing behavior — into an agent-ready Linear ticket in the team's Hebrew format, with type and priority. Use when someone reports a testing finding, shares a screenshot of a problem, or says "pick up task", "open a ticket", "תפתח טיקט", "מצאתי באג", "תכתוב טיקט על זה".
---

# Pick Up Task — from app testing to an agent-ready ticket

Teammates test the app by hand and report what they saw. Turn each finding into a Linear ticket that a coding agent can pick up and fix without coming back with questions.

You don't see the code and you don't need to. Your job is to describe **behavior** precisely: where in the app, under which conditions, what happened, what should happen. Finding the code is the agent's job.

Read these before drafting:
- `references/conventions.md` — Linear team, types, priority rubric, environments
- `references/ticket-template.md` — the ticket structure. Same headings, same order. Never add, drop, or rename sections.
- `references/quality-checklist.md` — the gate every ticket must pass
- `examples/good-ticket.md` — the depth and tone to match

## Hard rules

- **Behavior, not implementation.** Write what the user sees and does. Don't guess at causes, files, or functions. If the tester offers a hypothesis ("I think it's the cache"), keep it, labeled as the tester's unverified hypothesis.
- **One finding per ticket.** A report with several problems becomes several tickets. List them first and confirm the split with the tester.
- **Exact words.** Error messages, toasts, button labels, and URLs are copied verbatim, in backticks. The agent will search for them.
- **Evidence in words.** The agent may not be able to see images. Describe in the ticket what each screenshot shows. The files themselves also get attached to the Linear issue.
- **No secrets, no real user data.** Refer to test accounts by role ("משתמש admin ב-staging"), never by password. If a screenshot or description contains real customer data, tell the tester before anything goes to Linear.
- **Expected behavior is a product decision.** If the tester doesn't know what should happen, ask them to decide or to name who decides. Never leave it to the agent.
- **Never invent a ticket number.** Linear assigns the identifier (e.g. `MARI-42`) when the issue is created.
- **Never create or comment in Linear without an explicit yes.**

## Hebrew writing rules

The ticket is written in Hebrew, read by a coding agent, and displayed in Linear, which renders text left-to-right.
- Prose is in Hebrew, even when the tester wrote in English.
- Technical and UI tokens stay exactly as they appear, inside backticks: URLs and routes, error messages, button labels in English, field names, version numbers.
- No markdown tables in the ticket body. Use bullet lists.
- Start prose lines with a Hebrew word, not an English token, so mixed lines render in readable order.
- Acceptance criteria use the form: בהינתן <מצב>, כאשר <פעולה>, אז <תוצאה נצפית>.

## Workflow

### 1. Read the report
Inputs are the tester's message plus whatever they attach: screenshots, pasted error text, console output, a list of steps. Look at every screenshot and extract the screen, the visible state, any error text, and the data shown.

If the report contains more than one finding, split it now. Then restate each finding in one line — `<סוג>: <מה קרה או מה חסר>`.

**Type** (from `conventions.md`):
- **באג** — the app does something wrong: an error, a crash, wrong data, or behavior that contradicts how it's supposed to work.
- **פיצ׳ר** — the app works as built, but a behavior is missing or should change.
- If you can't tell (e.g. "this screen is confusing"), ask.

### 2. Check for duplicates
If a Linear tool is available, search the team's open issues for the finding's key terms: screen name, error text, URL (in Linear's connector: `list_issues` with the team and a `query`). If you find a likely match, show it (identifier, title, status) and ask: open a new ticket, or add this finding as a comment on the existing one (`save_comment`)?

### 3. Fill the gaps — one round
Required for a **bug**: starting point, numbered steps, expected behavior, actual behavior, frequency, environment.
Required for a **feature**: the situation today, the missing behavior, who needs it and why.

Ask only for what's missing and not visible in the screenshots. One round, max 5 questions, concrete options where possible. Use a multiple-choice question tool when available. Typical gaps:
- Environment, device, browser or app version
- How often it happens (every time? 2 out of 5?)
- What should have happened, if it isn't obvious
- Impact: who is affected, and is there a workaround?

### 4. Set priority
Use the rubric in `conventions.md`. For bugs, decide from the signals: is a core flow blocked, is there a workaround, is there data loss or a security or money issue, how many users are affected, and which environment. Show your choice with a one-line reason; the tester can override it. Never default to דחוף.

### 5. Draft
Fill `references/ticket-template.md` exactly. Remove the guidance comments. For a feature, delete the bug-only lines in section 3.

Sections 1–7 are for people. Verification and agent instructions go in the collapsible `+++ הערות לאייג׳נט` block at the end, which Linear renders folded. Keep the `+++` opening line and the closing `+++` on its own line.

### 6. Quality gate
Run every check in `references/quality-checklist.md`. Fix what you can. Anything still failing goes back to the tester as a specific question. Report the result in one line, e.g. `בדיקת איכות: 17/18 ✅ — ❌ #8 תדירות: קורה כל פעם?`.

Do not hand off a ticket with a failing **blocking** check.

### 7. Deliver to Linear
Show two things:
1. **Linear fields**, one line: team, title, type label, priority, mapped with the tables in `conventions.md`.
2. **The ticket body** in one markdown block, ready to paste into the Linear description.

Then:
- **If a Linear tool is available**, offer to create the issue. On an explicit yes, create it with the team key, title, body as description, priority value, and type label. Linear's connector accepts the team key and label name directly (`save_issue` without an `id` creates). Report the identifier and link, e.g. `נוצר: MARI-42 — <link>`.
- **Screenshots:** if you can read the image file and the connector offers file upload (`prepare_file_upload`), upload each screenshot and embed the returned markdown in the ראיות line. Otherwise remind the tester to drag the screenshots and recordings into the issue in Linear. Either way, the written description of each screenshot stays in the ticket.
- **If no Linear tool is available**, say once that connecting Linear lets you create the issue directly. The tester creates it from the fields line and the body, and attaches the screenshots.

## Anti-patterns to catch in the report

- **"It doesn't work"** — ask what exactly appeared on screen.
- **Steps that start mid-flow** ("click save") — from which screen, logged in as whom, with which data?
- **Several findings in one message** — split them.
- **A solution instead of a problem** ("add a loading spinner") — record the problem ("no feedback for 10 seconds after clicking, so users click again") and keep the idea under "הצעת המדווח".
- **A wish reported as a bug** — if the app behaves as designed and the tester wants it different, it's a פיצ׳ר.
