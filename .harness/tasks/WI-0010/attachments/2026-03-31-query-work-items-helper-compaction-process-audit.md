# Process Audit

- Linked work items: WI-0010


- Date: 2026-03-31
- Owner: Workflow & Automation Lead
- Scope: why `query_work_items.sh` helper dedupe is the highest-leverage subtractive cleanup slice to advance `WI-0010` right now
- Signals reviewed:
  - `audit_entropy_budget.sh` showing `growth state: breached`, `control state: compaction-only`, `new-active-files: 9`, and `pending-active-files: 47`
  - full worktree diff showing many mixed changes, making broad cleanup unsafe as a single honest slice
  - the `scripts/query_work_items.sh` diff, which is a 59-line pure deletion boundary with no new file creation
  - live dogfood smokes proving `query_work_items.sh` still emits valid `json` and `record` output after the dedupe
- Repeated frictions:
  - repeated JSON/record helper implementations inflate the active surface and force every work-item query path to carry its own serialization code
  - broad entropy work can easily sprawl when the worktree is already mixed, so bounded pure-deletion slices matter more than ambitious rewrites
- Cross-task handoff failures:
  - recent `WI-0010` work improved routing into the compaction lane, but without a concrete subtractive slice the task could still look like process-only motion
- Candidate root causes:
  - canonical helper functions already exist in `lib_state.sh`, but some scripts still carried stale local copies
  - the live entropy breach makes it tempting to tackle too much at once instead of validating a single honest deletion boundary
- Proposed experiments:
  - keep `query_work_items.sh` on the shared helper surface only
  - use this validated pure-deletion slice as the template for subsequent subtractive cleanup choices
- Risks of change:
  - this slice is too small to clear the entropy audit on its own
  - if we celebrate it as "the fix," `WI-0010` will drift away from the broader active-surface reduction objective
- Recommendation:
  - accept `query_work_items.sh` helper dedupe as the current subtractive compaction slice
  - keep `WI-0010` in-progress and use the new checkpoint as the durable boundary before choosing the next cleanup target
