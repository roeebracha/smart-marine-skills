# smart-marine-skills

Shared Claude skills for the team. One plugin for now — `dev-kit` — with one skill:

| Skill | What it does |
|---|---|
| `pick-up-task` | Turns what you found while testing the app — a bug or a missing behavior — into an agent-ready Linear ticket: Hebrew, typed (באג / פיצ׳ר), with priority |

Use it by typing `/` in the chat and picking `pick-up-task`, or just describe what you found: "מצאתי באג במסך…". Attach screenshots — Claude reads them.

**Recommended:** connect Linear (Customize → Connectors → Linear) so Claude can create the issue directly. Linear assigns the number; Claude sets the type label and priority. Without the connector, Claude gives you the fields and the body to paste.

## Install in Claude (web / desktop app) — each teammate, once

Requirements: a paid Claude plan, and **Code execution and file creation** turned on (Settings → Capabilities). Skills don't run without it.

1. Open **Customize** → **Plugins**.
2. Click **Add** → **Add marketplace** → **Add from a repository**.
3. Enter `roeebracha/smart-marine-skills`.
4. Install the **dev-kit** plugin from that marketplace.

That's it. Plugins added this way are saved to your Claude account, so they also show up in Claude Code when you sign in with the same account.

### Getting updates

When the format changes, the owner pushes to this repo. Teammates refresh the marketplace from the Plugins page (**Update**). If a change doesn't appear after updating, add a `version` to `plugins/dev-kit/.claude-plugin/plugin.json` and bump it on every change.

### Fallback: install from a file

If adding the repository doesn't work for someone, upload `pick-up-task.zip` in **Customize** → **Skills** → **+** → **Create skill** → **Upload a skill**. This copy doesn't update itself — re-upload after every format change.

## Install in Claude Code (optional, for developers)

Not needed if you already installed it in Claude with the same account. Otherwise, in a Claude Code session:

```
/plugin marketplace add roeebracha/smart-marine-skills
/plugin install dev-kit@smart-marine-skills
```

## Change the ticket format

The format is data, not logic. Edit these files and push — nothing else needs to change:

| File | Controls |
|---|---|
| `plugins/dev-kit/skills/pick-up-task/references/ticket-template.md` | Ticket sections and order |
| `plugins/dev-kit/skills/pick-up-task/references/conventions.md` | Linear team key, environments, types → labels, priority rubric |
| `plugins/dev-kit/skills/pick-up-task/references/quality-checklist.md` | What blocks a ticket from handoff |
| `plugins/dev-kit/skills/pick-up-task/examples/good-ticket.md` | The reference example Claude imitates — keep it in sync with the template |

After changing the format, rebuild the fallback zip from the repo root:

```bash
(cd plugins/dev-kit/skills && zip -r ../../../pick-up-task.zip pick-up-task)
```

## Add another skill

Create `plugins/dev-kit/skills/<skill-name>/SKILL.md`. Use lowercase words separated by hyphens, and keep the folder name identical to the `name` field. Everyone gets it on their next update.

## Validate before pushing

```bash
claude plugin validate .
```
