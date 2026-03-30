# Acceptance Review Brief

- Linked work items: WI-0004

- Date: 2026-03-29
- Host: dogfood consumer runtime repo
- Demo slice under review: adding a framework-side preflight/report path for Codex Playwright persistent-profile conflicts by extending `scripts/research/runtime_status.sh` and binding the trigger into the Codex provider delta
- What the final reviewer can do right now: inspect the framework diff in `.agents/skills/harness/scripts/research/runtime_status.sh`, `.agents/skills/harness/docs/workflows/provider-deltas/codex.md`, `.agents/skills/harness/scripts/run_state_validation_slice.sh`, and `.agents/skills/harness/scripts/validate_source_repo.sh`, then rerun `./scripts/validate_source_repo.sh`, `./scripts/audit_entropy_budget.sh`, `./scripts/run_state_validation_slice.sh`, `./.agents/skills/harness/scripts/validate_workspace.sh --mode core`, and `./.agents/skills/harness/scripts/audit_state_system.sh`
- Acceptance criteria:
  - the framework exposes a cheap preflight that reports `playwright_mcp_profile_state` before blind Playwright retries
  - the preflight distinguishes at least `locked-live-owner` and `stale-lock`
  - Codex-specific guidance tells operators to write the conflict back to task truth rather than silently retrying or default-killing the live owner
  - source and runtime validation pass after the new preflight lands
- Known boundaries:
  - this slice does not patch the provider-owned Playwright tool itself
  - this slice does not auto-kill the live owner by default
  - the preflight currently surfaces through `runtime_status.sh`, not an automatic wrapper around every direct tool invocation
- Open risks:
  - direct Playwright tool use can still skip the preflight if the operator ignores the Codex delta
  - a stronger wrapper or tool-level interception may still be worthwhile if this failure mode keeps recurring
- Verification date: 2026-03-29
- Sources reviewed:
  - official Playwright `launch_persistent_context` documentation
  - official Chrome remote debugging security guidance from March 17, 2025
  - task-local reproduction note from this dogfood run
  - current source diff and validation output
- What remains unverified:
  - whether future provider adapter changes alter the default persistent profile path away from `ms-playwright/mcp-chrome`
- Decisions needed from final reviewer:
  - accept preflight/report as the first bounded framework fix for this issue
  - defer any stronger repair automation until recurrence proves the current boundary insufficient

## Thinking Protocol Summary

### Divergent Hypotheses

1. Auto-kill the dedicated `mcp-chrome` owner whenever a conflict is detected.
2. Leave the provider tool unchanged and just document the failure after it happens.
3. Add a cheap framework-side preflight that detects live-owner vs stale-lock states, then route retries through task truth and explicit recovery guidance.

### First Principles Deconstruction

1. The provider-owned Playwright tool is outside harness source truth, so this repo should not pretend it can patch the tool binary itself.
2. Blindly killing an existing browser owner risks destroying an active debugging session that the user did not ask to terminate.
3. A high-leverage first fix is one that turns a silent failure into a detectable runtime condition with durable writeback and clear next action.

### Convergence To Excellence

Hypothesis 1 is too risky for a default. Hypothesis 2 preserves the original broken behavior. Hypothesis 3 is the best answer because it keeps the fix inside harness source, adds a real preflight/report surface, and avoids overreaching into provider-owned process control.

### Challenge Vincent

If someone says "just kill the old browser and move on," that is not a safe default. The framework should first detect and classify the conflict, then let stronger repair automation earn its way in with evidence.

## Post-Acceptance Compounding Review

- Outcome: no-change
- Reason: the issue is a missing adapter-side runtime preflight, not a role-gap or compounding-cadence gap
- Follow-up posture: resume stronger repair exploration only if `locked-live-owner` continues to recur after this preflight/report slice is in use
