# Workspace rules

Shared instructions for every Claude session in this workspace. Project-specific rules live in each project's own `CLAUDE.md`. **Whenever Claude makes a mistake, add a row to the mistake log below**, so it doesn't happen twice.

## Layout

```
.
├── CLAUDE.md            this file: workspace-wide rules
├── PROJECTS.md          project index (one row per project)
├── README.md            documentation for this kit
├── .claude/
│   ├── settings.json    pre-approved safe actions; asks before risky ones
│   ├── skills/          /sts, /wrp, /new-project
│   └── agents/          worker (medium effort), analyst (high), deep-researcher (xhigh)
├── _templates/project/  starting files for every new project
└── <project>/           one folder per project
    ├── CLAUDE.md        project context and rules
    ├── README.md        what it is, structure, status checklist
    └── log.md           session log, newest first; the handoff between sessions
```

## Session routine

- **Start:** run `/sts` before doing anything.
- **End:** run `/wrp` so the next session can pick up where this one stopped. It also commits locally.
- **New project:** run `/new-project <folder-name> <purpose>`. Never create project files in the root.

## How we work

1. **Plan first.** For non-trivial tasks, agree the plan, then execute without stopping.
2. **Verify before saying "done".** Run the code, check that files exist where the READMEs say, and back facts with a source. Say what was checked.
3. **Mistakes become rules.** Add them to the log below.
4. **Repeated work becomes a skill**, in `.claude/skills/` (workspace) or `<project>/.claude/skills/` (project).
5. **Subagents for parallel research and checks.** Use the agents in `.claude/agents/`; they run on the same model as the main session.

## Conventions

- Decisions go into a project's `strategy/` or `decisions` section, and only after the user agrees.
- Keep replies short. Explain new terms with an example.
- **Keep context small.** Each rule is one line. A log entry is a few bullets. Keep every `CLAUDE.md` under 200 lines; when one grows, move the details into the project's own files.

<!-- Add your own rules below: language, tone, things Claude must never do, etc. -->

## Mistake log

| Date | Mistake | Rule now |
|---|---|---|
| YYYY-MM-DD | *(example)* Said "done" without running the script | Run it and show the output before saying done |
