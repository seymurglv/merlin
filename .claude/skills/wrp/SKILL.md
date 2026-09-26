---
name: wrp
description: Wrap-up — end-of-session handoff. Updates the project's log.md, its README status and the mistake log so the next session can pick up. Use when the user says wrap up, end the session, or save progress.
argument-hint: "[project-folder]"
disable-model-invocation: true
---

Write the handoff for this session.

1. **Which project.** Use `$ARGUMENTS` if given. Otherwise use the project whose files were worked on this session. If it's unclear, or several projects were touched, ask. You may write one entry per project.
2. **Log entry.** Add a new entry at the top of `<project>/log.md` (below the intro line), dated today, with these sections:
   - **Done:** concrete bullets with file paths.
   - **Decisions (user agreed):** only the ones the user explicitly agreed to.
   - **Open:** questions waiting on the user or on data.
   - **Next steps:** numbered, where the first item is the very next action.
3. **Status.** Update the status checklist in `<project>/README.md`, and the phase column in the root `PROJECTS.md` if it changed.
4. **Project rules.** If the project's key files or current phase changed, update `<project>/CLAUDE.md`.
5. **Mistakes.** If Claude made a mistake this session, add a row to the mistake log in the root `CLAUDE.md` (date | mistake | rule now).
6. **Verify before reporting:**
   - every path mentioned in the README and log exists
   - the `PROJECTS.md` phase matches the project's status list
   - State what you checked.
7. **Commit locally:** if the workspace is a git repo, run `git add -A` and `git commit` with a one-line summary. Never push unless the user asks.
8. **Reply** with at most 5 lines: what was saved, and the next step.
