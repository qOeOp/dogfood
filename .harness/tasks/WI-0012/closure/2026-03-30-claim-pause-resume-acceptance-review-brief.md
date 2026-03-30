# Acceptance Review Brief

- Linked work items: WI-0012



- Date: 2026-03-30
- Host: dogfood consumer runtime repo
- Demo slice under review: exposing active-task claim metadata on the high-level `start/open` control surfaces and proving a live `pause -> resume` path in task truth
- What the final reviewer can do right now: inspect `.agents/skills/harness/scripts/lib_state.sh`, `.agents/skills/harness/scripts/open_work_item.sh`, `.agents/skills/harness/scripts/start_work_item.sh`, and `.agents/skills/harness/scripts/run_state_validation_slice.sh`, then rerun `./.agents/skills/harness/scripts/run_state_validation_slice.sh`, `./.agents/skills/harness/scripts/validate_workspace.sh --mode core`, and `./.agents/skills/harness/scripts/audit_state_system.sh --mode core`, and review the linked checkpoint plus the WI-0012 transition sequence from `ready` through `paused` and back into `review`
- Acceptance criteria:
  - active-task claim metadata is exposed on the high-level JSON control surface instead of remaining visible only in raw task headers
  - pause writes interrupt and resume metadata, and resume clears them back to `none`
  - the bounded validation slice fails if `start_work_item.sh` or `open_work_item.sh` stops exposing claim metadata for active tasks
  - task truth contains a real dogfood `ready -> in-progress -> paused -> in-progress -> review` lineage for this slice
- Known boundaries:
  - once `WI-0012` enters `review`, its own claim fields are expected to clear; the claim proof is about active-task behavior, not review-state retention
  - `open_work_item.sh --json shared` still follows shared priority ordering, so claim visibility is most direct through targeted validation or explicit targeting rather than generic shared selection
  - this slice does not redesign selector ergonomics, acceptance-ledger handling, or broader async orchestration
- Open risks:
  - richer shared-scope ergonomics may still warrant a later follow-up if operators keep wanting alternate active candidates surfaced directly
  - source-repo-wide audits were not used as the deciding gate for this bounded consumer-runtime slice
- Verification date: 2026-03-30
- Sources reviewed:
  - `.agents/skills/harness/scripts/lib_state.sh`
  - `.agents/skills/harness/scripts/open_work_item.sh`
  - `.agents/skills/harness/scripts/start_work_item.sh`
  - `.agents/skills/harness/scripts/run_state_validation_slice.sh`
  - [`/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0012/attachments/2026-03-30-claim-pause-resume-visible-checkpoint.md`](/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0012/attachments/2026-03-30-claim-pause-resume-visible-checkpoint.md)
  - [`/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0012/history/transitions/TX-20260330T113812-WI-0012-ready-to-in-progress.md`](/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0012/history/transitions/TX-20260330T113812-WI-0012-ready-to-in-progress.md)
  - [`/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0012/history/transitions/TX-20260330T114633-WI-0012-in-progress-to-paused.md`](/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0012/history/transitions/TX-20260330T114633-WI-0012-in-progress-to-paused.md)
  - [`/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0012/history/transitions/TX-20260330T114633-WI-0012-paused-to-in-progress.md`](/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0012/history/transitions/TX-20260330T114633-WI-0012-paused-to-in-progress.md)
  - [`/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0012/history/transitions/TX-20260330T114949-WI-0012-in-progress-to-review.md`](/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0012/history/transitions/TX-20260330T114949-WI-0012-in-progress-to-review.md)
  - `./.agents/skills/harness/scripts/run_state_validation_slice.sh`
  - `./.agents/skills/harness/scripts/validate_workspace.sh --mode core`
  - `./.agents/skills/harness/scripts/audit_state_system.sh --mode core`
- What remains unverified:
  - whether the source repo as a whole passes every broader source audit unrelated to this bounded consumer-runtime slice
  - whether future operator UX should expose alternate active candidates more directly than the current shared-priority surface does
- Decisions needed from final reviewer:
  - accept the bounded claim-visibility plus pause/resume proof slice as sufficient for `WI-0012`
  - keep shared-selector ergonomics, if needed, as a separate follow-up lane instead of silently expanding this task

## Thinking Protocol Summary

### Divergent Hypotheses

1. Keep `WI-0012` in `review` until the shared `open` surface also exposes richer alternate-candidate ergonomics and all broader source audits are rerun.
2. Accept `WI-0012` mainly on checkpoint prose and prior manual inspection without replaying the bounded validation or runtime audits.
3. Accept `WI-0012` on direct bounded evidence for its own done criteria, while keeping shared-selector ergonomics and broader repo audits explicit as separate residuals.

### First Principles Deconstruction

1. A bounded slice should be accepted against its own stated objective and done criteria, not against every adjacent ergonomics improvement that could someday exist.
2. Claim visibility for active tasks and live pause/resume semantics are the kernel behaviors under review here; shared selector UX is adjacent but not identical.
3. Acceptance still needs replayable evidence, so a green task-specific validation slice plus runtime audits and live transition lineage are stronger than narrative agreement alone.

### Convergence To Excellence

Hypothesis 1 would expand the slice and falsely couple claim-kernel proof to a broader selector-UX redesign. Hypothesis 2 would under-verify a real runtime control-surface change. Hypothesis 3 is the strongest answer because it accepts the slice on replayable evidence for its own contract while honestly preserving the remaining ergonomics question as a separate residual.

### Challenge Vincent

If someone says "don't accept this until the generic shared `open` surface always shows the claim-bearing task first," that sounds strict but is actually mixing two different problems. `WI-0012` is about active-task claim visibility and pause/resume proof, not a wholesale redesign of shared priority ordering.

## Post-Acceptance Compounding Review

- Outcome: follow-up-candidate
- Reason: the slice appears sufficient on its own terms, but the remaining shared-selector ergonomics question may deserve a later bounded follow-up if operator demand keeps recurring
- Follow-up posture: keep this residual as a small candidate rather than re-expanding `WI-0012`; only promote it if recurrence proves that explicit targeting plus validation is not enough
