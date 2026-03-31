# Process Audit

- Linked work items: WI-0010


- Date: 2026-03-31
- Owner: Workflow & Automation Lead
- Scope: why `open_work_item.sh` helper dedupe is the next best subtractive cleanup slice after `query_work_items.sh`
- Signals reviewed:
  - the existing `open_work_item.sh` diff showing `46 insertions(+), 154 deletions(-)`
  - helper duplication already retired in `query_work_items.sh`, suggesting the same compaction pattern is safe to extend
  - live dogfood output from `open_work_item.sh --json shared` and `--record shared`
  - current entropy state, which is still `breached / compaction-only`
- Repeated frictions:
  - `open_work_item.sh` is a high-traffic runtime entrypoint, so stale local helper copies there amplify entropy more than edge scripts do
  - repeated recovery-loading and serialization logic increases the cost of every future schema or output-shape change
- Cross-task handoff failures:
  - earlier `WI-0010` work already created canonical recovery and JSON helper surfaces, but not all entrypoints had been brought onto them as explicit compaction slices
- Candidate root causes:
  - helper consolidation happened incrementally, leaving some entrypoints partially duplicated
  - mixed-worktree pressure makes it easy to overlook deletion-dominant slices that are already present and verifiable
- Proposed experiments:
  - accept `open_work_item.sh` as the next helper-compaction slice and keep validating these migrations one script at a time
  - continue preferring bounded helper reuse over fresh wrapper/controller creation
- Risks of change:
  - because this slice also carries metadata exposure via canonical helper payloads, reviewers could overread it as feature work rather than compaction
  - the live entropy breach can still mask whether these local wins compound fast enough
- Recommendation:
  - treat `open_work_item.sh` helper dedupe as the current subtractive boundary after `query_work_items.sh`
  - keep `WI-0010` in-progress and continue selecting deletion-dominant hotspots until the active surface materially shrinks
