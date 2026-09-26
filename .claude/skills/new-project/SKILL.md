---
name: new-project
description: Create a new project folder from the workspace template and register it in the root PROJECTS.md index.
argument-hint: "<folder-name> <one-line purpose>"
disable-model-invocation: true
---

Create a new project in this workspace.

Input: `$ARGUMENTS`. The first word is the folder name; the rest is the purpose. If the name is missing, ask. If the purpose is missing, ask for one line.

1. **Name.** Normalize the folder name to lowercase kebab-case. Stop and ask if `<workspace-root>/<folder-name>/` already exists.
2. **Copy the template.** Copy `_templates/project/` to `<folder-name>/`. Rename `CLAUDE.template.md` to `CLAUDE.md`.
3. **Fill placeholders** in the three files:
   - `{{name}}`: the folder name
   - `{{purpose}}`: the one-line purpose
   - `{{phase}}`: "Just started"
   - `{{date}}`: today's date as YYYY-MM-DD
4. **Register it.** Add a row to the table in the root `PROJECTS.md`: folder, purpose, phase "Just started", and today's date.
5. **Verify:**
   - no `{{` placeholders remain in the new folder
   - the three files exist
   - the `PROJECTS.md` row was added
   - Show the new folder's tree.
6. **Ask** the user for the first milestone and put it in the new README's status list and log's next steps.
