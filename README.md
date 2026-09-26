# merlin

A Claude Code workspace that remembers.

One folder for all your projects. Each project keeps its own notes, so any new session picks up where the last one stopped. Three short commands handle the routine, and every mistake Claude makes becomes a rule, so it doesn't happen twice.

We built this to start or continue any project in seconds, without re-explaining everything and without drowning in setup. It works for code and non-code projects alike.

## Quick start

```bash
gh repo create my-workspace --template seymurglv/merlin --private --clone
cd my-workspace
```

No GitHub CLI? Clone it and start a fresh history instead:

```bash
git clone https://github.com/seymurglv/merlin.git my-workspace
cd my-workspace && rm -rf .git && git init
```

Then open Claude Code in that folder and run:

```
/new-project my-first-project what this project is for
```

## Three commands

| Command | When | What it does |
|---|---|---|
| `/sts` | start of a session | Shows every project's phase, the last session, and the next step |
| `/wrp` | end of a session | Writes the handoff into the project's `log.md`, updates status, logs mistakes, commits locally |
| `/new-project` | new idea | Creates a project folder from the template and adds it to `PROJECTS.md` |

The short names are on purpose: they don't clash with Claude Code's built-in commands (there's already a built-in `/status`).

## What's inside

```
.
├── CLAUDE.md            workspace rules + the mistake log
├── PROJECTS.md          one row per project
├── .claude/
│   ├── settings.json    pre-approved safe actions; asks before risky ones
│   ├── skills/          sts, wrp, new-project
│   └── agents/          worker, analyst, deep-researcher
└── _templates/project/  every new project starts with:
    ├── CLAUDE.md        project rules and context
    ├── README.md        what it is + status checklist
    └── log.md           session log, newest first
```

## How we work

- **Plan first, then go.** For anything bigger than a quick fix, agree on the plan, then let Claude run without stopping.
- **Mistakes become rules.** When Claude gets something wrong, it adds a row to the mistake log in `CLAUDE.md`. Every future session reads it.
- **Every session ends with a handoff.** `/wrp` writes what was done, what was decided, and the next step into `log.md`. `/sts` reads it back next time.
- **Verify before "done".** Run it, check it, and say what was checked. Every command ends with a verification step.
- **Helpers on the same model.** The three subagents use `model: inherit` at different effort levels (medium, high, xhigh), so no task quietly lands on a weaker model.
- **Safe permissions, not zero permissions.** Routine actions run without asking, and risky ones always ask.

## Under the hood

- **Two layers of rules.** The root `CLAUDE.md` holds workspace rules; each project's `CLAUDE.md` holds its own. Open Claude Code inside a project folder and it loads both.
- **Permissions** (`.claude/settings.json`):
  - Run without asking: edits inside the workspace, plus git `status`, `diff`, `log`, `add` and `commit`.
  - Always ask, even in auto mode: deleting files, and git `push`, `reset`, `clean`, `checkout` and `restore`.
- **Same model everywhere.** `settings.json` sets `CLAUDE_CODE_SUBAGENT_MODEL_FORCE=1`, so built-in helpers run on your main model too. This needs Claude Code v2.1.257 or later; on older versions, remove the `env` block.
- **Keep it a git repo.** Claude Code's auto memory is keyed to the git repository, so every session in this workspace shares one memory, even sessions opened inside a project folder.

## Make it yours

- **Rules:** add your own under the marked line in `CLAUDE.md` (language, tone, things Claude must never do).
- **Commands:** allow more commands in `.claude/settings.json`, e.g. `"Bash(npm run *)"` or `"Bash(python3 *)"`.
- **Project-only commands:** put them in `<project>/.claude/skills/`.
- **Global gitignore:** if yours ignores `.claude/`, the `!.claude/` line in `.gitignore` keeps this folder in git.

## License

MIT
