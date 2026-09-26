---
name: sts
description: Status — show where projects stand — phase, last session, next step. Use at the start of a session or when the user asks "where are we" / "what's next".
argument-hint: "[project-folder]"
---

Give a short status of the workspace projects.

1. Read the project index in the workspace root `PROJECTS.md`.
2. If `$ARGUMENTS` names a project folder, cover only that project. Otherwise, cover every project in the index.
3. For each project, read its `README.md` status checklist and the top entry of its `log.md`.
4. Reply with one compact table:

   | Project | Phase | Last session | Next step |
   |---|---|---|---|

   Under the table, list any open questions that wait on the user, at most 3.
5. Keep it under 15 lines. Don't start any work; this command only reports.
