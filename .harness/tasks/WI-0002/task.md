# Work Item

- Schema version: 2
- State authority: script-only
- State version: 19
- Last operation ID: WI-0002-archive
- Last transition event: .harness/tasks/WI-0002/history/transitions/TX-20260329T204110-WI-0002-done-to-archived.md
- ID: WI-0002
- Title: Lifecycle coverage blind spot
- Type: control
- Status: archived
- Priority: high
- Owner: codex
- Sponsor: general-manager
- Assignee: none
- Worktree: none
- Claimed at: none
- Claim expires at: none
- Lease version: 2
- Objective: Harden the research/evidence collection path so a terminal tool failure with explicit task context always writes a task-local failure checkpoint and refreshes recovery instead of disappearing into chat.
- Ready criteria: Choose one bounded integration point, define the failure artifact shape, and confirm the change stays framework-generic.
- Done criteria: research_ctl.sh records a task-local failure checkpoint plus recovery update when a task-scoped collection command fails, and state/runtime validation covers that path.
- Required artifacts: process-audit
- Current stage owner: codex
- Current stage role: archive
- Next gate: none
- Founder escalation: not-needed
- Decision status: approved
- Review status: approved
- QA status: not-needed
- UAT status: not-needed
- Acceptance status: approved
- Why it matters: If harness can skip tool failures and leave lifecycle coverage debt implicit, dogfood rounds will overstate system health and under-test the very controls they claim to provide.
- Decision needed: Adopt task-scoped failure checkpoint + recovery writeback in research_ctl as the first generic control-surface hardening slice.
- Deadline: none
- Due review at: none
- Blocked by: none
- Blocks: none
- Current blocker: none
- Next handoff: none
- Linked attachments: .harness/tasks/WI-0002/attachments/2026-03-29-lifecycle-coverage-process-audit.md|process-audit|approved;.harness/tasks/WI-0002/attachments/2026-03-29-research_ctl-ingest-local-tool-failure-203250-checkpoint.md|checkpoint|approved;.harness/tasks/WI-0002/attachments/2026-03-29-failure-writeback-slice-validated-checkpoint.md|checkpoint|approved;.harness/tasks/WI-0002/closure/2026-03-29-failure-writeback-acceptance-review-brief.md|acceptance-review-brief|approved;.harness/tasks/WI-0002/attachments/2026-03-29-failure-writeback-acceptance-closeout-checkpoint.md|checkpoint|approved
- Interrupt marker: none
- Resume target: none
- Created at: 2026-03-29
- Updated at: 2026-03-29
- Archived at: 2026-03-29T20:41:10+0800

## Summary

- Problem: the dogfood run surfaced a control gap where a tool failure (Playwright opening blank tabs and exiting) could be skipped without becoming task truth, while the broader lifecycle surface remained mostly unexercised and therefore easy to overestimate.
- Why now: `WI-0001` proved the minimum-core bootstrap path, but it also showed that one successful happy-path task can make the runtime look healthier than it really is if tool-failure escalation and lifecycle coverage debt stay implicit.
- Persistent risk if unfixed: future self-evolution rounds may keep closing scoped fixes while repeatedly under-testing `paused/resume`, archive discipline, multi-task handoffs, and failure-to-follow-up behavior.
- Non-goals: force every task through every lifecycle state, kill user browser sessions blindly, or redesign all control surfaces in one round.

## Recovery
- Current focus: Closed after accepted failure-writeback control-surface fix.
- Next command: none
- Recovery notes: If reopened for Playwright browser-profile preflight, start from the acceptance brief in closure/ and rerun validate_source_repo.sh, run_state_validation_slice.sh, validate_workspace.sh --mode core, and audit_state_system.sh before scoping a new work item.
## Workflow Notes

- Seeded by ./scripts/new_work_item.sh on 2026-03-29.

## Signoff Notes

- Review status starts at pending until the designated reviewer signs off.

## Attachment Notes

- Attach decision, research, review, QA, and output materials under attachments/ as they are created.

## Transition Log

- Created from backlog on 2026-03-29 by ./scripts/new_work_item.sh.

## Notes

- `WI-0001` is now archived after acceptance, checkpointing, and this follow-up audit, so the archive step is no longer merely theoretical in this dogfood runtime.
- The highest-leverage unresolved question is not "why don't we use every feature"; it is "which skipped failure or coverage debt must become impossible to ignore by default."
