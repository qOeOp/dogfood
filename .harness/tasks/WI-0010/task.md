# Work Item

- Schema version: 2
- State authority: script-only
- State version: 15
- Last operation ID: OP-20260330T172110-43940-WI-0010-link-artifact
- Last transition event: .harness/tasks/WI-0010/history/transitions/TX-20260330T172110-WI-0010-in-progress-to-in-progress.md
- ID: WI-0010
- Title: Source entropy compaction trigger
- Type: control
- Status: in-progress
- Priority: critical
- Owner: Workflow & Automation Lead
- Sponsor: general-manager
- Assignee: codex
- Worktree: /Users/vx/WebstormProjects/dogfood
- Claimed at: 2026-03-30T10:22:41+0800
- Claim expires at: 2026-03-30T14:22:41+0800
- Lease version: 1
- Objective: Reduce source-surface entropy when the harness active surface crosses the configured trigger threshold, and ensure any net-new control surface carries explicit survivor disposition.
- Ready criteria: Confirm the current entropy state, identify the smallest merge/compress/archive/delete candidates, and separate active-source cleanup from expected runtime history growth.
- Done criteria: A compaction plan or merged change reduces ambiguity in the active source surface, the trigger rationale is documented, and any required budget raise is explicit.
- Required artifacts: process-audit
- Current stage owner: codex
- Current stage role: executor
- Next gate: review
- Founder escalation: not-needed
- Decision status: none
- Review status: pending
- QA status: not-needed
- UAT status: not-needed
- Acceptance status: pending
- Why it matters: When soft-threshold entropy pressure is written back as a hard source-validation failure, downstream task truth becomes more restrictive than the actual controller and future resumes follow the wrong gate.
- Decision needed: Keep soft-threshold entropy in explicit compaction/decision space instead of representing it as a hard downstream source-validation failure.
- Deadline: none
- Due review at: none
- Blocked by: none
- Blocks: none
- Current blocker: none
- Next handoff: none
- Linked attachments: /Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0010/attachments/2026-03-29-source-entropy-compaction-process-audit.md|process-audit|draft;/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0010/attachments/2026-03-29-requirements-to-plan-brainstorming-notes.md|brainstorming-notes|draft;.harness/tasks/WI-0010/attachments/2026-03-29-soft-threshold-blocker-semantics-process-audit.md|process-audit|draft;.harness/tasks/WI-0010/attachments/2026-03-30-selector-json-builder-compaction-checkpoint.md|checkpoint|active;.harness/tasks/WI-0010/attachments/2026-03-30-selector-json-builder-compaction-process-audit.md|process-audit|draft;.harness/tasks/WI-0010/attachments/2026-03-30-consumer-surface-diagnostic.md|surface-audit|active;.harness/tasks/WI-0010/attachments/2026-03-30-wrapper-aware-recovery-path-process-audit.md|process-audit|draft;.harness/tasks/WI-0010/attachments/2026-03-30-wrapper-aware-recovery-path-checkpoint.md|checkpoint|active
- Interrupt marker: none
- Resume target: none
- Created at: 2026-03-29
- Updated at: 2026-03-30
- Archived at: none

## Summary

- Trigger state: the source active surface is no longer treated as a passive budget meter; it now enters a real cleanup lane where soft-threshold saturation creates or reuses this work item, and zero-headroom saturation escalates into compaction-only handling.
- Why this task exists: user feedback exposed a gap between "audit says ok" and lived experience of nonstop `md` / `sh` growth, and the root cause was a mix of weak cleanup triggering, a broken consumer audit path, and planning surfaces that can formalize ideas before option generation is finished.
- Current compaction stance: subtractive work should focus on the active source working set, not on append-only runtime history under `.harness/tasks/*`, and any future budget raise must stay explicit and justified.
- Planning implication: harness does have a `brainstorming-session` bundle, but it is not a mandatory precursor to `requirements-meeting`; this task records the need for an ideation gate so unresolved asks do not harden into rewritable requirement briefs too early.
- Contract correction: the entropy audit no longer treats whole-project total files / total lines or per-bucket line ceilings as the hard gate; the source repo now triggers compaction from change pressure, centered on recent churn, pending active-surface batch size, and net-new surface expansion.

## Recovery
- Current focus: Keep WI-0010 on wrapper-aware recovery and minimum-core task-local audit writeback: the consumer diagnostic lane is now real and should drive the next entropy decision.
- Next command: Review .harness/tasks/WI-0010/attachments/2026-03-30-consumer-surface-diagnostic.md, then choose whether the next bounded slice is freshness-follow-up or another subtractive active-surface cleanup using the new task-local audit lane.
- Recovery notes: This round fixed cwd-correct command echoing for the embedded harness source repo, added --work-item support to run_surface_diagnostic.sh, linked a real consumer surface-audit artifact to WI-0010, validated workspace/state checks in the dogfood runtime, and confirmed source validation still fails for the pre-existing breached entropy gate rather than for this slice.
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
