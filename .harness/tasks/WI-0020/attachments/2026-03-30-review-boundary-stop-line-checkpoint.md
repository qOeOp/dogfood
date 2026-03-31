# Status Snapshot

- Linked work items: WI-0020

- Date: 2026-03-30
- Label: review-boundary-stop-line
- Flush boundary: task truth, recovery, research artifacts, process audit, and blocker wiring for `WI-0017` are all written under `.harness/tasks/WI-0020/` and `.harness/tasks/WI-0017/`
- Crash-safe through: selector-chosen `WI-0017` is now explicitly paused and blocked by `WI-0020`; `WI-0020` exists as the durable stop-the-line carrier and is itself blocked by upstream `WI-0010`
- New decisions:
  - Do not accept `WI-0017` from the current mixed embedded harness source worktree.
  - Treat review-boundary collapse as its own explicit blocker instead of leaving it as review prose.
  - Keep the next implementation slice thin and tied to restoring a clean acceptance boundary, not to auto-merging or release-management expansion.
- Open risks:
  - `WI-0010` still owns the upstream entropy-pressure lane, so `WI-0020` cannot be resolved honestly by documentation alone.
  - The exact thin mechanism is still undecided: promotion bundle inventory, acceptance preflight, or another narrowly-scoped boundary check.
- Follow-ups:
  - Resume from `WI-0020` recovery and inspect `WI-0010` plus `accept_review_work_item.sh`.
  - Only resume `WI-0017` after `WI-0020` establishes a reviewable framework source slice again.
- What changed in current state:
  - created `WI-0020` as the blocker task for reviewable framework promotion boundary integrity
  - added approved research dispatch, source notes, and research memo plus an active process audit
  - paused `WI-0017` with `Blocked by: WI-0020` and refreshed both tasks' recovery paths
