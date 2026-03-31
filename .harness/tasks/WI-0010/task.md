# Work Item

- Schema version: 2
- State authority: script-only
- State version: 58
- Last operation ID: OP-20260331T112903-28063-WI-0010-update-fields
- Last transition event: .harness/tasks/WI-0010/history/transitions/TX-20260331T112903-WI-0010-in-progress-to-in-progress.md
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
- Required artifacts: process-audit,research-memo
- Current stage owner: Workflow & Automation Lead
- Current stage role: planner
- Next gate: review
- Founder escalation: not-needed
- Decision status: none
- Review status: pending
- QA status: not-needed
- UAT status: not-needed
- Acceptance status: pending
- Why it matters: If accepted support slices keep landing without lowering the dominant entropy pressure, WI-0010 becomes process theater and keeps WI-0020 plus WI-0017 blocked behind the same mixed source boundary.
- Decision needed: Freeze adjacent support slices until one hotspot slice lowers dominant pressure or an explicit budget raise is written.
- Deadline: none
- Due review at: none
- Blocked by: none
- Blocks: none
- Current blocker: none
- Next handoff: Read the new compounding-effectiveness audit and research memo, inspect the current entropy audit and scripts/validate_source_repo.sh diff, then carve one deletion-dominant hotspot slice.
- Linked attachments: /Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0010/attachments/2026-03-29-source-entropy-compaction-process-audit.md|process-audit|draft;/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0010/attachments/2026-03-29-requirements-to-plan-brainstorming-notes.md|brainstorming-notes|draft;.harness/tasks/WI-0010/attachments/2026-03-29-soft-threshold-blocker-semantics-process-audit.md|process-audit|draft;.harness/tasks/WI-0010/attachments/2026-03-30-selector-json-builder-compaction-checkpoint.md|checkpoint|superseded;.harness/tasks/WI-0010/attachments/2026-03-30-selector-json-builder-compaction-process-audit.md|process-audit|draft;.harness/tasks/WI-0010/attachments/2026-03-30-consumer-surface-diagnostic.md|surface-audit|approved;.harness/tasks/WI-0010/attachments/2026-03-30-wrapper-aware-recovery-path-process-audit.md|process-audit|draft;.harness/tasks/WI-0010/attachments/2026-03-30-wrapper-aware-recovery-path-checkpoint.md|checkpoint|superseded;.harness/tasks/WI-0010/attachments/sources/2026-03-31-openai-codex-staying-in-flow-task-queue-and-background-work.md|source-note|approved;./.harness/tasks/WI-0010/attachments/2026-03-31-entropy-auto-interrupt-and-resume-process-audit.md|process-audit|approved;./.harness/tasks/WI-0010/attachments/sources/2026-03-31-openai-background-mode-asynchronous-polling-and-cancel-semantics.md|source-note|approved;.harness/tasks/WI-0010/attachments/2026-03-31-entropy-auto-interrupt-and-selector-routing-checkpoint.md|checkpoint|superseded;.harness/tasks/WI-0010/attachments/2026-03-31-entropy-auto-interrupt-review-slice-checkpoint.md|checkpoint|superseded;/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0010/attachments/2026-03-31-mixed-worktree-review-boundary-process-audit.md|process-audit|approved;/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0010/attachments/2026-03-31-in-progress-vs-review-carrier-vocabulary-process-audit.md|process-audit|approved;/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0010/attachments/2026-03-31-wi-0010-scope-clarification-process-audit.md|process-audit|approved;/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0010/attachments/2026-03-31-entropy-interrupt-must-transfer-focus-process-audit.md|process-audit|approved;.harness/tasks/WI-0010/attachments/2026-03-31-query-work-items-helper-compaction-checkpoint.md|checkpoint|superseded;/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0010/attachments/2026-03-31-query-work-items-helper-compaction-process-audit.md|process-audit|approved;/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0010/attachments/2026-03-31-consent-seeking-pause-regression-process-audit.md|process-audit|approved;.harness/tasks/WI-0010/attachments/2026-03-31-open-work-item-helper-compaction-checkpoint.md|checkpoint|superseded;/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0010/attachments/2026-03-31-open-work-item-helper-compaction-process-audit.md|process-audit|approved;/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0010/attachments/2026-03-31-load-bearing-entropy-reduction-method-process-audit.md|process-audit|approved;.harness/tasks/WI-0010/attachments/2026-03-31-complete-work-item-helper-compaction-checkpoint.md|checkpoint|superseded;/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0010/attachments/2026-03-31-complete-work-item-helper-compaction-process-audit.md|process-audit|approved;/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0010/attachments/2026-03-31-micro-confirmation-hard-guard-gap-process-audit.md|process-audit|approved;.harness/tasks/WI-0010/attachments/2026-03-31-unfinished-slice-accretion-process-audit.md|process-audit|approved;.harness/tasks/WI-0010/attachments/issue-ledger.md|issue-ledger|active;.harness/tasks/WI-0010/attachments/2026-03-31-single-active-checkpoint-discipline-checkpoint.md|checkpoint|active;.harness/tasks/WI-0010/attachments/2026-03-31-should-wi-0010-stop-adjacent-support-slices-until-entropy-pressure-visibly-drops-research-memo.md|research-memo|approved;.harness/tasks/WI-0010/attachments/sources/2026-03-31-github-pull-requests-as-reviewable-change-sets.md|source-note|approved;.harness/tasks/WI-0010/attachments/sources/2026-03-31-github-sub-issues-as-thin-blocker-carriers.md|source-note|approved;.harness/tasks/WI-0010/attachments/sources/2026-03-31-openai-background-mode-explicit-async-status.md|source-note|approved;.harness/tasks/WI-0010/attachments/2026-03-31-compounding-effectiveness-regression-process-audit.md|process-audit|approved
- Interrupt marker: none
- Resume target: none
- Created at: 2026-03-29
- Updated at: 2026-03-31
- Archived at: none

