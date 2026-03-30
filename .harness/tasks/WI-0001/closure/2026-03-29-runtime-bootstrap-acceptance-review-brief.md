# Acceptance Review Brief

- Linked work items: WI-0001


- Date: 2026-03-29
- Host: dogfood consumer runtime repo
- Demo slice under review: lazy minimum-core bootstrap on the first canonical task write inside a non-empty consumer repo
- What the final reviewer can do right now: inspect the framework diff in `.agents/skills/harness/scripts/lib_state.sh` and `.agents/skills/harness/scripts/run_state_validation_slice.sh`, then rerun `./scripts/validate_source_repo.sh`, `./scripts/run_state_validation_slice.sh`, and `./.agents/skills/harness/scripts/validate_workspace.sh --mode core`
- Acceptance criteria:
  - the first canonical task write creates `.harness/README.md` and `.harness/entrypoint.md`
  - user-owned root files such as `README.md` remain untouched
  - the runtime still validates as minimum-core after bootstrap
  - the fix stays inside the framework source boundary and does not add wrapper-owned top-level surface
- Known boundaries:
  - the change is scoped to minimum-core bootstrap only
  - shared writeback, provider adapters, and task taxonomy are unchanged
  - runtime doc text now exists in both `materialize_runtime_fixture.sh` and `lib_state.sh`
- Open risks:
  - duplicated runtime doc text can drift over time
  - future non-core runtime modes may need a stronger sync story than create-if-missing
- Verification date: 2026-03-29
- Sources reviewed:
  - internal repro and validators in this repo
  - MCP Roots spec
  - Anthropic Claude Code memory/bootstrap docs
  - OpenAI background mode guide
- What remains unverified:
  - whether runtime bootstrap prose should be centralized into a single generator or template
- Decisions needed from final reviewer:
  - accept the lazy create-if-missing bootstrap fix for the broken first-write path
  - defer prose deduplication unless drift becomes a real recurring failure

## Thinking Protocol Summary

### Divergent Hypotheses

1. Keep bootstrap as a separate manual or script-explicit step and document the workaround.
2. Create missing minimum-core runtime docs lazily inside `ensure_core_runtime_dirs()` and guard it with an in-place regression.
3. Refuse acceptance until runtime doc generation is fully centralized behind one template or generator.

### First Principles Deconstruction

1. The first task mutation must leave the canonical read order valid immediately.
2. The operator should not need hidden script knowledge or manual repair to recover state.
3. Automatic bootstrap must stay inside `.harness/` and must not overwrite consumer-owned root files.
4. A fix is only real if source-level and consumer-runtime validation both pass after the change.

### Convergence To Excellence

Hypothesis 1 fails first principles because it preserves the hidden manual bootstrap gap. Hypothesis 3 is directionally cleaner, but it expands scope before repairing the broken contract and would turn one high-leverage repair into two coupled changes. Hypothesis 2 is the best current choice because it restores the contract at the first write boundary, preserves layering, and is covered by a regression that exercises the exact failure mode in a non-empty consumer repo.

### Challenge Vincent

If someone asks to fold text deduplication or broader runtime redesign into this same round, that is the wrong optimization. The highest-leverage defect here is the broken first-write contract, not the existence of a smaller follow-on cleanup opportunity.

## Post-Acceptance Compounding Review

- Outcome: no-change
- Reason: this repo has no earlier accepted task, process-audit, or role-change history, so there is not enough trend data to justify a runtime role mutation from this single bootstrap repair
- Follow-up posture: keep the doc-drift risk visible as a residual, and only promote it into a new work item if it causes real recurrence or validation churn
