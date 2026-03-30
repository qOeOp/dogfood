# Work Item

- Schema version: 2
- State authority: script-only
- State version: 22
- Last operation ID: WI-0001-archive
- Last transition event: .harness/tasks/WI-0001/history/transitions/TX-20260329T201633-WI-0001-done-to-archived.md
- ID: WI-0001
- Title: Dogfood runtime bootstrap gap
- Type: bootstrap
- Status: archived
- Priority: high
- Owner: Workflow & Automation Lead
- Sponsor: general-manager
- Assignee: none
- Worktree: none
- Claimed at: none
- Claim expires at: none
- Lease version: 2
- Objective: Make any canonical task write in a consumer repo lazily materialize the full minimum-core runtime surface so the first write leaves a valid, recoverable .harness/.
- Ready criteria: Reproduce the bootstrap gap, collect external/internal evidence, and choose one framework-generic fix with explicit non-goals.
- Done criteria: A first task mutation in a non-empty consumer repo creates .harness/README.md and .harness/entrypoint.md without damaging user-owned root files, and source/runtime validators pass.
- Required artifacts: source-note,research-memo
- Current stage owner: Workflow & Automation Lead
- Current stage role: archive
- Next gate: none
- Founder escalation: not-needed
- Decision status: approved
- Review status: approved
- QA status: not-needed
- UAT status: not-needed
- Acceptance status: approved
- Why it matters: Without a full bootstrap, the canonical read order breaks on first use and operators need manual repair or source-script knowledge, violating harness entrypoint semantics.
- Decision needed: Adopt lazy in-place minimum-core bootstrap on first state mutation instead of requiring a separate manual bootstrap step.
- Deadline: none
- Due review at: none
- Blocked by: none
- Blocks: none
- Current blocker: none
- Next handoff: none
- Linked attachments: .harness/tasks/WI-0001/attachments/sources/2026-03-29-mcp-roots-boundary-requirements.md|source-note|approved;.harness/tasks/WI-0001/attachments/sources/2026-03-29-anthropic-claude-code-project-bootstrap.md|source-note|approved;.harness/tasks/WI-0001/attachments/sources/2026-03-29-openai-background-mode-handles.md|source-note|approved;.harness/tasks/WI-0001/attachments/2026-03-29-dogfood-runtime-bootstrap-path-research-memo.md|research-memo|approved;.harness/tasks/WI-0001/closure/2026-03-29-runtime-bootstrap-acceptance-review-brief.md|acceptance-review-brief|approved;.harness/tasks/WI-0001/attachments/2026-03-29-bootstrap-acceptance-closeout-checkpoint.md|checkpoint|approved
- Interrupt marker: none
- Resume target: none
- Created at: 2026-03-29
- Updated at: 2026-03-29
- Archived at: 2026-03-29T20:16:33+0800

## Summary

- Problem: the first canonical task write in a non-empty consumer repo materialized `.harness/tasks/` and `.harness/manifest.toml`, but it did not materialize `.harness/README.md` or `.harness/entrypoint.md`, so the runtime failed its own minimum-core contract on first use.
- Why now: this is the first dogfood round in this wrapper repo, so a broken bootstrap blocks the default read order, workspace validation, recovery discipline, and any trustworthy compounding loop before they even start.
- Persistent risk if unfixed: operators must know hidden source-script behavior or hand-repair `.harness/`, which violates `/harness` as the entrypoint and turns bootstrap friction into recurring entropy.
- Non-goals: redesign shared writeback, broaden work-item type taxonomy, or change task-local artifact routing beyond the minimum-core bootstrap gap.

## Recovery
- Current focus: Closed after accepted minimum-core bootstrap fix.
- Next command: none
- Recovery notes: If reopened for runtime doc drift, start from the acceptance brief in closure/ and rerun validate_source_repo.sh, run_state_validation_slice.sh, and validate_workspace.sh --mode core before proposing broader refactoring.
## Workflow Notes

- Seeded by ./scripts/new_work_item.sh on 2026-03-29.
- Reproduced in this consumer repo by running `STATE_ACTOR=codex ./.agents/skills/harness/scripts/new_work_item.sh bootstrap "Dogfood runtime bootstrap gap" ...` and then `./.agents/skills/harness/scripts/validate_workspace.sh --mode core`.
- Chosen fix boundary: framework-generic only, inside `./.agents/skills/harness/`, with no dogfood-specific wrapper surface added at repo root.

## Signoff Notes

- Review status starts at pending until the designated reviewer signs off.

## Attachment Notes

- Attach decision, research, review, QA, and output materials under attachments/ as they are created.
- Official evidence and synthesis live in task-local source notes plus the research memo linked from the header.

## Transition Log

- Created from backlog on 2026-03-29 by ./scripts/new_work_item.sh.

## Notes

- Compounding effectiveness review found no prior accepted task, checkpoint, process-audit, or role-change artifact in this consumer runtime because `.harness/` had never been materialized here before this round.
- That means there is no trend data proving compounding reduced recurrence in this repo; the absence of that observation surface is noted, but this round stays scoped to the bootstrap gap rather than expanding into a second initiative.
