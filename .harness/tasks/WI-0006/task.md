# Work Item

- Schema version: 2
- State authority: script-only
- State version: 6
- Last operation ID: WI-0006-review
- Last transition event: .harness/tasks/WI-0006/history/transitions/TX-20260329T212240-WI-0006-in-progress-to-review.md
- ID: WI-0006
- Title: Transition obligation kernel slice
- Type: control
- Status: review
- Priority: high
- Owner: codex
- Sponsor: general-manager
- Assignee: none
- Worktree: none
- Claimed at: none
- Claim expires at: none
- Lease version: 2
- Objective: Make lifecycle status transitions fail closed on missing blocking obligations by introducing a machine-readable transition-obligation contract and enforcing it in the state kernel.
- Ready criteria: The first bounded obligation slice is reduced to review->done and done->archived, using only fields and artifact types that already exist in task truth.
- Done criteria: A machine-readable transition-obligation contract gates review->done and done->archived, blocked transitions explain the missing obligation plus owner role/handler kind, and runtime validation covers both the failure and success paths.
- Required artifacts: none
- Current stage owner: codex
- Current stage role: reviewer
- Next gate: acceptance
- Founder escalation: not-needed
- Decision status: none
- Review status: pending
- QA status: not-needed
- UAT status: not-needed
- Acceptance status: pending
- Why it matters: If status changes remain mostly ledger-only, harness will keep allowing silent skips between lifecycle state changes and the process obligations they are supposed to trigger.
- Decision needed: Adopt transition-obligation contract plus fail-closed enforcement as the first lifecycle-process-kernel slice instead of adding more prose-only workflow guidance.
- Deadline: none
- Due review at: none
- Blocked by: none
- Blocks: none
- Current blocker: none
- Next handoff: none
- Linked attachments: none
- Interrupt marker: none
- Resume target: none
- Created at: 2026-03-29
- Updated at: 2026-03-29
- Archived at: none

## Summary

- fill-me

## Recovery
- Current focus: Introduce a machine-readable transition-obligation contract and wire it into transition enforcement without over-expanding the source surface.
- Next command: inspect transition_work_item.sh, lib_state.sh, and run_state_validation_slice.sh around review->done and done->archived
- Recovery notes: Keep the first slice bounded to existing fields and artifact types; defer subagent auto-dispatch and in-progress->review obligations to follow-up work.
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
