# Acceptance Review Brief

- Linked work items: WI-0008

- Date: 2026-03-29
- Host: dogfood consumer runtime repo
- Demo slice under review: correcting compounding semantics so the framework compounds the current work object, with dogfood harness-iteration rounds targeting harness only because harness is the active thing being improved in this repo right now
- What the final reviewer can do right now: inspect the framework diff in `.agents/skills/harness/SKILL.md`, `.agents/skills/harness/docs/workflows/process-compounding-cadence.md`, and `.agents/skills/harness/scripts/validate_source_repo.sh`, then rerun `./scripts/validate_source_repo.sh`, `./scripts/audit_entropy_budget.sh`, `./.agents/skills/harness/scripts/validate_workspace.sh --mode core`, and `./.agents/skills/harness/scripts/audit_state_system.sh`
- Acceptance criteria:
  - canonical instructions say compounding follows the current work object rather than repo type alone
  - dogfood harness-evolution rounds explicitly target harness because harness is the active work object in this repo
  - non-harness work stays with the active repo/task instead of being silently absorbed into harness self-evolution
  - source validation checks the work-object-relative wording and the runtime remains valid after the correction
- Known boundaries:
  - this slice corrects semantics and validation, not transcript-level automatic classification of every user complaint
  - ambiguous conversations can still require judgment if the active work object is genuinely unclear
  - `WI-0004` remains the next bounded implementation issue once this semantics fix is archived
- Open risks:
  - a future typed feedback surface may still be useful if scope ambiguity recurs
  - source entropy is saturated, so further framework edits must stay line-neutral or compaction-first
- Verification date: 2026-03-29
- Sources reviewed:
  - live user clarification in this dogfood thread
  - `WI-0008` task truth
  - updated framework source diff and validation results
  - `WI-0008` process audit attachment
- What remains unverified:
  - whether stronger typed routing would reduce ambiguity further than the new wording-backed default
- Decisions needed from final reviewer:
  - accept work-object-relative compounding as the stable default semantics
  - defer any stronger transcript classifier until recurrence proves the wording+validator layer insufficient

## Thinking Protocol Summary

### Divergent Hypotheses

1. Keep the narrowed harness-only rule and rely on humans to reinterpret it when the active work object is a user project.
2. Revert to the broader repo-agnostic trigger and accept that harness may sometimes absorb unrelated project feedback.
3. Make compounding explicitly follow the current work object, then state that dogfood harness-iteration rounds target harness only because harness is the active object in this repo right now.

### First Principles Deconstruction

1. Compounding should improve the thing currently being evolved, not whichever layer has the loudest identity label.
2. User-project workflow feedback should stay with the user project unless the defect is actually in harness/control-surface behavior.
3. Dogfood is special only because the active work object for this round is harness itself; that is a runtime fact, not a universal rule.

### Convergence To Excellence

Hypothesis 1 keeps the wrong default and depends on operator rescue. Hypothesis 2 recreates the over-broad failure mode. Hypothesis 3 is the best answer because it preserves immediate compounding, restores correct target selection, and binds the semantics into validator-backed source truth.

### Challenge Vincent

If anyone says "just remember that dogfood means harness," that is still too lossy. The durable rule must be "follow the current work object," with dogfood harness-evolution called out only as this round's concrete instantiation.

## Post-Acceptance Compounding Review

- Outcome: no-change
- Reason: this slice repairs the compounding target rule itself rather than revealing a new downstream role or audit surface
- Follow-up posture: resume `WI-0004` after archive and only open a stronger typed-routing task if ambiguity recurs in later runs
