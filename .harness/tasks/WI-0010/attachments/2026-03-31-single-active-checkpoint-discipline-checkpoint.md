# Status Snapshot

- Linked work items: WI-0010
- Date: 2026-03-31
- Label: single-active-checkpoint-discipline
- Flush boundary: `scripts/link_work_item_artifact.sh` now auto-supersedes older `checkpoint|active` entries when a newer checkpoint becomes current, `scripts/set_work_item_artifact_status.sh` can clean legacy multi-active states, `scripts/audit_state_system.sh` now fails on more than one active checkpoint per task, and the transition-obligation contract now blocks `done -> archived` while any checkpoint is still active.
- Crash-safe through: `sh -n` passed for the touched scripts, `./scripts/audit_role_schema.sh` passed, `./scripts/run_state_validation_slice.sh` passed after the archive-gate contract was tightened, and the real dogfood runtime now retains one active checkpoint for both `WI-0010` and `WI-0020`.
- New decisions: treat `checkpoint|active` as the singleton execution carrier for a task; keep open issue ledgers separate from that rule; and require archive to see both a non-active checkpoint disposition and no remaining active checkpoint.
- Open risks: the current workspace `audit_state_system.sh --mode core` still fails on pre-existing `WI-0017` paused-claim metadata drift, so the dogfood runtime still carries at least one unrelated residual state inconsistency outside this slice.
- Follow-ups: inspect the bounded single-active-checkpoint diff and its runtime cleanup first, then continue deletion-oriented entropy work with only one active checkpoint retained per task.
- What changed in current state: `WI-0010` no longer carries a pile of fake-active checkpoint carriers. Older slice checkpoints were compacted to `superseded`, the stale consumer surface diagnostic was approved, the user criticism became both a process audit and an issue-ledger entry, and this checkpoint is now the one active execution boundary.
