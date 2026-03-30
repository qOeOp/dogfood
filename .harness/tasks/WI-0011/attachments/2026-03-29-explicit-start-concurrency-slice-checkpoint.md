# Status Snapshot

- Linked work items: WI-0011


- Date: 2026-03-29
- Label: explicit-start-concurrency-slice
- Flush boundary: `start_work_item.sh`, `work_item_ctl.sh`, `run_state_validation_slice.sh`, `validate_source_repo.sh`, and `worktree-parallelism.md` are updated in the working tree; task truth and linked artifact statuses are written back through state scripts.
- Crash-safe through: `WI-0011` is in `in-progress` with current recovery text, an approved source note, an approved process audit, and a linked checkpoint recording the remaining entropy-budget blocker.
- New decisions:
  - Treat shared `select/open` as top-attention routing, not as proof of a repo-global single-active-task invariant.
  - Add a high-level explicit `start --work-item <WI-xxxx>` path rather than redesigning the whole selector in one pass.
  - Explicit task targeting may bypass shared top-item selection, but it must still respect task-local blockers, founder escalation, and scope checks.
- Open risks:
  - `./scripts/validate_source_repo.sh` is still blocked by the active entropy-budget breach, so the slice is functionally validated but not source-accepted yet.
  - Shared default `start shared` still surfaces the review item first by design; the current fix removes the false global prohibition, not the priority ordering itself.
- Follow-ups:
  - Resume `WI-0011` after `WI-0010` or equivalent compaction work clears the entropy-budget gate.
  - If parallel-task ergonomics still feel too implicit after source acceptance, consider a follow-up that exposes alternate startable candidates directly in shared JSON output.
- What changed in current state:
  - `WI-0011` was moved from `planning` to `ready` and then started explicitly while `WI-0006` remained in `review`, proving the bounded concurrency fix in the real dogfood runtime.
  - A new validation regression now checks that shared start remains blocked on the review item by default, while explicit high-level start of another ready task succeeds and claims that task correctly.
