# Process Audit

- Linked work items: WI-0010



- Date: 2026-03-31
- Owner: Workflow & Automation Lead
- Scope: why `WI-0010` should stop expanding adjacent support slices until the entropy lane shows visible improvement
- Signals reviewed:
  - current source audit output: `growth state: breached`, `control state: compaction-only`, `pending-active-files: 49`, `new-active-files: 9`, and `scripts/validate_source_repo.sh` as the recent hotspot with `16` touches
  - current embedded harness source diff stat: `41 files changed, 4516 insertions(+), 1149 deletions(-)`
  - earlier `WI-0010` checkpoints showing pressure worsened from `pending-active-files=28` / `new-active-files=3` on 2026-03-30 to `pending-active-files=47` / `new-active-files=9` earlier on 2026-03-31
  - accepted or completed support slices under `WI-0018` and `WI-0019`, whose own review artifacts still called out unrelated entropy blockers and broader repo noise
- Repeated frictions:
  - support slices can improve correctness while still leaving the parent entropy task less reviewable than before
  - the source worktree keeps getting more mixed, so each new adjacent controller edit makes the next honest review boundary harder to carve
  - `WI-0020` remains blocked not because there is no acceptance guard, but because `WI-0010` has not yet restored a clean enough source slice
- Cross-task handoff failures:
  - `WI-0010` accepted real support progress without demanding visible pressure reduction, so downstream tasks inherited a still-breached source surface
  - `WI-0020` now has the correct stop-the-line semantics, but the parent compaction lane did not hand it a reviewable slice to resume from
  - `WI-0017` is still paused behind the same mixed source boundary, proving the compounding loop did not actually shrink recurrence yet
- Candidate root causes:
  - `WI-0010` lacked an effectiveness gate that says "no more adjacent support expansion until the dominant pressure metric falls or the budget is explicitly raised"
  - slice selection drifted toward nearby validated controllers instead of the dominant hotspot with the highest repeated touch pressure
  - recent wins improved substrate truthfulness, but the task did not keep a before/after trend requirement strong enough to distinguish real compaction from adjacent maintenance
- Proposed experiments:
  - freeze adjacent support-slice expansion under `WI-0010` until the next checkpoint records a visible before/after change in dominant entropy metrics
  - choose one explicit hotspot, starting with `scripts/validate_source_repo.sh`, and keep the next reviewable boundary centered there unless a stronger hotspot emerges
  - require every future `WI-0010` checkpoint to include the pre-slice and post-slice values for `pending-active-files`, `new-active-files`, and the current recent-hotspot-touches leader
- Risks of change:
  - a too-rigid hotspot rule could ignore a smaller coupled file that is necessary to keep the slice honest
  - if the chosen hotspot slice adds new surface or starts another controller tangent, the compaction-only lane will regress while claiming discipline
  - delaying adjacent support work can frustrate progress if the repo ultimately needs both hotspot cleanup and an explicit budget raise
- Recommendation:
  - treat compounding-effectiveness regression as the current `WI-0010` issue, not as a side comment
  - keep `WI-0010` active and block further adjacent support expansion until a hotspot slice visibly lowers pressure or an explicit budget decision is written
  - leave `WI-0020` and `WI-0017` blocked behind `WI-0010` until that evidence exists
