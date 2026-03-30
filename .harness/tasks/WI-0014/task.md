# Work Item

- Schema version: 2
- State authority: script-only
- State version: 4
- Last operation ID: WI-0014-owner-alignment
- Last transition event: .harness/tasks/WI-0014/history/transitions/TX-20260330T113034-WI-0014-planning-to-planning.md
- ID: WI-0014
- Title: Closeout retro follow-up disposition
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
- Objective: Require every archived task to leave behind an explicit closeout disposition that says whether no follow-up is needed or a concrete follow-up work item should exist.
- Ready criteria: Reduce the first slice to the done-to-archived path, define a minimal closeout checkpoint shape, and prove that archive no longer succeeds without an explicit retro disposition.
- Done criteria: Done-to-archived fails closed without a closeout checkpoint, each archived task records a clear no-followup-needed or follow-up pointer disposition, and validation plus at least one dogfood archive path cover the rule.
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
- Why it matters: If archived tasks can close without an explicit retro disposition, harness keeps finishing work without systematically deciding what should compound into the next iteration.
- Decision needed: Adopt a mandatory closeout disposition lane before archive instead of treating retro and follow-up creation as optional post-task hygiene.
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

- Problem: archived tasks prove that status reached a terminal state, but they do not yet prove that the task left behind an explicit retro disposition about whether follow-up work is needed.
- Why now: recent work has improved process-compounding semantics, but the archive path still does not force the system to say whether a lesson should die here or become the next work item.
- Persistent risk if unfixed: harness will keep finishing tasks cleanly on paper while repeatedly missing small retro insights that should compound into the next iteration.
- Non-goals: create a heavyweight retro ritual, require shared-memory promotion for every task, or broaden this slice into organization-wide postmortem workflow.

## Recovery
- Current focus: Make archive mean both completion and explicit compounding disposition, not only final status mutation.
- Next command: Inspect finalize_work_item.sh, new_checkpoint.sh, transition_work_item.sh, and run_state_validation_slice.sh around done-to-archived enforcement.
- Recovery notes: Keep the checkpoint minimal and task-local; do not broaden this slice into organization-wide retrospectives or shared memory promotion.
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
