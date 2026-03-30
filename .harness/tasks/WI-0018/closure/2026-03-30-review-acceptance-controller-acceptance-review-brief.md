# Acceptance Review Brief

- Linked work items: WI-0018



- Date: 2026-03-30
- Host: dogfood consumer runtime repo
- Demo slice under review: replacing manual multi-step review closure with a high-level `accept` control surface that can carry the acceptance brief, approve the bounded review gates, and complete `review -> done`
- What the final reviewer can do right now: inspect `./.agents/skills/harness/scripts/accept_review_work_item.sh`, `./.agents/skills/harness/scripts/work_item_ctl.sh`, and `./.agents/skills/harness/scripts/run_state_validation_slice.sh`, then rerun `./.agents/skills/harness/scripts/run_state_validation_slice.sh` and `./.agents/skills/harness/scripts/audit_state_system.sh --mode core`, and compare the linked checkpoint with the `WI-0018` review handoff
- Acceptance criteria:
  - a reviewer can express bounded review acceptance through one high-level command surface instead of manually sequencing multiple low-level state mutations
  - the controller fails closed when no acceptance review brief is supplied or already approved
  - the bounded happy path links or upgrades the acceptance review brief, approves the necessary review gates, and completes `review -> done`
  - the validation slice proves the high-level `work_item_ctl.sh accept` surface rather than only a lower-level helper script
- Known boundaries:
  - this slice is limited to bounded review closure and does not redesign archive closeout, residual disposition, or acceptance-ledger policy
  - non-`review` terminal completion semantics still come from `complete_work_item.sh`; this task is not redefining every close path
  - the current proof is task-record and shell-surface based; it does not add a new UI layer
- Open risks:
  - broader `close/accept` ergonomics may still deserve a follow-up if more terminal intents keep leaking low-level choreography
  - `complete_work_item.sh` has adjacent JSON/output concerns outside this slice that were intentionally left untouched
- Verification date: 2026-03-30
- Sources reviewed:
  - `./.agents/skills/harness/scripts/accept_review_work_item.sh`
  - `./.agents/skills/harness/scripts/work_item_ctl.sh`
  - `./.agents/skills/harness/scripts/run_state_validation_slice.sh`
  - `./.agents/skills/harness/scripts/complete_work_item.sh`
  - [`/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0018/attachments/2026-03-30-review-acceptance-controller-implementation-checkpoint.md`](/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0018/attachments/2026-03-30-review-acceptance-controller-implementation-checkpoint.md)
  - `./.agents/skills/harness/scripts/run_state_validation_slice.sh`
  - `./.agents/skills/harness/scripts/audit_state_system.sh --mode core`
- What remains unverified:
  - whether the higher-level completion surface should eventually absorb more than bounded review acceptance
  - whether adjacent `complete_work_item.sh` JSON surface cleanup should be folded into a separate follow-up
- Decisions needed from final reviewer:
  - accept this bounded controller slice as sufficient to stop normalizing manual review-accept choreography
  - keep any broader terminal-control-surface cleanup as separate follow-up work instead of silently expanding `WI-0018`

## Thinking Protocol Summary

### Divergent Hypotheses

1. Rework this slice because the controller is not yet a universal close surface for every terminal path.
2. Accept this slice on the narrow claim that bounded `review -> done` closure now has one high-level control surface with fail-closed behavior.
3. Pause the slice until adjacent `complete_work_item.sh` JSON and broader close-surface ergonomics are folded into the same task.

### First Principles Deconstruction

1. The user need here is not "one script to rule every transition," but "stop forcing operators to manually stitch together low-level review-accept mutations."
2. A bounded controller slice should be judged against the stated objective and done criteria, not against every adjacent cleanup opportunity in the closure surface.
3. Replayable evidence matters more than intent language, so the deciding signal is whether the high-level `accept` surface now blocks without a review brief and succeeds with one.

### Convergence To Excellence

Hypothesis 1 over-expands the slice and would delay a clean control-surface win in order to absorb unrelated terminal-surface work. Hypothesis 3 repeats the same mistake in pause form. Hypothesis 2 is the strongest answer because it accepts the slice on its own bounded contract: one high-level review-accept intent, one high-level controller, one replayable blocked path, and one replayable happy path.

### Challenge Vincent

If we insist that this task is not acceptable until every `complete/close/done/archive` path is also redesigned, we would be mixing "bounded review acceptance controller" with "complete lifecycle controller redesign." That sounds thorough, but it is actually scope bleed and would teach the harness to delay obvious high-value control-surface wins.

## Post-Acceptance Compounding Review

- Outcome: follow-up-candidate
- Reason: this slice removes manual review-accept field choreography, but adjacent terminal-surface cleanup and `complete_work_item.sh` JSON/output cleanup still look like separate follow-up lanes rather than reasons to reopen `WI-0018`
- Follow-up posture: keep broader close-surface ergonomics and completion-surface cleanup as explicit candidates if recurrence continues; do not silently re-expand this bounded task
