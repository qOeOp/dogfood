# Process Audit

- Linked work items: WI-0019


- Date: 2026-03-30
- Owner: codex
- Scope: why this round pivoted from `WI-0017` issue-ledger design into a stop-the-line mutation-lock fix
- Signals reviewed:
  - paused [`WI-0017`](/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0017/task.md) after concurrent research-artifact creation lost two linked source notes
  - concurrent transition events under `.harness/tasks/WI-0017/history/transitions/` showing three separate `in-progress -> in-progress` artifact-link writes with `Version before: 7` and `Version after: 8`
  - [`lib_state.sh`](/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/scripts/lib_state.sh) lock lifecycle around `acquire_named_lock` and `release_registered_locks`
  - targeted lock regression run proving successor lease metadata survives release and a third contender stays blocked while the successor holder is active
- Repeated frictions:
  - task-local artifacts can be created in parallel, but task truth silently keeps only the last surviving linked-attachment snapshot
  - transition history can claim multiple successful artifact-link writes even when the canonical header lost earlier entries
  - higher-level work such as `WI-0017` issue-ledger design becomes unsafe because the substrate can corrupt truth before the new controller even exists
- Cross-task handoff failures:
  - external sensing initially converged on issue-ledger work, but the first real artifact-first step surfaced a more fundamental runtime corruption path
  - `WI-0017` therefore could not responsibly continue, because any new residual-disposition surface would inherit broken task-truth mutation semantics
- Candidate root causes:
  - `release_registered_locks` deleted lock directories unconditionally during `EXIT` trap handling, so an earlier owner could remove a successor lease created on the same lock path
  - stale lock reclaim in `acquire_named_lock` used the same unconditional directory cleanup pattern, so reclaim could race with a fresh successor lease
  - optimistic `expected-version` checks only fail closed if mutual exclusion holds; once successor leases can be deleted, parallel writers can enter overlapping critical sections and overwrite each other
- Proposed experiments:
  - store the acquired `lease_id` in process-local state and only delete a lock directory when the current on-disk `lease_id` still matches that held lease
  - apply the same lease-match guard to stale reclaim paths before deleting lock metadata
  - keep a bounded regression in `run_state_validation_slice.sh` that proves both successor-lease preservation and third-writer exclusion
- Risks of change:
  - this slice hardens lease ownership only; it does not add automatic retries for stale `expected-version` callers, so parallel stale writers will fail closed instead of succeeding magically
  - full source validation remains noisy because the repo is already in entropy-breach mode and the existing Playwright live-owner probe still fails under current sandbox permissions
- Recommendation:
  - treat ownership-safe mutation-lock release as the highest-leverage fix for this round
  - keep `WI-0017` paused until `WI-0019` is reviewed or resumed with trusted task-truth semantics
  - do not resume higher-level issue-ledger work until lock integrity is accepted or explicitly waived
