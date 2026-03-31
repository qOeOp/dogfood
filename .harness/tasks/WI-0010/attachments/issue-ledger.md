# Issue Ledger

- Linked work items: WI-0010


- Date: 2026-03-31
- Owner: Workflow & Automation Lead
- Scope: task-local residual issues only
- Current issue status (update-only ledger; archive gate summary): open
- Gate policy: archive blocks while any issue row is not closed, or while a promoted-to-followup row lacks a follow-up work item
- Covered trigger paths in this slice: tool-failure / user-criticism

## Issues

| ID | Source | Summary | Evidence / artifact reference | Status | Disposition | Follow-up | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- |
| ISSUE-001 | user-criticism | soft confirmation and slice hopping left many active checkpoints while no single slice was fully finished | .harness/tasks/WI-0010/attachments/2026-03-31-single-active-checkpoint-discipline-checkpoint.md | closed | resolved-in-place | none | Resolved in place: runtime and framework now converge on one `checkpoint|active` carrier per task. |
| ISSUE-002 | tool-failure | workspace audit_state_system still fails on pre-existing WI-0017 paused-claim metadata drift | .harness/tasks/WI-0017/task.md | open | open | none | Observed after the single-active-checkpoint fix passed source regression; keep this residual separate from the current slice. |
| ISSUE-003 | process-regression | accepted support slices still left `WI-0010` in `compaction-only`, increased pending active files, and kept the review boundary mixed | .harness/tasks/WI-0010/attachments/2026-03-31-compounding-effectiveness-regression-process-audit.md | open | open | none | Do not start another adjacent support slice until one hotspot slice lowers dominant pressure or an explicit budget raise is written. |
