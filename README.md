# PatchWarden Evidence Pack for Spec Kit

This community extension adds optional Spec Kit hooks and commands for producing a bounded PatchWarden Evidence Pack alongside a Spec Kit implementation. It is independently maintained and is not an official Spec Kit feature or endorsement.

## What it does

- Before implementation, it can prepare a PatchWarden lineage linked to the current Spec Kit tasks and acceptance criteria.
- After implementation, it can guide an agent to export a bounded evidence pack for an accepted lineage.
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
specify extension add patchwarden-evidence --from https://github.com/jiezeng2004-design/spec-kit-patchwarden/archive/refs/tags/v1.0.0.zip
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
3. Run the normal Spec Kit implementation workflow through PatchWarden and keep the returned `lineage_id`.
4. After PatchWarden reports an accepted terminal state, run `/speckit.patchwarden-evidence.export-evidence <lineage_id>`, or allow the optional `after_implement` hook.
5. Review the bounded files under `.patchwarden/evidence-packs/<lineage_id>/` with the Spec Kit task and acceptance criteria.

## Security and scope

PatchWarden confines its operations to its configured workspace and uses allow-listed operations. This extension instructs agents to use only bounded evidence tools; it must not be used to retrieve secrets, raw logs, full diffs, or credential files. Evidence export is local-only and never publishes, tags, pushes, merges, or deploys.

An Evidence Pack is supplementary review material. It does not mark a Spec Kit task accepted and does not replace reviewer judgment.

## Development validation

```powershell
specify extension add --dev C:\path\to\spec-kit-patchwarden
specify extension list
specify extension remove patchwarden-evidence
```

## License

MIT. See [LICENSE](LICENSE).
