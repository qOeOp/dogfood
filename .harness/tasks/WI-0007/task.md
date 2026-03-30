# Work Item

- Schema version: 2
- State authority: script-only
- State version: 12
- Last operation ID: WI-0007-archive
- Last transition event: .harness/tasks/WI-0007/history/transitions/TX-20260329T213639-WI-0007-done-to-archived.md
- ID: WI-0007
- Title: Compounding trigger scope boundary
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
- Objective: Constrain the new process-miss compounding trigger so it applies to harness/framework/runtime/control-surface defects without swallowing ordinary project-domain feedback.
- Ready criteria: State the boundary clearly, choose the minimum source surfaces that carry the rule, and ensure validation checks the scoped wording.
- Done criteria: Canonical instructions distinguish harness/runtime/control-surface misses from project-domain process feedback, validation enforces the scoped rule, and the concern raised in this dogfood round is preserved as task truth.
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
- Why it matters: If the compounding trigger is too broad, harness can overfit to its own self-evolution and interfere with normal project work instead of staying a thin execution substrate.
- Decision needed: Scope the immediate compounding trigger to harness/framework/runtime/control-surface misses rather than all user-reported process feedback.
- Deadline: none
- Due review at: none
- Blocked by: none
- Blocks: none
- Current blocker: none
- Next handoff: none
- Linked attachments: .harness/tasks/WI-0007/closure/2026-03-29-compounding-scope-boundary-acceptance-review-brief.md|acceptance-review-brief|approved;.harness/tasks/WI-0007/attachments/2026-03-29-compounding-scope-boundary-acceptance-closeout-checkpoint.md|checkpoint|approved
- Interrupt marker: none
- Resume target: none
- Created at: 2026-03-29
- Updated at: 2026-03-29
- Archived at: 2026-03-29T21:36:39+0800

## Summary

- Problem: the immediate compounding trigger added in `WI-0005` was directionally correct but too broad, because "user-reported process miss" can be misread as any project-domain workflow feedback rather than specifically a harness/framework/runtime/control-surface defect.
- Why now: the user pointed out the boundary risk immediately after the fix landed, before the over-broad wording could calcify as canonical behavior.
- Persistent risk if unfixed: harness could start absorbing normal project-process feedback into self-evolution work, making the wrapper fatter and blurring framework-vs-consumer responsibility.
- Non-goals: remove the new compounding trigger entirely, redesign all user-feedback handling, or move ordinary project retrospectives into harness-owned workflow by default.

## Recovery
- Current focus: Closed after accepted compounding trigger scope fix.
- Next command: none
- Recovery notes: If reopened for stronger typed feedback handling, start from the acceptance brief in closure/ and rerun validate_source_repo.sh, audit_entropy_budget.sh, validate_workspace.sh --mode core, and audit_state_system.sh before widening scope.
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
