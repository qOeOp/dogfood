# Acceptance Review Brief

- Linked work items: WI-0003



- Date: 2026-03-29
- Host: dogfood consumer runtime repo
- Demo slice under review: version-aware latest transition resolution for same-second work-item events, plus a deterministic validation slice for the archive-ordering collision
- What the final reviewer can do right now: inspect the framework diff in `.agents/skills/harness/scripts/lib_state.sh`, `.agents/skills/harness/scripts/rehash_state_events.sh`, and `.agents/skills/harness/scripts/run_state_validation_slice.sh`, then rerun `./scripts/validate_source_repo.sh`, `./scripts/run_state_validation_slice.sh`, `./scripts/audit_entropy_budget.sh`, `./.agents/skills/harness/scripts/validate_workspace.sh --mode core`, and `./.agents/skills/harness/scripts/audit_state_system.sh`
- Acceptance criteria:
  - `latest_transition_event_path()` returns the semantically latest event even when two transition files share the same second
  - the existing archived `WI-0002` state passes runtime audit without manual repair of task history
  - validation now includes a deterministic same-second collision regression rather than relying on wall-clock luck
  - the fix does not depend on sleeps, timestamp padding, or rewriting historical transition filenames
- Known boundaries:
  - this slice does not change existing transition filenames or event payload shape
  - the fix is scoped to work-item latest-event resolution and the transition-order helper reused by rehashing
  - this slice still does not address the Playwright browser-profile conflict itself
- Open risks:
  - if future callers need a globally ordered cross-task transition listing, `list_transition_events()` may need a similar semantic-order helper instead of basename sort
  - same-second ordering still assumes `Version after` remains a valid monotonic contract on work-item transition events
- Verification date: 2026-03-29
- Sources reviewed:
  - internal runtime repro from `WI-0002`
  - current framework source and validation scripts in this repo
  - consumer-runtime validators against the live dogfood `.harness/`
- What remains unverified:
  - whether any future cross-task transition consumers should adopt the same semantic ordering helper
  - whether a broader transition-history API cleanup is warranted beyond the currently used work-item latest-event path
- Decisions needed from final reviewer:
  - accept version-aware latest-event resolution as the canonical fix for same-second transition collisions
  - defer broader transition-history API cleanup unless another real caller proves it is needed

## Thinking Protocol Summary

### Divergent Hypotheses

1. Avoid the bug operationally by inserting sleeps or forcing wall-clock separation between closeout events.
2. Change filename generation so later events always sort later lexicographically, then rely on basename order.
3. Resolve the latest event from transition metadata (`Version after`) and back it with a deterministic same-second regression.

### First Principles Deconstruction

1. "Latest transition event" is a semantic fact about state progression, not a filename coincidence.
2. The fix must work for already-written history, not only for future files created under stricter timing.
3. Validation should reproduce the collision deterministically instead of hoping two events happen in the same second.
4. The repair should stay framework-generic and avoid mutating consumer task history just to placate the reader.

### Convergence To Excellence

Hypothesis 1 is brittle because it depends on wall-clock timing and still leaves existing histories ambiguous. Hypothesis 2 improves future filenames but does not repair already-materialized histories unless the whole event path contract changes. Hypothesis 3 is the best choice because it redefines "latest" in semantic terms, immediately fixes the live runtime audit failure, and is covered by a deterministic regression that does not rely on timing luck.

### Challenge Vincent

If someone proposes `sleep 1` or a timestamp workaround as "good enough," that is the wrong optimization. It hides the ordering defect instead of fixing the reader contract, and it does nothing for already-written task histories like `WI-0002`.

## Post-Acceptance Compounding Review

- Outcome: no-change
- Reason: the failure came from a framework transition-order contract, not from an unclear runtime role boundary or handoff owner gap
- Follow-up posture: only open a broader transition-history API cleanup if a real caller needs semantic ordering outside the work-item latest-event path
