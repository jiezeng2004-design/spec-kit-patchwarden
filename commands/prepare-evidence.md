---
description: "Prepare a PatchWarden lineage for the current Spec Kit implementation"
---

# Prepare PatchWarden Evidence

Use this optional command before `/speckit.implement` when PatchWarden is configured as an MCP server for the current project.

## Safety boundary

- Work only inside the project workspace accepted by PatchWarden.
- Do not read, display, or copy secrets, credentials, full logs, or full diffs.
- Do not publish packages, create releases, push branches, or merge pull requests.
- If PatchWarden is unavailable, explain that evidence export is skipped; do not emulate an evidence pack.

## Steps

1. Read the current Spec Kit `spec.md`, `plan.md`, and `tasks.md` only as needed to identify the approved task IDs, acceptance criteria, and declared file scope.
2. Confirm that PatchWarden is connected and its configured `workspaceRoot` is the current project root.
3. If the implementation will be delegated through PatchWarden, use its `import_speckit_tasks` tool with a minimal JSON object containing the spec title, task IDs/descriptions, declared file scopes, and acceptance criteria. Do not include secrets or unrelated repository content.
4. Start or continue the project’s normal PatchWarden task workflow. Record the returned `lineage_id` in the task or handoff notes; it is required for export.
5. State the intended scope and the `lineage_id` (if one exists). Do not claim verification has passed before PatchWarden reports an accepted lineage.

## Expected result

A PatchWarden lineage is available for the implementation, with a clear link to the current Spec Kit task IDs and acceptance criteria.