## Summary

- Trigger state: the source active surface is no longer treated as a passive budget meter; it now enters a real cleanup lane where soft-threshold saturation creates or reuses this work item, and zero-headroom saturation escalates into compaction-only handling.
- Why this task exists: user feedback exposed a gap between "audit says ok" and lived experience of nonstop `md` / `sh` growth, and the root cause was a mix of weak cleanup triggering, a broken consumer audit path, and planning surfaces that can formalize ideas before option generation is finished.
- Current compaction stance: subtractive work should focus on the active source working set, not on append-only runtime history under `.harness/tasks/*`, and any future budget raise must stay explicit and justified.
- Reduction method: analyze load-bearing surfaces first, delete non-load-bearing support logic around them second, and only then return to direct optimization of the load-bearing controller itself. In compaction-only mode, default to deletion-dominant cleanup before new feature work.
- Task-scope stance: `WI-0010` still means source cleanup / 减熵. The recent entropy auto-interrupt, acceptance-guard, mutation-lock, and single-active-checkpoint work are real support wins, but they do not satisfy the parent task unless dominant pressure visibly falls or the budget change is made explicit.
- Interrupt-routing stance: when entropy pressure creates or reuses a compaction task that blocks active work, that compaction task should immediately become the active lane. The interrupted task is backgrounded as paused work and should resume only after the compaction blocker clears.
- Compounding-effectiveness stance: accepted support slices no longer count as sufficient progress on `WI-0010` while the audit worsens from `pending-active-files=28` to `47` to `49`, `new-active-files` remains at `9`, and the review boundary stays mixed.
- Trend snapshot: the current dominant hotspot is `scripts/validate_source_repo.sh` with `16` touches in the last 20 commits, so the next bounded source slice should follow that pressure leader instead of opening another adjacent controller lane.
- Resolved support lane: the single-active-checkpoint discipline is now task-local truth and should remain in place, but it is no longer the active `WI-0010` slice because it did not lower the dominant entropy metrics.
- Constraint boundary: current harness can soft-constrain execution continuity through task truth, recovery, and routing, but it still lacks a hard commentary-generation guard that fail-closes micro-confirmation phrasing. That remains a separate framework gap and is not the current active slice here.
- Current subtractive slice: this run is a stop-the-line/writeback slice, not another framework controller edit. The next legitimate source slice is one reviewable hotspot around `scripts/validate_source_repo.sh` that must record before/after entropy metrics and either reduce the dominant pressure or make an explicit budget-raise case.
- Review-boundary stance: because the harness source worktree is still mixed, the honest reviewer entrypoint is now the bounded artifact pair `2026-03-31-entropy-auto-interrupt-review-slice-checkpoint.md` plus `2026-03-31-mixed-worktree-review-boundary-process-audit.md`, not the raw full-file diffs.
- Planning implication: harness does have a `brainstorming-session` bundle, but it is not a mandatory precursor to `requirements-meeting`; this task records the need for an ideation gate so unresolved asks do not harden into rewritable requirement briefs too early.
- Contract correction: the entropy audit no longer treats whole-project total files / total lines or per-bucket line ceilings as the hard gate; the source repo now triggers compaction from change pressure, centered on recent churn, pending active-surface batch size, and net-new surface expansion.

## Recovery
- Current focus: Stop the line on compounding-effectiveness regression. `WI-0010` remains the cleanup / 减熵 lane, but adjacent support-slice expansion is paused until a hotspot slice visibly lowers the dominant pressure or an explicit budget raise is written.
- Next command: cd /Users/vx/WebstormProjects/dogfood && ./.agents/skills/harness/scripts/audit_entropy_budget.sh && sed -n '1,220p' .harness/tasks/WI-0010/attachments/2026-03-31-compounding-effectiveness-regression-process-audit.md && sed -n '1,260p' .harness/tasks/WI-0010/attachments/2026-03-31-should-wi-0010-stop-adjacent-support-slices-until-entropy-pressure-visibly-drops-research-memo.md && git -C ./.agents/skills/harness diff --stat -- scripts/validate_source_repo.sh
- Recovery notes: If the next slice starts in `accept_review_work_item.sh`, `work_item_ctl.sh`, or another adjacent support controller before the `scripts/validate_source_repo.sh` hotspot is evaluated against before/after entropy metrics, treat that as recurrence of the same compounding failure. Keep `WI-0020` and `WI-0017` blocked until the source pressure stops worsening or the budget raise is made explicit.
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
