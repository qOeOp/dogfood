# Work Item

- Schema version: 2
- State authority: script-only
- State version: 13
- Last operation ID: WI-0005-archive
- Last transition event: .harness/tasks/WI-0005/history/transitions/TX-20260329T210951-WI-0005-done-to-archived.md
- ID: WI-0005
- Title: User-reported process miss compounding trigger
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
- Objective: Make a user-reported harness/process/control-surface miss trigger immediate compounding writeback by default instead of being handled as chat-only correction.
- Ready criteria: Document the failure pattern, choose the minimum canonical instruction surface for the trigger, and bind it to source validation.
- Done criteria: Harness canonical instructions explicitly require immediate task truth plus process-audit escalation for user-reported process misses, source validation enforces the rule, and this dogfood runtime has a durable process-audit artifact for the incident.
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
- Why it matters: If a user has to remind harness to turn process mistakes into compounding work, the framework is not actually self-evolving; it is relying on user babysitting at exactly the layer that claims to absorb operational failure.
- Decision needed: Adopt immediate compounding trigger semantics for user-reported harness/process misses instead of deferring them to optional chat judgment or weekly cadence.
- Deadline: none
- Due review at: none
- Blocked by: none
- Blocks: none
- Current blocker: none
- Next handoff: none
- Linked attachments: .harness/tasks/WI-0005/attachments/2026-03-29-user-reported-process-miss-process-audit.md|process-audit|approved;.harness/tasks/WI-0005/closure/2026-03-29-process-miss-compounding-acceptance-review-brief.md|acceptance-review-brief|approved;.harness/tasks/WI-0005/attachments/2026-03-29-process-miss-compounding-acceptance-closeout-checkpoint.md|checkpoint|approved
- Interrupt marker: none
- Resume target: none
- Created at: 2026-03-29
- Updated at: 2026-03-29
- Archived at: 2026-03-29T21:09:51+0800

## Summary

- Problem: when the user pointed out that I had corrected the immediate issue without turning the workflow miss itself into compounding work, harness did not automatically trigger a process-audit and framework follow-up task; the user had to ask for the meta-fix explicitly.
- Why now: this is a direct contradiction of harness's self-evolution claim, and it was exposed in a live dogfood run immediately after two accepted lifecycle-hardening tasks.
- Persistent risk if unfixed: the framework will keep treating user-reported process misses as optional conversational feedback instead of durable signals that should improve the control surface.
- Non-goals: redesign the whole compounding system, require a role mutation for every process miss, or delay all product/runtime fixes until an expansive governance loop completes.

## Recovery
- Current focus: Closed after accepted process-miss compounding trigger fix.
- Next command: none
- Recovery notes: If reopened for stronger transcript-level enforcement, start from the acceptance brief in closure/ and rerun validate_source_repo.sh, audit_entropy_budget.sh, validate_workspace.sh --mode core, and audit_state_system.sh before widening scope.
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
