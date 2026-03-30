# Work Item

- Schema version: 2
- State authority: script-only
- State version: 12
- Last operation ID: WI-0008-to-archived
- Last transition event: .harness/tasks/WI-0008/history/transitions/TX-20260329T215314-WI-0008-done-to-archived.md
- ID: WI-0008
- Title: Compounding target semantics
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
- Objective: Define compounding semantics against the current work object so harness only compounds itself when harness is the active thing being evolved.
- Ready criteria: State the work-object rule clearly, patch the minimum source surfaces, and bind the wording to source validation.
- Done criteria: Canonical instructions say compounding improves the current work object, explicitly note that dogfood harness-iteration rounds target harness, and source/runtime validation pass.
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
- Why it matters: If compounding target semantics are wrong, harness will either hijack user project feedback or overcorrect into thinking it should only ever evolve itself.
- Decision needed: Adopt work-object-relative compounding semantics instead of repo-type-only or harness-only semantics.
- Deadline: none
- Due review at: none
- Blocked by: none
- Blocks: none
- Current blocker: none
- Next handoff: none
- Linked attachments: .harness/tasks/WI-0008/attachments/2026-03-29-compounding-target-semantics-process-audit.md|process-audit|approved;.harness/tasks/WI-0008/closure/2026-03-29-compounding-target-semantics-acceptance-review-brief.md|acceptance-review-brief|approved;.harness/tasks/WI-0008/attachments/2026-03-29-compounding-target-semantics-acceptance-closeout-checkpoint.md|checkpoint|approved
- Interrupt marker: none
- Resume target: none
- Created at: 2026-03-29
- Updated at: 2026-03-29
- Archived at: 2026-03-29T21:53:14+0800

## Summary

- Problem: the narrowed wording from `WI-0007` still framed compounding too much around "harness defects" rather than around the current work object, which is the more general rule the user just clarified.
- Why now: the user corrected the semantic model immediately, before the too-narrow phrasing could harden into the next default.
- Persistent risk if unfixed: harness will keep oscillating between two wrong extremes, either swallowing user project feedback or pretending compounding should only ever improve harness itself.
- Non-goals: broaden compounding back to an unscoped catch-all, or remove the immediate trigger for process/control-surface misses.

## Recovery
- Current focus: Closed after accepted work-object-relative compounding semantics fix.
- Next command: none
- Recovery notes: If reopened, start from the process audit and acceptance brief, verify the active work object is still ambiguous in practice, then rerun source/runtime validation before widening beyond wording+validator enforcement. The next active bounded issue remains `WI-0004`.
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
