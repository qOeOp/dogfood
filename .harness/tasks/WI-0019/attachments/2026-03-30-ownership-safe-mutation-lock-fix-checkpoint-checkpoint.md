# Status Snapshot

- Linked work items: WI-0019


- Date: 2026-03-30
- Label: Ownership-safe mutation lock fix checkpoint
- Flush boundary: `lib_state.sh` now records held `lease_id` values and only releases or stale-reclaims a lock when the on-disk lease still matches; `run_state_validation_slice.sh` now contains both an ownership-safe lock regression and an artifact-link fail-closed regression that mirrors the original `WI-0017` failure shape.
- Crash-safe through: fresh-runtime targeted regressions both pass, proving successor lease metadata survives release, a third contender remains blocked while the successor holder is active, and concurrent stale artifact-link writers now fail closed instead of silently corrupting `Linked attachments`.
- New decisions:
  - Stop the line on mutation-lock integrity before resuming `WI-0017` issue-ledger work.
  - Fail closed on stale `expected-version` callers rather than allowing overlapping critical sections to corrupt task truth.
- Open risks:
  - `./scripts/validate_source_repo.sh` is still blocked by the repo's existing entropy-pressure breach, not by this lock patch.
  - `./scripts/run_state_validation_slice.sh` still hits the pre-existing Playwright live-owner probe failure under current sandbox permissions, so full suite confirmation is still noisy.
- Follow-ups:
  - Re-run full source validation once the known entropy and Playwright probe blockers are handled or explicitly waived.
  - Resume `WI-0017` from its paused recovery point after `WI-0019` review confirms lock integrity.
- What changed in current state:
  - ownership-safe lease release is now part of the source truth in `lib_state.sh`
  - lock regression coverage and artifact-link fail-closed regression now both exist in `run_state_validation_slice.sh`
  - `WI-0017` is paused with an explicit blocker pointing at `WI-0019`
