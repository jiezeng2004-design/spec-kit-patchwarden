# Changelog

All notable changes to this extension are documented in this file.

## [1.0.1] - 2026-07-14

### Fixed

- Reconciled the documented runtime-validation scope with the released commands.
- Limited the prepare command to `create_goal` and `import_speckit_tasks`.
- Clarified that preparation creates Goal/Subgoal metadata only; implementation, lineage creation, verification, and export remain separate.
- Documented that export uses only `get_task_lineage` and `export_task_evidence_pack`.

## [1.0.0] - 2026-07-11

### Added

- Optional `before_implement` and `after_implement` hooks for PatchWarden evidence workflows.
- Commands to prepare a lineage and export a bounded Evidence Pack.
