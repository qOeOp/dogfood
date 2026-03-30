# Work Item

- Schema version: 2
- State authority: script-only
- State version: 14
- Last operation ID: OP-20260330T183634-78479-WI-0019-accept-review-done-transition-cleanup
- Last transition event: .harness/tasks/WI-0019/history/transitions/TX-20260330T183636-WI-0019-done-to-done.md
- ID: WI-0019
- Title: Ownership-safe work item mutation locks
- Type: control
- Status: done
- Priority: critical
- Owner: Workflow & Automation Lead
- Sponsor: general-manager
- Assignee: none
- Worktree: none
- Claimed at: none
- Claim expires at: none
- Lease version: 2
- Objective: Make work item mutation locks ownership-safe so concurrent task-local writes cannot delete a successor lease and silently drop task-truth updates.
- Ready criteria: Reproduce the concurrent lost-update path, patch the lock release path so a process only releases its own lease, and prove the fix with a bounded concurrency validation slice.
- Done criteria: Concurrent artifact-link writes on one work item no longer lose linked attachments; releasing an expired prior lease cannot delete a successor lease; and validation covers both the reproduction and the fixed path.
- Required artifacts: none
- Current stage owner: Workflow & Automation Lead
- Current stage role: closer
- Next gate: archive
- Founder escalation: not-needed
- Decision status: approved
- Review status: approved
- QA status: not-needed
- UAT status: not-needed
- Acceptance status: approved
- Why it matters: If mutation locks are not ownership-safe, any higher-level controller can silently corrupt task truth under concurrency, which invalidates recovery, review, and compounding semantics.
- Decision needed: Prioritize ownership-safe lease release ahead of additional task-surface features because task truth integrity is foundational.
- Deadline: none
- Due review at: none
- Blocked by: none
- Blocks: none
- Current blocker: none
- Next handoff: none
- Linked attachments: .harness/tasks/WI-0019/attachments/2026-03-30-work-item-mutation-lock-ownership-process-audit.md|process-audit|active;.harness/tasks/WI-0019/attachments/2026-03-30-ownership-safe-mutation-lock-fix-checkpoint-checkpoint.md|checkpoint|approved;.harness/tasks/WI-0019/closure/2026-03-30-ownership-safe-mutation-lock-acceptance-review-brief.md|acceptance-review-brief|approved
- Interrupt marker: none
- Resume target: none
- Created at: 2026-03-30
- Updated at: 2026-03-30
- Archived at: none

## Summary

- Problem: work item mutation locks were not ownership-safe, so an exiting process could delete a successor lease and reopen the same critical section to overlapping writers.
- Why now: the first real artifact-first step under `WI-0017` reproduced a concrete lost-update bug, where three artifact-link transitions succeeded against the same version boundary but task truth retained only one linked source note.
- Persistent risk if unfixed: task truth, recovery, review, and any future high-level controller can all silently lose durable facts under concurrency, which is worse than an explicit failure.
- Non-goals: add automatic retry loops for stale writers, redesign the full task runtime, or resume issue-ledger work before the substrate is trustworthy again.

## Recovery

- Current focus: Move the mutation-lock fix to review now that both the lease-ownership regression and the artifact-link fail-closed regression pass.
- Next command: `cd /Users/vx/WebstormProjects/dogfood/.agents/skills/harness && ./scripts/validate_source_repo.sh && ./scripts/run_state_validation_slice.sh`
- Recovery notes: Targeted lock regression and targeted artifact-link fail-closed regression both pass. Remaining validation noise is currently dominated by the existing entropy-pressure gate and the pre-existing Playwright live-owner probe failure under sandbox permissions, so treat those as separate blockers rather than evidence that the lease fix regressed.

## Workflow Notes

- Seeded by ./.agents/skills/harness/scripts/new_work_item.sh on 2026-03-30.

## Signoff Notes

- Review status starts at pending until the designated reviewer signs off.

## Attachment Notes

- Attach decision, research, review, QA, and output materials under attachments/ as they are created.

## Transition Log

- Created from backlog on 2026-03-30 by ./.agents/skills/harness/scripts/new_work_item.sh.

## Notes

- none
