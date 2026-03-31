# Work Item

- Schema version: 2
- State authority: script-only
- State version: 17
- Last operation ID: WI-0020-restore-current-active-checkpoint
- Last transition event: .harness/tasks/WI-0020/history/transitions/TX-20260331T111530-WI-0020-planning-to-planning.md
- ID: WI-0020
- Title: Reviewable framework promotion boundary
- Type: control
- Status: planning
- Priority: critical
- Owner: Workflow & Automation Lead
- Sponsor: general-manager
- Assignee: none
- Worktree: none
- Claimed at: none
- Claim expires at: none
- Lease version: 0
- Objective: Make review and acceptance fail closed when a selected framework review item no longer maps to a clean embedded harness source slice because unrelated pending mutations share the same promotion boundary.
- Ready criteria: Confirm the stop-the-line signal on the real dogfood runtime, capture fresh external evidence for thin blocker/dependency handling, and reduce the first fix to one review-boundary restoration mechanism rather than a broad release workflow.
- Done criteria: WI-0017 or any similar review item can no longer be accepted from a mixed framework worktree without an explicit blocker; WI-0020 leaves behind a durable process audit and research memo; and recovery points at the next thin mechanism to restore a clean reviewable boundary.
- Required artifacts: process-audit,research-memo
- Current stage owner: Workflow & Automation Lead
- Current stage role: planner
- Next gate: ready
- Founder escalation: not-needed
- Decision status: none
- Review status: pending
- QA status: not-needed
- UAT status: not-needed
- Acceptance status: pending
- Why it matters: If acceptance can proceed while the real framework change set is broader than the selected review slice, harness will approve ambiguous source truth, weaken recovery, and compound false confidence.
- Decision needed: Adopt an explicit review-boundary blocker before any further acceptance of mixed framework slices.
- Deadline: none
- Due review at: none
- Blocked by: WI-0010
- Blocks: WI-0017
- Current blocker: WI-0010 still owns the upstream entropy-compaction lane; WI-0020 now has the acceptance guard implemented and validated, but its framework source slice is not yet clean enough for honest review.
- Next handoff: Resume WI-0020 by carving a reviewable slice around scripts/accept_review_work_item.sh and scripts/run_state_validation_slice.sh, then return to WI-0017 acceptance only after that slice is clean.
- Linked attachments: .harness/tasks/WI-0020/attachments/2026-03-30-should-harness-block-acceptance-when-framework-promotion-boundary-is-unclear-research-memo.md|research-memo|approved;.harness/tasks/WI-0020/attachments/2026-03-30-reviewable-framework-promotion-boundary-external-sensing-research-dispatch.md|research-dispatch|approved;.harness/tasks/WI-0020/attachments/sources/2026-03-30-openai-harness-engineering-on-versioned-plans-and-doc-gardening.md|source-note|approved;.harness/tasks/WI-0020/attachments/sources/2026-03-30-openai-codex-worktrees-skills-and-automations-surfaces.md|source-note|approved;.harness/tasks/WI-0020/attachments/sources/2026-03-30-github-issues-sub-issues-and-dependencies-as-follow-up-carriers.md|source-note|approved;.harness/tasks/WI-0020/attachments/2026-03-30-review-boundary-collapse-process-audit.md|process-audit|approved;.harness/tasks/WI-0020/attachments/2026-03-30-review-boundary-stop-line-checkpoint.md|checkpoint|superseded;.harness/tasks/WI-0020/attachments/2026-03-31-accept-review-entropy-boundary-implementation-checkpoint.md|checkpoint|active
- Interrupt marker: none
- Resume target: none
- Created at: 2026-03-30
- Updated at: 2026-03-31
- Archived at: none

## Summary

- Problem: `work_item_ctl` 会优先把 `WI-0017` 这样的 review item 选出来，但当前 embedded harness source worktree 已经混入多轮未晋升的 framework 改动，导致“被选中的 review item”不再等于“可独立验收的 source slice”。
- Why now: 本轮真实 intake 首先选中了 `WI-0017`，但内部 sensing 同时确认 source validation 仍被 entropy pressure 卡住，且当前 framework diff 横跨 docs / scripts / contracts / skills 多个面，已经不适合继续做假性 acceptance。
- Persistent risk if unfixed: harness 会继续把状态为 `review` 的 task 误当成可验收对象，在 source truth 仍混杂的情况下给出通过信号；这会污染恢复、后续 compounding 和 framework promotion 边界。
- Non-goals: 自动 merge 到 `harness/main`、在一轮里清空所有 pending framework 变更、或引入一套厚重 release-management 流程。

## Recovery
- Current focus: The review-boundary guard is implemented and validated. The remaining gap is not runtime behavior; it is extracting a clean framework source slice so WI-0020 can be reviewed without mixed pending mutations.
- Next command: cd /Users/vx/WebstormProjects/dogfood && git -C ./.agents/skills/harness status --short && git -C ./.agents/skills/harness diff -- scripts/accept_review_work_item.sh scripts/run_state_validation_slice.sh && sed -n '1,240p' .harness/tasks/WI-0020/attachments/2026-03-31-accept-review-entropy-boundary-implementation-checkpoint.md
- Recovery notes: Do not resume WI-0017 acceptance until the guard changes live in a clean reviewable framework slice.
## Workflow Notes

- Seeded by ./.agents/skills/harness/scripts/new_work_item.sh on 2026-03-30.

## Signoff Notes

- Review status starts at pending until the designated reviewer signs off.

## Attachment Notes

- Attach decision, research, review, QA, and output materials under attachments/ as they are created.

## Transition Log

- Created from backlog on 2026-03-30 by ./.agents/skills/harness/scripts/new_work_item.sh.

## Notes

- none
