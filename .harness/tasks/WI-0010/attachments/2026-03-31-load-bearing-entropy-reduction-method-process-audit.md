# Process Audit

- Linked work items: WI-0010


- Date: 2026-03-31
- Owner: Workflow & Automation Lead
- Scope: establish an explicit entropy-reduction method based on load-bearing analysis before further subtractive cleanup
- Signals reviewed:
  - user instruction to follow an "analysis-bearing first, clear non-bearing features, then continue optimizing bearing features" approach
  - current `WI-0010` slices across `query_work_items.sh` and `open_work_item.sh`
  - remaining mixed diffs in `select_work_item.sh`, `complete_work_item.sh`, `start_work_item.sh`, and `validate_source_repo.sh`
- Repeated frictions:
  - without a fixed reduction method, entropy work can oscillate between real deletion, process discussion, and accidental edits to core control logic
  - mixed files make it easy to mistake load-bearing changes for easy cleanup targets
- Cross-task handoff failures:
  - the task had already gathered several bounded slices, but the decision rule for "which slice next" was still too implicit
- Candidate root causes:
  - active-surface reduction was being chosen opportunistically instead of through an explicit bearing analysis
  - helper-dedupe wins were real, but the repo lacked a durable rule for when to pause load-bearing optimization and when to keep deleting surrounding support logic
- Proposed experiments:
  - define load-bearing surfaces as routing, interrupt/resume semantics, blocker semantics, review/acceptance truthfulness, and any logic that changes which work item becomes active
  - define non-load-bearing surfaces as duplicated serializers, local helper copies, redundant path-resolution wrappers, and equivalent output-shape plumbing around already-validated control logic
  - in compaction-only mode, prefer deletion-dominant non-load-bearing cleanup first; only return to direct load-bearing optimization after the surrounding support clutter is reduced
- Risks of change:
  - the method can be misused to avoid necessary load-bearing edits when the real blocker is still semantic, not structural
  - if the bearing analysis is too coarse, some mixed slices will still contain both kinds of change and require bounded review carriers
- Recommendation:
  - adopt this as the standing `WI-0010` method
  - treat `select_work_item.sh` as currently load-bearing because it changes active-lane routing priority
  - treat `complete_work_item.sh` helper dedupe as the next cleanup boundary around a load-bearing controller, because its large local helper deletions reduce support clutter while preserving the already-validated truthfulness fix
