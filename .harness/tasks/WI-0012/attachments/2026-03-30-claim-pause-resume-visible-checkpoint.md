# Status Snapshot

- Linked work items: WI-0012


- Date: 2026-03-30
- Label: claim-pause-resume-visible
- Flush boundary: `lib_state.sh`, `open_work_item.sh`, `start_work_item.sh`, and `run_state_validation_slice.sh` are updated in the working tree; `WI-0012` task truth records a real start, pause, and resume path in the dogfood runtime.
- Crash-safe through: `run_state_validation_slice.sh` passes with the new claim-visibility assertions, and `WI-0012` has already exercised a live `in-progress -> paused -> in-progress` proof with renewed claim lease metadata.
- New decisions:
  - Treat this slice as proof-and-surface hardening, not as invention of a brand-new claim kernel.
  - Expose claim metadata on high-level `start/open` JSON surfaces so the existing kernel is visible to operators and regressions.
- Open risks:
  - `open_work_item.sh --json shared` in the real dogfood runtime still selects the top actionable review task, so claim visibility is most obvious through explicit targeting or sandbox validation rather than generic shared selection.
  - Source-wide acceptance still depends on broader repo gates outside this focused validation slice.
- Follow-ups:
  - Decide in review whether any remaining gap warrants a tiny follow-up for blocked-candidate ergonomics, or whether this slice is already sufficient.
- What changed in current state:
  - `start_work_item.sh --json --work-item WI-0012 shared` now emits `assignee`, `worktree`, `claimed_at`, `claim_expires_at`, and `lease_version`.
  - `open_work_item.sh` now emits the same claim metadata for actionable and blocked task projections.
  - `run_state_validation_slice.sh` now fails if those claim fields disappear from the high-level JSON control surface.
  - `WI-0012` itself was started, paused for `risk-review-required`, and resumed successfully, proving live dogfood pause/resume semantics and lease rotation.
