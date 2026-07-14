---
description: "Map the current Spec Kit scope into a guarded PatchWarden Goal"
---

# Prepare PatchWarden Evidence Context

Use this optional command before `/speckit.implement` when PatchWarden is configured as an MCP server for the current project.

## Safety boundary

- Work only inside the project workspace accepted by PatchWarden.
- Use only PatchWarden's `create_goal` and `import_speckit_tasks` MCP tools.
- Do not start implementation tasks, run a task loop, or claim that a lineage or verification result exists.
- Do not read, display, or copy secrets, credentials, raw logs, or full diffs.
- Do not publish packages, create releases, push branches, merge pull requests, or deploy.
- If PatchWarden is unavailable, explain that preparation is skipped; do not emulate PatchWarden state.

## Steps

1. Read the current Spec Kit `spec.md`, `plan.md`, and `tasks.md` only as needed to identify the approved task IDs, descriptions, dependencies, acceptance criteria, and declared file scope.
2. Confirm that PatchWarden is connected and that its configured `workspaceRoot` contains the current project.
3. Call `create_goal` with:
   - `repo_path`: the current project path inside `workspaceRoot`;
   - `title`: a concise title derived from the approved specification;
   - `goal_description`: a bounded summary of the approved scope and acceptance criteria.
4. Record the returned `goal_id`. Call `import_speckit_tasks` with that `goal_id` and a minimal `spec_kit_json` object containing only:
   - `spec`;
   - `tasks[]` entries with `id`, `desc`, optional `files`, and optional `depends_on`;
   - `acceptance[]`.
5. Report the `goal_id`, created/skipped subgoal counts, and bounded warnings. State explicitly that this command created only Goal/Subgoal metadata: implementation, task execution, lineage creation, verification, and evidence export remain separate steps.

## Expected result

PatchWarden has a guarded Goal with Spec Kit task IDs mapped to subgoals, declared file scopes mapped to scope hints, dependencies preserved where resolvable, and acceptance criteria recorded. No implementation task or lineage is created by this command.
