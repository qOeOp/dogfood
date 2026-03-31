# Work Item

- Schema version: 2
- State authority: script-only
- State version: 7
- Last operation ID: OP-20260330T213223-6056-WI-0015-link-artifact
- Last transition event: .harness/tasks/WI-0015/history/transitions/TX-20260330T213223-WI-0015-planning-to-planning.md
- ID: WI-0015
- Title: User criticism compounding writeback controller
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
- Objective: Convert user-reported harness, process, or control-surface misses into default durable writeback so criticism does not stop at chat correction.
- Ready criteria: Choose one explicit high-level trigger path, keep the first slice bounded to process-audit plus optional follow-up work item creation, and preserve the existing scope boundary between harness misses and ordinary product feedback.
- Done criteria: A user-reported harness or control-surface miss can be routed through one high-level controller that writes a process-audit and, when appropriate, a linked follow-up work item instead of relying on conversational memory.
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
- Why it matters: If criticism can still be fixed only in chat, harness will continue missing its strongest compounding inputs exactly where users are telling it the execution substrate failed.
- Decision needed: Adopt an explicit criticism-to-writeback controller for harness misses rather than assuming the operator will remember to create durable follow-up truth manually.
- Deadline: none
- Due review at: none
- Blocked by: none
- Blocks: none
- Current blocker: none
- Next handoff: none
- Linked attachments: .harness/tasks/WI-0015/attachments/issue-ledger.md|issue-ledger|active;.harness/tasks/WI-0015/attachments/2026-03-30-harness-intake-auto-load-process-audit.md|process-audit|active
- Interrupt marker: none
- Resume target: none
- Created at: 2026-03-30
- Updated at: 2026-03-30
- Archived at: none

## Summary

- Problem: user-reported harness or control-surface misses can still be corrected in chat without a guaranteed process-audit artifact or linked follow-up work item.
- Why now: earlier compounding tasks fixed the semantics and scope boundary, but the writeback path is still not productized as a narrow high-level controller.
- Persistent risk if unfixed: the strongest real-world compounding signals will continue depending on operator memory instead of becoming durable task truth by default.
- Non-goals: infer every criticism from free-form transcripts automatically, absorb ordinary product feedback into harness work, or redesign the full compounding system in one round.

## Recovery
- Current focus: Turn criticism into a first-class compounding input without pretending free-form transcript interpretation is already solved.
- Next command: Inspect work_item_ctl.sh, new_work_item.sh, link_work_item_artifact.sh, and the current process-audit routing surfaces for the narrowest high-level entrypoint.
- Recovery notes: Start with an explicit controller invocation rather than heuristic transcript mining; preserve the scope boundary fixed by the earlier compounding semantics tasks.
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
