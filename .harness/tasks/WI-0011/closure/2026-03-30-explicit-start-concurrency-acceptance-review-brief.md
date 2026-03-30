# Acceptance Review Brief

- Linked work items: WI-0011


- Date: 2026-03-30
- Host: dogfood consumer runtime repo
- Demo slice under review: repairing the shared `select/open/start` surface so a `review` item remains the top-attention selection while a different ready task can still be started explicitly in a separate worktree-compatible flow
- What the final reviewer can do right now: inspect the framework diff in `.agents/skills/harness/scripts/start_work_item.sh`, `.agents/skills/harness/scripts/work_item_ctl.sh`, `.agents/skills/harness/scripts/run_state_validation_slice.sh`, `.agents/skills/harness/docs/workflows/worktree-parallelism.md`, and `.agents/skills/harness/scripts/validate_source_repo.sh`, then rerun `cd .agents/skills/harness && ./scripts/validate_source_repo.sh && ./scripts/audit_entropy_budget.sh`, `./.agents/skills/harness/scripts/validate_workspace.sh --mode core`, `./.agents/skills/harness/scripts/audit_state_system.sh --mode core`, and the bounded explicit-start regression captured in the targeted validation checkpoint
- Acceptance criteria:
  - shared routing no longer implies a repo-global single-active-task invariant
  - the high-level start surface exposes explicit `--work-item <WI-xxxx>` targeting as the review-time escape hatch
  - explicit targeting still respects task-local blocker, founder escalation, and scope checks rather than bypassing safety boundaries
  - validation covers at least one multi-open scenario where a `review` task remains in place while a different `ready` task is started explicitly
- Known boundaries:
  - this slice preserves the existing shared priority ordering; `start shared` still surfaces the `review` item first by design
  - this slice does not redesign selector ranking, expose multiple alternate start candidates in one response, or change claim/worktree safety rules
  - the broad `run_state_validation_slice.sh` still contains an unrelated Playwright probe that can fail before this concurrency regression runs
- Open risks:
  - if future operators need richer high-level ergonomics, a follow-up may still be worthwhile to surface alternate explicit-start candidates directly in JSON output
  - the source surface remains under soft-threshold entropy pressure, so future iterations should keep this lane compact
- Verification date: 2026-03-30
- Sources reviewed:
  - current source diff for `start_work_item.sh`, `work_item_ctl.sh`, `run_state_validation_slice.sh`, `worktree-parallelism.md`, and `validate_source_repo.sh`
  - [`/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0011/attachments/2026-03-29-shared-selector-concurrency-process-audit.md`](/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0011/attachments/2026-03-29-shared-selector-concurrency-process-audit.md)
  - [`/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0011/attachments/sources/2026-03-29-anthropic-parallel-worktrees-source-note.md`](/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0011/attachments/sources/2026-03-29-anthropic-parallel-worktrees-source-note.md)
  - [`/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0011/attachments/2026-03-29-explicit-start-targeted-validation-checkpoint.md`](/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0011/attachments/2026-03-29-explicit-start-targeted-validation-checkpoint.md)
  - `cd .agents/skills/harness && ./scripts/validate_source_repo.sh`
  - `cd .agents/skills/harness && ./scripts/audit_entropy_budget.sh`
  - `./.agents/skills/harness/scripts/validate_workspace.sh --mode core`
  - `./.agents/skills/harness/scripts/audit_state_system.sh --mode core`
- What remains unverified:
  - the broad `run_state_validation_slice.sh` is still not end-to-end green because the existing Playwright `locked-live-owner` probe fails earlier in the script
  - whether future UX should expose alternate explicit-start candidates more directly than the current bounded targeting surface
- Decisions needed from final reviewer:
  - accept the explicit-target start path plus targeted regression as sufficient for this bounded concurrency slice
  - keep the unrelated Playwright broad-slice failure in a separate follow-up lane instead of treating it as a failure of `WI-0011`

## Thinking Protocol Summary

### Divergent Hypotheses

1. Block acceptance until the entire broad validation slice is green, even though it currently fails on an unrelated Playwright probe before reaching this regression.
2. Accept the concurrency slice solely on narrative reasoning without replayable validation.
3. Accept the slice based on direct evidence for its own done criteria, while keeping the unrelated Playwright failure explicit as a separate residual risk.

### First Principles Deconstruction

1. A task should be accepted against its own stated objective and done criteria, not against every unrelated probe bundled into a larger verifier.
2. If a broad verifier exits before it reaches the target regression, that verifier cannot serve as the deciding gate for this slice.
3. Acceptance still needs replayable evidence, so a bounded targeted regression is stronger than prose-only justification.

### Convergence To Excellence

Hypothesis 1 would keep false coupling in place and continue teaching the wrong control-surface model. Hypothesis 2 would under-verify a real framework change. Hypothesis 3 is the best answer because it uses direct, replayable evidence for the concurrency slice while honestly preserving the unrelated Playwright residual as a separate issue.

### Challenge Vincent

If someone says "don't accept anything until the whole broad slice is green," that sounds safe but is actually sloppy here. It would let an unrelated Playwright probe keep vetoing a concurrency fix that already has targeted evidence and a clear boundary.

## Post-Acceptance Compounding Review

- Outcome: no-change
- Reason: this issue is a bounded selector/start control-surface correction with sufficient existing role ownership; it does not reveal a missing runtime role or a new compounding cadence gap
- Follow-up posture: only open a separate follow-up if the Playwright broad-slice failure needs its own owner or if operators later need richer multi-candidate start ergonomics
