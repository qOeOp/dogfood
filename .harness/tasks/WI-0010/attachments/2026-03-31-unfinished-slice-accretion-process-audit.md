# Process Audit

- Linked work items: WI-0010



- Date: 2026-03-31
- Owner: Workflow & Automation Lead
- Scope: active checkpoint accretion caused by soft-confirmation pauses and slice switching before the current slice was fully closed
- Signals reviewed:
  - live user criticism that work kept stopping for soft confirmation and left many pending todos without finishing one concrete thing
  - current `WI-0010` linked attachments, which had accumulated six `checkpoint|active` entries plus an old `surface-audit|active`
  - neighboring task `WI-0020`, which had also accumulated two `checkpoint|active` entries instead of one current execution carrier
  - current harness source behavior, where `link_work_item_artifact.sh` allowed a new `checkpoint|active` to be added without retiring the previous one
- Repeated frictions:
  - announcing a new slice before the current slice is truly closed makes the task feel busy but not finished
  - recovery and handoff surfaces become noisier because multiple stale checkpoints keep masquerading as current work
  - entropy-reduction work can paradoxically become another entropy source when execution carriers are never compacted
- Cross-task handoff failures:
  - `WI-0010` and `WI-0020` both carried multiple active checkpoints, so recovery truth no longer pointed at a single authoritative slice
  - the framework had a soft expectation of continuity, but no hard guard that retired stale active checkpoints when a new one became current
- Candidate root causes:
  - `active` status on checkpoints was treated as an append-only marker instead of a singleton execution surface
  - conversational pauses encouraged slice hopping without a matching status compaction step
  - audit coverage validated linked-artifact shape, but not the stronger invariant that a task should have only one active checkpoint at a time
- Proposed experiments:
  - auto-supersede older `checkpoint|active` entries whenever a new active checkpoint is linked or reactivated
  - fail workspace/state audit when a task retains more than one active checkpoint
  - keep one explicit rule in task recovery: do not announce the next slice until the current slice has checkpoint, validation, and recovery writeback
- Risks of change:
  - some older tasks may already rely on multi-active checkpoint history and will need a one-time cleanup before the new audit can pass
  - overgeneralizing this into "only one active artifact of any kind" would break legitimate carriers such as open issue ledgers
- Recommendation:
  - treat `checkpoint|active` as a singleton execution carrier
  - auto-retire older active checkpoints to `superseded`
  - clean legacy tasks so only the latest checkpoint remains active, then continue `WI-0010` from that single bounded slice
