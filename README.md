# PatchWarden Evidence Pack for Spec Kit

This community extension adds optional Spec Kit hooks and commands for mapping approved Spec Kit tasks into PatchWarden and exporting a bounded Evidence Pack after an accepted implementation. It is independently maintained and is not an official Spec Kit feature or endorsement.

## What it does

- Before implementation, it can create a guarded PatchWarden Goal and import the current Spec Kit tasks as subgoals.
- After implementation, it can guide an agent to export a bounded evidence pack for an accepted PatchWarden lineage.
- It exposes two commands:
  - `/speckit.patchwarden-evidence.prepare-evidence`
  - `/speckit.patchwarden-evidence.export-evidence <lineage_id>`

The commands are prompts for an AI agent with an already configured PatchWarden MCP server. They do not install, start, or configure PatchWarden themselves.

## Requirements

- Spec Kit with extension support (`>=0.1.0`).
- PatchWarden `>=1.5.1` configured as an MCP server for the target workspace.
- A completed, accepted PatchWarden lineage before evidence export.

## Install

```powershell
specify extension add patchwarden-evidence --from https://github.com/jiezeng2004-design/spec-kit-patchwarden/archive/refs/tags/v1.0.1.zip
```

For local development:

```powershell
specify extension add --dev C:\path\to\spec-kit-patchwarden
```

Verify registration:

```powershell
specify extension list
```

## Usage

1. Configure PatchWarden for the project and connect it to your AI client as an MCP server.
2. Run `/speckit.patchwarden-evidence.prepare-evidence` before implementation, or allow the optional `before_implement` hook.
3. The prepare command calls only `create_goal` and `import_speckit_tasks`. It records Goal/Subgoal metadata and does not execute implementation work or create a lineage.
4. Run the normal Spec Kit implementation workflow through PatchWarden separately and keep the resulting `lineage_id`.
5. After PatchWarden reports an accepted terminal state, run `/speckit.patchwarden-evidence.export-evidence <lineage_id>`, or allow the optional `after_implement` hook.
6. Review the bounded files under `.patchwarden/evidence-packs/<lineage_id>/` with the Spec Kit tasks and acceptance criteria.

## Security and runtime scope

The prepare and export commands have separate, explicit tool scopes:

- **Prepare:** `create_goal` and `import_speckit_tasks` only. These write bounded Goal/Subgoal metadata under PatchWarden's configured workspace. They do not start tasks, run commands, create a lineage, or claim verification.
- **Export:** `get_task_lineage` and `export_task_evidence_pack` only. These inspect accepted bounded lineage state and write the local Evidence Pack.

The extension must not retrieve secrets, raw logs, full diffs, credential files, or out-of-workspace paths. It must not publish, tag, push, merge, deploy, or modify Spec Kit artifacts during export.

An Evidence Pack is supplementary review material. It does not mark a Spec Kit task accepted and does not replace reviewer judgment.

## Development validation

```powershell
specify extension add --dev C:\path\to\spec-kit-patchwarden
specify extension list
specify extension remove patchwarden-evidence
```

## License

MIT. See [LICENSE](LICENSE).
