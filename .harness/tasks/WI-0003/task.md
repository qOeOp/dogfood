# Work Item

- Schema version: 2
- State authority: script-only
- State version: 12
- Last operation ID: WI-0003-archive
- Last transition event: .harness/tasks/WI-0003/history/transitions/TX-20260329T204836-WI-0003-done-to-archived.md
- ID: WI-0003
- Title: Transition latest-event ordering collision
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
- Objective: Make latest transition resolution depend on transition metadata rather than filename sort so same-second archive flows remain valid.
- Ready criteria: Reproduce the audit failure, choose one framework-generic ordering rule, and define a deterministic regression.
- Done criteria: lib_state.sh resolves the latest transition event correctly when multiple events share the same second, run_state_validation_slice.sh covers the collision, and source/runtime validators pass.
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
- Why it matters: If archive-time validation can fail because latest-event lookup depends on filename accident, harness still overstates lifecycle coverage right when a task finally exercises archive.
- Decision needed: Adopt version-aware latest transition resolution instead of basename-only ordering for work-item transition history.
- Deadline: none
- Due review at: none
- Blocked by: none
- Blocks: none
- Current blocker: none
- Next handoff: none
- Linked attachments: .harness/tasks/WI-0003/closure/2026-03-29-transition-ordering-acceptance-review-brief.md|acceptance-review-brief|approved;.harness/tasks/WI-0003/attachments/2026-03-29-transition-ordering-acceptance-closeout-checkpoint.md|checkpoint|approved
- Interrupt marker: none
- Resume target: none
- Created at: 2026-03-29
- Updated at: 2026-03-29
- Archived at: 2026-03-29T20:48:36+0800

## Summary

- Problem: when two transition events land in the same second, `latest_transition_event_path()` currently picks the lexicographically last filename rather than the semantically latest event, so a valid `done -> archived` closeout can fail runtime audit.
- Why now: `WI-0002` finally exercised archive closeout with a same-second artifact-status event plus archive event, which exposed that the lifecycle path is still under-covered at the framework contract level.
- Persistent risk if unfixed: accepted tasks can archive into a verifier-failing runtime, making lifecycle coverage look complete even while the canonical transition reader disagrees with the recorded task header.
- Non-goals: redesign the entire transition event format, add sleeps to force wall-clock separation, or broaden this round into Playwright-specific browser-profile repair.

## Recovery
- Current focus: Closed after accepted latest-event ordering fix.
- Next command: none
- Recovery notes: If reopened for broader transition-history API cleanup, start from the acceptance brief in closure/ and rerun validate_source_repo.sh, run_state_validation_slice.sh, validate_workspace.sh --mode core, and audit_state_system.sh before widening scope.
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
