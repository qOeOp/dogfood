# Acceptance Review Brief

- Linked work items: WI-0019


- Date: 2026-03-30
- Host: codex
- Demo slice under review: ownership-safe work item mutation locks for task-truth mutation paths
- What the final reviewer can do right now: inspect the `lib_state.sh` lease-release patch, inspect the new `run_state_validation_slice.sh` regressions, and rerun the targeted lock and artifact-link fail-closed regressions from a fresh fixture
- Acceptance criteria:
  - a process only releases the lock lease it actually acquired
  - a successor lease is not deleted by a prior owner exiting
  - concurrent `link_work_item_artifact.sh` writers fail closed to one winner plus stale-version losers instead of silently dropping linked attachments
- Known boundaries:
  - this slice hardens lease ownership and fail-closed behavior only; it does not add automatic retry loops for stale writers
  - full source validation is still noisy because of unrelated repo-level blockers
- Open risks:
  - `validate_source_repo.sh` still fails on the existing entropy-pressure breach
  - full `run_state_validation_slice.sh` still hits the pre-existing Playwright live-owner probe failure under current sandbox permissions
- Verification date: 2026-03-30
- Sources reviewed:
  - targeted ownership regression pass
  - targeted artifact-link fail-closed regression pass
  - [`2026-03-30-work-item-mutation-lock-ownership-process-audit.md`](/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0019/attachments/2026-03-30-work-item-mutation-lock-ownership-process-audit.md)
  - [`2026-03-30-ownership-safe-mutation-lock-fix-checkpoint-checkpoint.md`](/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0019/attachments/2026-03-30-ownership-safe-mutation-lock-fix-checkpoint-checkpoint.md)
- What remains unverified:
  - whether the unrelated entropy gate and Playwright probe blockers are resolved in the broader repo
- Decisions needed from final reviewer:
  - accept this bounded mutation-lock hardening slice despite unrelated full-suite noise, or require those broader blockers to be cleared before closure
