# Work Item

- Schema version: 2
- State authority: script-only
- State version: 14
- Last operation ID: WI-0012-done-transition
- Last transition event: .harness/tasks/WI-0012/history/transitions/TX-20260330T133720-WI-0012-review-to-done.md
- ID: WI-0012
- Title: Active claim and pause-resume kernel
- Type: control
- Status: done
- Priority: critical
- Owner: Workflow & Automation Lead
- Sponsor: general-manager
- Assignee: none
- Worktree: none
- Claimed at: none
- Claim expires at: none
- Lease version: 3
- Objective: Promote task claim, worktree ownership, and pause/resume metadata from paper contract to default start, pause, and resume behavior.
- Ready criteria: Reduce the first slice to existing claim and interrupt fields, identify the smallest start/pause/resume write path, and define one validation slice that proves a real paused task can resume cleanly.
- Done criteria: Active tasks always carry non-none claim metadata, pause paths write valid interrupt and resume metadata, resume clears that metadata correctly, and validation plus real dogfood evidence cover the path from start through review.
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
- Why it matters: Long-running work cannot become reliably resumable while active tasks still look unclaimed and pause/resume remains mostly theoretical in task truth.
- Decision needed: Adopt claim and pause/resume enforcement in the task kernel before adding more long-task workflow surfaces.
- Deadline: none
- Due review at: none
- Blocked by: none
- Blocks: none
- Current blocker: none
- Next handoff: none
- Linked attachments: .harness/tasks/WI-0012/attachments/2026-03-30-claim-pause-resume-visible-checkpoint.md|checkpoint|approved;.harness/tasks/WI-0012/closure/2026-03-30-claim-pause-resume-acceptance-review-brief.md|acceptance-review-brief|approved
- Interrupt marker: none
- Resume target: none
- Created at: 2026-03-30
- Updated at: 2026-03-30
- Archived at: none

## Summary

- Problem: claim, worktree, and pause/resume metadata already exist in the runtime contract, but recent dogfood tasks still leave those fields at `none`, so long-running execution has weak durable ownership and weak resume semantics.
- Why now: the current backlog is shifting from single-slice control fixes toward multi-step task completion, and that requires active-task ownership plus a real paused/resume path rather than prose-only recovery.
- Persistent risk if unfixed: harness will keep claiming resumability and worktree isolation while active tasks still behave like loosely tracked chat sessions.
- Non-goals: redesign transport-state handling, add a new lease taxonomy, or broaden this slice into full async callback orchestration.

## Recovery
- Current focus: Closed after accepted claim-visibility and pause-resume proof for the existing kernel path.
- Next command: none
- Recovery notes: Reopen only if active-task claim metadata disappears from the high-level `start/open` surfaces or if the live pause/resume contract regresses. Shared-selector ergonomics, if they recur, should continue as a separate follow-up lane rather than expanding this accepted slice.
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
