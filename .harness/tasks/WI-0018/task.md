# Work Item

- Schema version: 2
- State authority: script-only
- State version: 13
- Last operation ID: WI-0018-archive
- Last transition event: .harness/tasks/WI-0018/history/transitions/TX-20260330T165253-WI-0018-done-to-archived.md
- ID: WI-0018
- Title: High-level review acceptance and closure controller
- Type: control
- Status: archived
- Priority: critical
- Owner: Workflow & Automation Lead
- Sponsor: general-manager
- Assignee: none
- Worktree: none
- Claimed at: none
- Claim expires at: none
- Lease version: 2
- Objective: Replace manual multi-step review acceptance choreography with one high-level controller that can link the acceptance brief, approve required artifacts and gate fields, and close a bounded review slice atomically.
- Ready criteria: Keep the first slice narrow: identify the exact review-to-done sequence that still requires low-level field orchestration, define one high-level command surface, and prove it can close a bounded review slice without manual version juggling.
- Done criteria: A reviewer can accept a bounded slice through one high-level controller that links the acceptance brief, advances required artifact and gate state, and transitions review to done without manual field sequencing; validation covers both the happy path and at least one blocked obligation path.
- Required artifacts: none
- Current stage owner: Workflow & Automation Lead
- Current stage role: archive
- Next gate: none
- Founder escalation: not-needed
- Decision status: approved
- Review status: approved
- QA status: not-needed
- UAT status: not-needed
- Acceptance status: approved
- Why it matters: If a single review-accept intent still forces the operator to stitch together multiple state mutations, harness is teaching manual state choreography instead of providing a trustworthy control surface.
- Decision needed: Adopt a high-level review acceptance and closure controller instead of normalizing low-level review-state scripting as operator work.
- Deadline: none
- Due review at: none
- Blocked by: none
- Blocks: none
- Current blocker: none
- Next handoff: none
- Linked attachments: .harness/tasks/WI-0018/attachments/2026-03-30-review-acceptance-controller-implementation-checkpoint.md|checkpoint|approved;/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0018/closure/2026-03-30-review-acceptance-controller-acceptance-review-brief.md|acceptance-review-brief|approved
- Interrupt marker: none
- Resume target: none
- Created at: 2026-03-30
- Updated at: 2026-03-30
- Archived at: 2026-03-30T16:52:53+0800

## Summary

- Problem: bounded review acceptance currently succeeds only by stitching together multiple low-level mutations such as artifact linking, artifact approval, gate-field approval, and terminal state transition, which turns a single operator intent into manual state choreography.
- Why now: the `WI-0012` review proved that the underlying state kernel is strong enough to enforce obligations, but it also exposed that closing a review slice still lacks a high-level controller and therefore produces avoidable version-order friction.
- Persistent risk if unfixed: harness will keep teaching operators and models to "carefully push fields until the state machine is satisfied," which is exactly the opposite of what a trustworthy control surface should require.
- Non-goals: redesign every lifecycle stage, replace transition obligations, or absorb unrelated acceptance-ledger and archive-disposition work into this slice.

## Recovery
- Current focus: Bounded review-acceptance controller slice is closed after replayable validation, reviewer brief, and self-hosted accept proof.
- Next command: none
- Recovery notes: Reopen only if the high-level accept surface regresses, replayable evidence stops passing, or artifact path equivalence breaks again; broader completion-surface cleanup remains a separate follow-up lane.
## Workflow Notes

- Seeded by ./scripts/new_work_item.sh on 2026-03-30.

## Signoff Notes

- Review status starts at pending until the designated reviewer signs off.

## Attachment Notes

- Attach decision, research, review, QA, and output materials under attachments/ as they are created.

## Transition Log

- Created from backlog on 2026-03-30 by ./scripts/new_work_item.sh.

## Notes

- none
