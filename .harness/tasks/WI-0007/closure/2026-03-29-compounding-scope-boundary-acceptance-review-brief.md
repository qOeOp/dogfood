# Acceptance Review Brief

- Linked work items: WI-0007



- Date: 2026-03-29
- Host: dogfood consumer runtime repo
- Demo slice under review: narrowing the new process-miss compounding trigger so it applies only to harness/framework/runtime/control-surface defects rather than ordinary project-domain feedback
- What the final reviewer can do right now: inspect the framework diff in `.agents/skills/harness/SKILL.md`, `.agents/skills/harness/docs/workflows/process-compounding-cadence.md`, and `.agents/skills/harness/scripts/validate_source_repo.sh`, then rerun `./scripts/validate_source_repo.sh`, `./scripts/audit_entropy_budget.sh`, `./.agents/skills/harness/scripts/validate_workspace.sh --mode core`, and `./.agents/skills/harness/scripts/audit_state_system.sh`
- Acceptance criteria:
  - canonical instructions now scope the trigger to harness/framework/runtime/control-surface misses
  - project-domain workflow feedback is explicitly left with the active repo/task instead of being absorbed into harness self-evolution by default
  - source validation checks the narrowed wording rather than the previously over-broad rule
  - live runtime state remains valid after the boundary correction
- Known boundaries:
  - this slice narrows wording and validation, not a transcript-level classifier
  - ambiguous user feedback can still require judgment; the fix is about default boundary, not total automation
  - `WI-0004` remains the active next issue once this boundary correction is archived
- Open risks:
  - future stronger automation may still need a typed feedback/interrupt surface if boundary ambiguity recurs
  - the source surface is now saturated, so future fixes must stay especially compact
- Verification date: 2026-03-29
- Sources reviewed:
  - live user feedback from this dogfood thread
  - current harness source diff and validators
  - `WI-0007` task truth
- What remains unverified:
  - whether transcript-level typed feedback would further reduce ambiguity beyond the current instruction boundary
- Decisions needed from final reviewer:
  - accept the narrowed boundary as the correct default semantics
  - defer any stronger automation until recurrence proves the wording+validation layer insufficient

## Thinking Protocol Summary

### Divergent Hypotheses

1. Keep the broader wording and rely on operator judgment not to over-trigger harness self-evolution.
2. Remove the new trigger entirely to avoid side effects.
3. Keep the trigger, but explicitly scope it to harness/framework/runtime/control-surface defects and bind that boundary into validation.

### First Principles Deconstruction

1. Harness should evolve itself only when the defect is in harness, not when the user is simply refining project-domain process.
2. Deleting the trigger would recreate the original failure mode where the user must demand compounding manually.
3. A safe fix must preserve the compounding trigger while preventing framework overreach into user project workflow.

### Convergence To Excellence

Hypothesis 1 leaves an over-broad default in place. Hypothesis 2 throws away the real improvement. Hypothesis 3 is the best answer because it preserves the compounding trigger, restores framework-vs-project layering, and makes the narrowed boundary part of validator-backed source truth.

### Challenge Vincent

If someone says "the operator will just know when to ignore the broader rule," that is not a reliable framework boundary. The right fix is to encode the scope explicitly where the framework reads and validates it.

## Post-Acceptance Compounding Review

- Outcome: no-change
- Reason: the issue was an over-broad wording boundary in existing framework instructions, not a missing runtime role
- Follow-up posture: continue `WI-0004` under the narrowed rule and only escalate further if transcript-level ambiguity becomes a repeated failure mode
