# Chief of Staff Template

A NanoClaw template for a chief of staff serving one principal: a founder, owner or head of operations with more work than hours. It keeps the goal and the numbers in view, tracks every open thread, tells the principal what to do with this week's hours, and writes decision memos. It prepares; the principal decides. It never sends anything on their behalf.

Built by Eva Spexard ([Intentional Remote](https://intentionalremote.com)) from the chief of staff agent she runs her own consulting business with.

## Layout

```
chief-of-staff/
├── plugin.json
├── ai.nanoco.nanoclaw/
│   ├── context/
│   │   ├── instructions.md              # the persona: protects the hours, prepares decisions, never sends
│   │   └── additional_context/
│   │       └── memory-structure.md      # principal, plan, threads, decisions, people, hours
│   └── tasks/
│       ├── monday-brief.md              # Mondays 08:00: goal status, threads, top three uses of the week
│       └── monthly-plan-check.md        # 1st of the month 09:00: numbers, drift, one change
├── skills/
│   ├── setup-interview/SKILL.md         # first run: builds memory in a 15-minute interview
│   ├── monday-brief/SKILL.md
│   ├── decision-memo/SKILL.md
│   └── inbox-triage/SKILL.md
├── claude-project/                      # the same role as a Claude or ChatGPT project
│   ├── chief-of-staff.md
│   └── business-context.md
└── README.md
```

## Stamp an agent

```bash
ncl groups create --template operations/chief-of-staff --name "Chief of Staff"
```

Wire it to a channel, say hello, and it runs the setup interview. Both scheduled tasks start paused: turn them on once the setup is done.

## Notes

- **No `mcp.json`.** It works from what the principal tells it. Connecting email or a calendar through OneCLI makes the brief better but isn't required.
- **Drafts only.** Every external message is a draft for the principal. Add sending rights deliberately if you want them.
- **Not on NanoClaw?** The same role works as a Claude or ChatGPT project, or as a skill. See [`claude-project/`](claude-project): paste `chief-of-staff.md` into the project instructions and upload `business-context.md` as a project file.
