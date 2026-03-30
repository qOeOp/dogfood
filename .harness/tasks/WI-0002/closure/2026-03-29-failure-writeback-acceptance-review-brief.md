# Acceptance Review Brief

- Linked work items: WI-0002



- Date: 2026-03-29
- Host: dogfood consumer runtime repo
- Demo slice under review: task-scoped failure checkpoint plus recovery writeback when `research_ctl.sh --work-item` fails during evidence collection
- What the final reviewer can do right now: inspect the framework diff in `.agents/skills/harness/scripts/record_tool_failure.sh`, `.agents/skills/harness/scripts/research_ctl.sh`, and `.agents/skills/harness/scripts/run_state_validation_slice.sh`, then rerun `./scripts/validate_source_repo.sh`, `./scripts/run_state_validation_slice.sh`, `./scripts/audit_entropy_budget.sh`, `./.agents/skills/harness/scripts/validate_workspace.sh --mode core`, and `./.agents/skills/harness/scripts/audit_state_system.sh`
- Acceptance criteria:
  - a task-scoped `research_ctl.sh` failure automatically writes a task-local checkpoint instead of disappearing into chat
  - `## Recovery` is refreshed to the failed invocation boundary with a concrete next command
  - source/runtime validation covers the missing-local-evidence regression
  - the fix stays framework-generic and does not add new wrapper-owned top-level surface
- Known boundaries:
  - this slice does not repair the Playwright browser-profile conflict itself
  - the control only applies when collection is routed through `research_ctl.sh` with explicit `--work-item`
  - other tool surfaces may still need their own task-scoped failure writeback if future dogfood runs expose similar gaps
- Open risks:
  - Playwright MCP browser runs can still fail earlier because the shared persistent Chrome profile is locked by live browser sessions
  - tool failures without explicit task context still cannot be promoted into task truth automatically
- Verification date: 2026-03-29
- Sources reviewed:
  - internal repro in this dogfood runtime
  - source validators and runtime validators in this repo
  - `WI-0002` process audit and task-local failure checkpoint artifacts
- What remains unverified:
  - a dedicated Playwright profile preflight or repair path
  - whether the same failure-writeback contract should be generalized beyond `research_ctl.sh`
- Decisions needed from final reviewer:
  - accept task-scoped failure writeback in `research_ctl.sh` as the first lifecycle-coverage hardening slice
  - keep Playwright profile preflight as the next bounded follow-up instead of coupling it into this round

## Thinking Protocol Summary

### Divergent Hypotheses

1. Repair only the Playwright blank-tab symptom and leave generic failure handling unchanged.
2. Record the incident in process artifacts but keep tool-failure writeback optional.
3. Make task-scoped evidence-collection failures durable by default in `research_ctl.sh`, then treat Playwright-specific preflight as a later slice.

### First Principles Deconstruction

1. If a tool fails with explicit task context, the failure must become task truth rather than remaining a chat-side anecdote.
2. A single task does not need to traverse every lifecycle state, but skipped failures must not be invisible by default.
3. The first repair should stay bounded, framework-generic, and layered inside harness source rather than expanding wrapper-specific surface.
4. A claimed control-surface fix is only real if both source-level and consumer-runtime validation pass.

### Convergence To Excellence

Hypothesis 1 is too narrow because it treats one browser failure mode while leaving the broader "tool failure can disappear" defect untouched. Hypothesis 2 improves narration but not control. Hypothesis 3 is the best first move because it closes the generic writeback gap at an existing integration point, produces durable recovery state, and is backed by a regression that exercises the exact failure path.

### Challenge Vincent

If someone asks to jump straight into Playwright-specific repair while leaving generic failure writeback optional, that is a short-term symptom patch, not the highest-leverage control fix. The stronger order is to make failure disappearance impossible at one bounded task-scoped surface first, then handle browser-profile preflight as the next issue.

## Post-Acceptance Compounding Review

- Outcome: no-change
- Reason: the new evidence shows a control-surface gap rather than a missing runtime role boundary, and there is still not enough repeated trend data to justify a role mutation from this slice alone
- Follow-up posture: keep the residual Playwright profile-conflict issue visible as the next candidate work item, but do not expand this accepted slice into a broader lifecycle redesign
