# Work Item

- Schema version: 2
- State authority: script-only
- State version: 4
- Last operation ID: WI-0016-owner-alignment
- Last transition event: .harness/tasks/WI-0016/history/transitions/TX-20260330T113035-WI-0016-planning-to-planning.md
- ID: WI-0016
- Title: Volatile research gate controller
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
- Objective: Require volatile external recommendations to pass through a bounded evidence lane before they become formal task recommendations or decision inputs.
- Ready criteria: Define the smallest gate that distinguishes trivial lookups from non-trivial volatile recommendations, reuse the existing dispatch, brief, source-note, and memo artifacts, and cover one blocked path plus one fast-lane path.
- Done criteria: Non-trivial volatile recommendations fail closed without the minimum required research artifacts, small fact lookups still retain a lightweight fast path, and validation plus one real dogfood research route prove the distinction works.
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
- Why it matters: Harness cannot claim disciplined evidence handling while volatile external advice still depends on whether the operator happens to remember the research bundle in that moment.
- Decision needed: Adopt a bounded volatile-research gate that requires explicit evidence artifacts for formal recommendations while preserving a fast lane for trivial queries.
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

- Problem: volatile external recommendations still rely too heavily on whether the operator remembers to invoke the research bundle, instead of being routed through a default evidence gate.
- Why now: the runtime already has dispatch, brief, source-note, and memo artifacts, but they are not yet enforced as the default path for non-trivial volatile recommendations.
- Persistent risk if unfixed: harness will keep mixing disciplined evidence-backed guidance with ad hoc latest-info judgment, which weakens both quality and reviewability.
- Non-goals: turn every web lookup into paperwork, eliminate the lightweight fast path for trivial factual queries, or broaden the slice into a universal research bureaucracy.

## Recovery
- Current focus: Make research routing a default controller for serious volatile claims instead of a best-effort habit.
- Next command: Inspect research_ctl.sh, new_research_dispatch.sh, new_research_brief.sh, new_source_note.sh, new_research.sh, and the current volatile-research workflow docs for the narrowest enforceable gate.
- Recovery notes: Do not turn every web lookup into paperwork; the first slice must preserve a low-friction fast lane for small factual queries.
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
