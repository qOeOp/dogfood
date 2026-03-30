# Status Snapshot

- Linked work items: WI-0011


- Date: 2026-03-30
- Label: explicit-start concurrency acceptance closeout
- Flush boundary: explicit-target concurrency routing landed in source truth, source/runtime validation passed for the bounded slice, acceptance artifacts are linked, and the terminal transition to `done` completed before this checkpoint
- Crash-safe through: `WI-0011` is `done`, the shared start surface now distinguishes top-attention routing from globally legal explicit start, and reopening can start from the acceptance brief plus targeted validation checkpoint
- New decisions: accept explicit `start --work-item <WI-xxxx>` as the bounded high-level escape hatch when another task remains in `review`, while preserving task-local blocker and scope checks
- Open risks: the broad `run_state_validation_slice.sh` still fails on the unrelated Playwright `locked-live-owner` probe before this regression runs; richer multi-candidate start ergonomics may still be worth a later follow-up if operators keep asking for them
- Follow-ups: keep any Playwright probe work in a separate lane; resume entropy compaction under `WI-0010` without re-blocking this accepted concurrency slice
- What changed in current state: the shared entry surface no longer teaches a false repo-global single-active-task model, because a `review` item can remain top attention while another ready task is started explicitly and safely in parallel
