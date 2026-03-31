# Process Audit

- Linked work items: WI-0010


- Date: 2026-03-31
- Owner: Workflow & Automation Lead
- Scope: clarify that `WI-0010` is still the source cleanup / entropy-reduction lane, not a renamed review-boundary or routing task
- Signals reviewed:
  - user pushback that `WI-0010` should mean cleanup and entropy reduction
  - current `WI-0010` objective, ready criteria, and done criteria
  - recent entropy auto-interrupt and review-carrier artifacts created under `WI-0010`
  - current recovery/handoff wording, which had become overly centered on the support slice
- Repeated frictions:
  - recent progress was real, but it was focused on a support mechanism, so the parent task started reading like "review the support slice" instead of "reduce entropy"
  - this creates scope drift: the operator can mistake a validated support fix for completion of the underlying cleanup task
- Cross-task handoff failures:
  - the new review carrier fixed one handoff problem, but it also made the current `WI-0010` surface understate the actual cleanup objective
- Candidate root causes:
  - the most recent sub-slice was highly visible because it changed runtime behavior and recovery flow
  - task summary and recovery text were not re-anchored to the parent objective after that sub-slice landed
- Proposed experiments:
  - restate in task truth that entropy auto-interrupt and review-boundary work are enabling mechanics inside `WI-0010`
  - shift handoff wording back toward subtractive cleanup / source ambiguity reduction after the support slice is inspected
- Risks of change:
  - if the task is described too broadly again, the already completed support slice can disappear from view
  - if the task stays support-slice-centric, the repo may confuse "better routing into compaction" with "actual compaction happened"
- Recommendation:
  - keep `WI-0010` anchored to cleanup /减熵
  - describe the auto-interrupt and review-carrier work as already-executed support slices that make the compaction lane honest and resumable
  - make the next step explicitly return from support-slice inspection to subtractive cleanup or source-slice reduction
