# Work Item

- Schema version: 2
- State authority: script-only
- State version: 13
- Last operation ID: OP-20260330T185144-18023-WI-0017-paused-to-in-progress
- Last transition event: .harness/tasks/WI-0017/history/transitions/TX-20260330T185144-WI-0017-paused-to-in-progress.md
- ID: WI-0017
- Title: Task issue ledger and residual disposition controller
- Type: control
- Status: in-progress
- Priority: critical
- Owner: Workflow & Automation Lead
- Sponsor: general-manager
- Assignee: codex
- Worktree: /Users/vx/WebstormProjects/dogfood
- Claimed at: 2026-03-30T18:51:44+0800
- Claim expires at: 2026-03-30T22:51:44+0800
- Lease version: 2
- Objective: Introduce a thin task-local issue ledger plus residual-disposition control so execution problems, user criticism, and review leftovers become structured task issues instead of prose-only artifacts.
- Ready criteria: Keep the first slice thin: define a minimal issue schema and one task-local storage carrier, route one tool-failure path plus one user-criticism path into it, and specify how archive will consume issue disposition without redesigning every artifact.
- Done criteria: Execution problems and user-reported harness misses can both produce task-linked issue entries with evidence refs and explicit disposition; the closeout path fails closed when open issues lack disposition or linked follow-up; and validation covers one resolved-in-place path plus one promoted-to-followup-WI path.
- Required artifacts: none
- Current stage owner: codex
- Current stage role: executor
- Next gate: review
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
- Blocked by: none
- Blocks: none
- Current blocker: none
- Next handoff: none
- Linked attachments: .harness/tasks/WI-0017/attachments/2026-03-30-task-local-issue-ledger-and-residual-disposition-controller-external-sensing-research-dispatch.md|research-dispatch|draft;.harness/tasks/WI-0017/attachments/sources/2026-03-30-github-issues-dependencies-and-work-hierarchy.md|source-note|draft;.harness/tasks/WI-0017/attachments/2026-03-30-should-harness-add-a-task-local-issue-ledger-and-residual-disposition-gate-research-memo.md|research-memo|draft
- Interrupt marker: none
- Resume target: none
- Created at: 2026-03-30
- Updated at: 2026-03-30
- Archived at: none

## Summary

- Problem: execution problems, user criticism, review residuals, and closeout leftovers can already leave durable traces, but they still live across checkpoints, process-audits, recovery notes, and review prose instead of converging into one task-local issue object with explicit disposition.
- Why now: `WI-0014` and `WI-0015` separately target archive-time disposition and criticism writeback, but neither slice by itself gives the runtime a unified substrate for issue capture, follow-up promotion, or residual closure.
- Persistent risk if unfixed: harness will keep accumulating more task artifacts while still forcing future compounding work to reconstruct what happened, what remains open, and what was intentionally deferred from scattered prose.
- Non-goals: build a heavyweight incident-management system, infer every issue from free-form transcripts, or replace checkpoints, process-audits, and acceptance artifacts with a brand-new bureaucracy.

## Recovery
- Current focus: Resume issue-ledger design now that WI-0019 closed the mutation-lock integrity blocker.
- Next command: STATE_ACTOR=codex ./.agents/skills/harness/scripts/work_item_ctl.sh resume --expected-version 12 WI-0017
- Recovery notes: Carry forward the existing WI-0017 research artifacts and start with task-local issue carrier selection plus archive-facing residual disposition; no need to re-open the lock investigation unless task-truth corruption recurs.
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
