# Work Item

- Schema version: 2
- State authority: script-only
- State version: 22
- Last operation ID: OP-20260330T222719-66506-WI-0017-update-fields
- Last transition event: .harness/tasks/WI-0017/history/transitions/TX-20260330T222719-WI-0017-paused-to-paused.md
- ID: WI-0017
- Title: Task issue ledger and residual disposition controller
- Type: control
- Status: paused
- Priority: critical
- Owner: Workflow & Automation Lead
- Sponsor: general-manager
- Assignee: none
- Worktree: none
- Claimed at: none
- Claim expires at: none
- Lease version: 3
- Objective: Introduce a thin task-local issue ledger plus residual-disposition control so execution problems, user criticism, and review leftovers become structured task issues instead of prose-only artifacts.
- Ready criteria: Keep the first slice thin: define a minimal issue schema and one task-local storage carrier, route one tool-failure path plus one user-criticism path into it, and specify how archive will consume issue disposition without redesigning every artifact.
- Done criteria: Execution problems and user-reported harness misses can both produce task-linked issue entries with evidence refs and explicit disposition; the closeout path fails closed when open issues lack disposition or linked follow-up; and validation covers one resolved-in-place path plus one promoted-to-followup-WI path.
- Required artifacts: none
- Current stage owner: Workflow & Automation Lead
- Current stage role: paused
- Next gate: resume
- Founder escalation: not-needed
- Decision status: none
- Review status: pending
- QA status: not-needed
- UAT status: not-needed
- Acceptance status: pending
- Why it matters: If harness keeps scattering residuals across checkpoints, audits, and review notes without a unified issue object, future compounding will devolve into prose archaeology and unresolved execution debt.
- Decision needed: Adopt a thin task-local issue ledger plus residual-disposition gate before adding more compounding rituals or memory surfaces.
- Deadline: none
- Due review at: none
- Blocked by: WI-0020
- Blocks: none
- Current blocker: acceptance blocked until WI-0020 restores a reviewable framework source boundary
- Next handoff: resume WI-0017 acceptance after WI-0020
- Linked attachments: .harness/tasks/WI-0017/attachments/2026-03-30-task-local-issue-ledger-and-residual-disposition-controller-external-sensing-research-dispatch.md|research-dispatch|approved;.harness/tasks/WI-0017/attachments/sources/2026-03-30-github-issues-dependencies-and-work-hierarchy.md|source-note|approved;.harness/tasks/WI-0017/attachments/2026-03-30-should-harness-add-a-task-local-issue-ledger-and-residual-disposition-gate-research-memo.md|research-memo|approved;.harness/tasks/WI-0017/attachments/sources/2026-03-30-openai-harness-engineering-agent-first-repository-knowledge-and-feedback-loops.md|source-note|approved;.harness/tasks/WI-0017/attachments/sources/2026-03-30-jira-work-item-model-as-issue-carrier.md|source-note|approved;.harness/tasks/WI-0017/attachments/2026-03-30-task-local-issue-ledger-runtime-slice-validated-checkpoint.md|checkpoint|draft
- Interrupt marker: risk-review-required
- Resume target: review
- Created at: 2026-03-30
- Updated at: 2026-03-30
- Archived at: none

## Summary

- Problem: execution problems, user criticism, review residuals, and closeout leftovers can already leave durable traces, but they still live across checkpoints, process-audits, recovery notes, and review prose instead of converging into one task-local issue object with explicit disposition.
- Why now: `WI-0014` and `WI-0015` separately target archive-time disposition and criticism writeback, but neither slice by itself gives the runtime a unified substrate for issue capture, follow-up promotion, or residual closure.
- Persistent risk if unfixed: harness will keep accumulating more task artifacts while still forcing future compounding work to reconstruct what happened, what remains open, and what was intentionally deferred from scattered prose.
- Non-goals: build a heavyweight incident-management system, infer every issue from free-form transcripts, or replace checkpoints, process-audits, and acceptance artifacts with a brand-new bureaucracy.

## Recovery
- Current focus: Paused because acceptance would be dishonest until WI-0020 re-establishes a reviewable framework source boundary.
- Next command: cd /Users/vx/WebstormProjects/dogfood && sed -n "1,220p" .harness/tasks/WI-0020/task.md && STATE_ACTOR=codex ./.agents/skills/harness/scripts/work_item_ctl.sh resume --expected-version 22 WI-0017
- Recovery notes: Treat the current pause as a review-boundary safety stop, not as evidence that the issue-ledger slice regressed.
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
