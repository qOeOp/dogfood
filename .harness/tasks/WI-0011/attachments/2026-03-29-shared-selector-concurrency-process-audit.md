# Process Audit

- Linked work items: WI-0011



- Date: 2026-03-29
- Owner: codex
- Scope: audit whether the current shared `select/open/start` control surface incorrectly serializes concurrent tasks even though the runtime model and worktree guidance support parallel task ownership
- Signals reviewed:
  - [`/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/scripts/select_work_item.sh`](/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/scripts/select_work_item.sh)
  - [`/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/scripts/open_work_item.sh`](/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/scripts/open_work_item.sh)
  - [`/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/scripts/start_work_item.sh`](/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/scripts/start_work_item.sh)
  - [`/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/scripts/transition_work_item.sh`](/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/scripts/transition_work_item.sh)
  - [`/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/references/contracts/task-record-runtime-tree-v2.toml`](/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/references/contracts/task-record-runtime-tree-v2.toml)
  - [`/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/docs/workflows/worktree-parallelism.md`](/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/docs/workflows/worktree-parallelism.md)
  - [`/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0006/task.md`](/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0006/task.md)
  - [`/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0009/task.md`](/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0009/task.md)
  - [`/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0010/task.md`](/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0010/task.md)
  - external source note on Anthropic parallel worktree guidance
- Repeated frictions:
  - the high-level shared starter currently picks one top open task and can treat an unrelated `review` item as a stop signal for starting any new task in that scope
  - this creates a false operator impression that harness only supports one active task at a time
  - the observed recommendation `finish_review_before_starting_new_work_item` is too global for a runtime that already models per-task claims and worktree isolation
- Cross-task handoff failures:
  - `WI-0006` being in `review` was treated as a general start gate even though `WI-0009` and `WI-0010` still exist as independent open tasks
  - the current shared selector does not expose a first-class way to say "keep the review task open, but start a different bounded task in a different worktree"
- Candidate root causes:
  - `select_work_item.sh` ranks `review` ahead of every other open status and returns one top candidate for the whole shared scope
  - `start_work_item.sh` converts that ranked result into a global recommendation to finish review before starting new work
  - the control surface currently over-compresses "what is top priority" and "what actions are legally possible" into one answer
  - the runtime contract and worktree-parallelism guidance define per-task ownership, but the shared entry surface still behaves like a single-thread queue
- Proposed experiments:
  - add a bounded validation slice with at least two simultaneous open tasks where one task is in `review` and another is `ready`, and assert that the second can still be started explicitly
  - separate "recommended next attention" from "globally legal next start" in the selector/open/start surfaces
  - add an explicit high-level start-by-task-id surface so concurrent task execution does not require dropping down to low-level transition scripts
  - keep claim/worktree checks per task instead of introducing a repo-global single-active invariant
- Risks of change:
  - loosening the starter surface without explicit worktree ownership could create accidental write collisions
  - a naive multi-start surface could hide real priority debt if it removes review visibility entirely
  - if the fix expands too far, it could accidentally redesign the whole planning/routing model instead of repairing the concurrency mismatch
- Recommendation: treat the current behavior as a framework control-surface bug, not as the intended runtime model; preserve per-task claims and worktree isolation, but remove shared-scope head-of-line blocking that turns one `review` item into a global no-start rule
