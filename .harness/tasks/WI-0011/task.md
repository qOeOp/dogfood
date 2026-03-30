# Work Item

- Schema version: 2
- State authority: script-only
- State version: 21
- Last operation ID: OP-20260330T000537-36433-WI-0011-artifact-status-approved
- Last transition event: .harness/tasks/WI-0011/history/transitions/TX-20260330T000538-WI-0011-archived-to-archived.md
- ID: WI-0011
- Title: Shared-scope selector head-of-line blocking
- Type: control
- Status: archived
- Priority: critical
- Owner: codex
- Sponsor: general-manager
- Assignee: none
- Worktree: none
- Claimed at: none
- Claim expires at: none
- Lease version: 2
- Objective: Repair the shared selector/start control surface so multiple open tasks can coexist across separate worktrees without an unrelated review item becoming a global start blocker.
- Ready criteria: Reduce the issue to the shared selector/open/start path when one task is in review and another task is otherwise startable, without changing the per-task task-record model.
- Done criteria: Shared-scope routing no longer implies a single active task, an explicit high-level path exists to start a different eligible task while another remains in review, and validation covers at least one multi-open scenario.
- Required artifacts: none
- Current stage owner: codex
- Current stage role: archive
- Next gate: none
- Founder escalation: not-needed
- Decision status: approved
- Review status: approved
- QA status: not-needed
- UAT status: not-needed
- Acceptance status: approved
- Why it matters: If the shared entry surface serializes all work behind one review item, harness will teach the wrong mental model, underuse parallel agent work, and turn normal multi-task execution into artificial friction.
- Decision needed: Treat concurrent active tasks across separate worktrees as a first-class runtime case and fix selector/start semantics instead of documenting a single-active default.
- Deadline: none
- Due review at: none
- Blocked by: none
- Blocks: none
- Current blocker: none
- Next handoff: none
- Linked attachments: .harness/tasks/WI-0011/attachments/sources/2026-03-29-anthropic-parallel-worktrees-source-note.md|source-note|approved;.harness/tasks/WI-0011/attachments/2026-03-29-shared-selector-concurrency-process-audit.md|process-audit|approved;.harness/tasks/WI-0011/attachments/2026-03-29-explicit-start-concurrency-slice-checkpoint.md|checkpoint|approved;.harness/tasks/WI-0011/attachments/2026-03-29-explicit-start-targeted-validation-checkpoint.md|checkpoint|approved;.harness/tasks/WI-0011/closure/2026-03-30-explicit-start-concurrency-acceptance-review-brief.md|acceptance-review-brief|approved;.harness/tasks/WI-0011/attachments/2026-03-30-explicit-start-concurrency-acceptance-closeout-checkpoint.md|checkpoint|approved
- Interrupt marker: none
- Resume target: none
- Created at: 2026-03-29
- Updated at: 2026-03-30
- Archived at: 2026-03-30T00:05:00+0800

## Summary

- Problem: the current shared `select/open/start` surface behaves like a single-thread queue, so an unrelated task in `review` can become a de facto global blocker for starting another task.
- Why now: this round exposed exactly that mismatch when `WI-0006` in `review` was treated as a reason to finish review before starting other work, even though the runtime contract and worktree docs point to per-task concurrency rather than repo-global singleton execution.
- Persistent risk if unfixed: harness will keep teaching the wrong operator model, suppress parallel agent work in separate worktrees, and make normal multi-task execution feel like a framework violation.
- Non-goals: remove review visibility, allow unsafe concurrent writes in one worktree, or redesign the whole planning/routing model in one pass.

## Recovery
- Current focus: Closed after accepted explicit-start concurrency fix.
- Next command: none
- Recovery notes: If reopened, start from the acceptance brief and closeout checkpoint, then decide separately whether the Playwright broad-slice failure warrants a new follow-up task.
## Workflow Notes

- Seeded by ./scripts/new_work_item.sh on 2026-03-29.

## Signoff Notes

- Review status starts at pending until the designated reviewer signs off.

## Attachment Notes

- Attach decision, research, review, QA, and output materials under attachments/ as they are created.

## Transition Log

- Created from backlog on 2026-03-29 by ./scripts/new_work_item.sh.

## Notes

- none
