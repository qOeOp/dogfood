# Work Item

- Schema version: 2
- State authority: script-only
- State version: 4
- Last operation ID: WI-0013-owner-alignment
- Last transition event: .harness/tasks/WI-0013/history/transitions/TX-20260330T113034-WI-0013-planning-to-planning.md
- ID: WI-0013
- Title: Acceptance ledger default lane
- Type: control
- Status: planning
- Priority: high
- Owner: Workflow & Automation Lead
- Sponsor: general-manager
- Assignee: none
- Worktree: none
- Claimed at: none
- Claim expires at: none
- Lease version: 0
- Objective: Make medium and long-running tasks materialize a task-local acceptance ledger by default instead of relying on closeout prose alone.
- Ready criteria: Define the minimum trigger for when a task requires an acceptance ledger, keep the ledger update-only under attachments, and isolate one blocking path where review cannot complete without the required ledger.
- Done criteria: Tasks that require structured acceptance tracking automatically create or demand an acceptance ledger, review-to-done fails closed when the required ledger is missing or incomplete, and validation covers both the blocked and passing paths.
- Required artifacts: none
- Current stage owner: Workflow & Automation Lead
- Current stage role: planner
- Next gate: ready
- Founder escalation: not-needed
- Decision status: none
- Review status: pending
- QA status: not-needed
- UAT status: not-needed
- Acceptance status: pending
- Why it matters: Without a default acceptance lane, long tasks still appear complete while progress, checklist state, and evidence remain implicit in chat or recovery prose.
- Decision needed: Adopt acceptance-ledger gating for tasks that cross a bounded complexity threshold rather than leaving structured acceptance tracking optional.
- Deadline: none
- Due review at: none
- Blocked by: none
- Blocks: none
- Current blocker: none
- Next handoff: none
- Linked attachments: none
- Interrupt marker: none
- Resume target: none
- Created at: 2026-03-30
- Updated at: 2026-03-30
- Archived at: none

## Summary

- Problem: non-trivial tasks can currently move through review and completion without a structured acceptance artifact, leaving checklist state and evidence implicit in chat, recovery prose, or reviewer memory.
- Why now: if harness is going to improve whole-task completion rather than only status mutation, it needs a default acceptance lane for work that exceeds the lightweight fast-path threshold.
- Persistent risk if unfixed: medium and long-running tasks will continue looking complete before acceptance evidence is actually durable or reviewable.
- Non-goals: require acceptance ledgers for every tiny fix, introduce a second acceptance spec surface, or broaden this slice into product-domain UAT design.

## Recovery
- Current focus: Turn acceptance tracking into a default lane for non-trivial tasks while preserving lightweight fast paths for small fixes.
- Next command: Inspect new_acceptance_ledger.sh, complete_work_item.sh, transition_work_item.sh, and run_state_validation_slice.sh around review-to-done gating.
- Recovery notes: Reuse Required artifacts, Linked attachments, and Acceptance status; avoid creating a second acceptance spec surface.
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
