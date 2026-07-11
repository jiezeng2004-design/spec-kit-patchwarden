---
description: "Export bounded PatchWarden evidence for a completed Spec Kit implementation"
---

# Export PatchWarden Evidence

Use this optional command after `/speckit.implement` when the implementation was handled through PatchWarden.

## Input

`$ARGUMENTS` may contain a PatchWarden `lineage_id`. If it is omitted, ask the user for the lineage ID; do not guess one from files or logs.

## Safety boundary

- Use only PatchWarden’s bounded `get_task_lineage` and `export_task_evidence_pack` MCP tools.
- Never request or print raw logs, stdout/stderr, complete diffs, secret values, credential files, or out-of-workspace paths.
- Export is local evidence generation only. Do not publish, push, tag, merge, deploy, or modify the Spec Kit specification artifacts.
- A pack supports review; it does not replace Spec Kit acceptance or reviewer judgment.

## Steps

1. Confirm that PatchWarden is connected for the current workspace and obtain the `lineage_id` from `$ARGUMENTS` or the user.
2. Call `get_task_lineage` with that ID. If it is not in an accepted terminal state, stop and report its bounded status and recommended next action.
3. Call `export_task_evidence_pack` with the same ID.
4. Report only the returned bounded summary: export status, evidence-pack directory, declared changed-file summary, verification status, warnings count, and redaction summary.
5. Tell the reviewer that the pack is supplementary, and link its lineage to the relevant Spec Kit task IDs and acceptance criteria.

## Expected result

PatchWarden writes a local, bounded evidence pack under `.patchwarden/evidence-packs/<lineage_id>/`. The pack contains no raw logs, full diffs, or original secret values.
