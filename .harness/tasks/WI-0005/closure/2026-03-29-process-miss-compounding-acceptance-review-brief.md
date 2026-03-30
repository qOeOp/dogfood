# Acceptance Review Brief

- Linked work items: WI-0005



- Date: 2026-03-29
- Host: dogfood consumer runtime repo
- Demo slice under review: immediate compounding trigger for user-reported harness/process/control-surface misses, bound into canonical instructions plus source validation
- What the final reviewer can do right now: inspect the framework diff in `.agents/skills/harness/SKILL.md`, `.agents/skills/harness/docs/workflows/process-compounding-cadence.md`, and `.agents/skills/harness/scripts/validate_source_repo.sh`, then review the incident artifact in `.harness/tasks/WI-0005/attachments/2026-03-29-user-reported-process-miss-process-audit.md` and rerun `./scripts/validate_source_repo.sh`, `./scripts/audit_entropy_budget.sh`, `./.agents/skills/harness/scripts/validate_workspace.sh --mode core`, and `./.agents/skills/harness/scripts/audit_state_system.sh`
- Acceptance criteria:
  - harness canonical instructions explicitly say that a user-reported harness/process miss must become task truth plus process-audit work before symptom-only continuation
  - process compounding cadence explicitly treats user-reported process/control-surface misses as an immediate trigger rather than a weekly-only input
  - source validation fails if either instruction disappears
  - the live incident is preserved as a task-local process-audit artifact
- Known boundaries:
  - this slice strengthens the instruction and validation surface; it does not magically infer every user comment as a process miss without agent judgment
  - the fix does not yet add a separate executable hook for transcript-level detection outside the current harness instruction surface
  - `WI-0004` remains a real follow-up issue, but it is correctly subordinated until this framework-process fix exists
- Open risks:
  - if future users phrase a process miss too ambiguously, the agent could still misclassify it without a stronger typed feedback channel
  - transcript-level automatic detection may still warrant a harder runtime mechanism later if this class of miss recurs
- Verification date: 2026-03-29
- Sources reviewed:
  - live dogfood incident from this thread
  - `WI-0005` process audit artifact
  - current harness source instructions and validator
- What remains unverified:
  - whether a future provider/runtime should expose a structured user-feedback interrupt channel for process misses
  - whether this trigger should also be mirrored into more roles or bundles beyond the root harness skill
- Decisions needed from final reviewer:
  - accept immediate compounding trigger semantics as canonical harness behavior for user-reported process misses
  - defer stronger transcript-level automation until recurrence proves the instruction+validation layer is insufficient

## Thinking Protocol Summary

### Divergent Hypotheses

1. Keep treating user-reported process misses as ordinary chat feedback and rely on agent judgment to remember when to open a follow-up task.
2. Fix only the surfaced issue each time, then trust post-acceptance compounding or weekly audit to catch the process lesson later.
3. Make user-reported harness/process misses an immediate compounding trigger in canonical instructions and bind that rule into source validation.

### First Principles Deconstruction

1. A self-evolving harness cannot require the user to babysit its own compounding trigger.
2. Process misses are durable control-surface facts, not ephemeral tone feedback.
3. If the rule is not in canonical instructions and not enforced by validation, it will regress silently under pressure.
4. The first repair should be small, framework-generic, and reviewable, not a sprawling governance redesign.

### Convergence To Excellence

Hypothesis 1 fails because it leaves the same category of miss discretionary. Hypothesis 2 still lets the framework repair symptoms first and only maybe learn later. Hypothesis 3 is the strongest current fix because it makes the trigger explicit at the root harness surface, upgrades it into validator-backed source truth, and preserves the current incident as a process-audit artifact.

### Challenge Vincent

If someone asks to "just remember next time" without changing canonical instructions or validation, that is not compounding. It is simply asking the operator to be more careful while leaving the framework defect intact.

## Post-Acceptance Compounding Review

- Outcome: no-change
- Reason: this incident exposed a missing trigger rule in existing framework instructions, not a need for a new runtime role or a role-boundary mutation
- Follow-up posture: watch whether the instruction+validation layer is enough; only propose a stronger typed feedback or hook mechanism if this class of miss recurs
