# Status Snapshot

- Linked work items: WI-0011



- Date: 2026-03-29
- Label: explicit-start-targeted-validation
- Flush boundary: reproduced the `run_shared_start_explicit_target_regression` logic from the current harness source in a fresh materialized runtime fixture, without relying on the unrelated Playwright probe in the broad validation slice
- Crash-safe through: the bounded concurrency regression passed against the current source working tree, and the resulting review handoff can reference this checkpoint directly
- New decisions:
  - `WI-0011` should be judged by the explicit shared-start concurrency regression plus the worktree-parallelism/source-note evidence, not by the unrelated Playwright profile probe that runs earlier in the broad validation slice
  - the remaining Playwright `locked-live-owner` failure is a separate follow-up signal and should not be reintroduced as a blocker on this task record
- Evidence:
  - in a fresh fixture, `start_work_item.sh --json shared` still reports the `review` item as the top-attention selection and returns `finish_review_or_start_explicit_other_work_item`
  - in the same fixture, `work_item_ctl.sh start --json --work-item <ready-id> shared` returns `started` for the explicitly targeted ready item
  - the review item stays in `review`, while the targeted ready item moves to `in-progress` and is claimed by `validation-slice`
- Open risks:
  - `cd .agents/skills/harness && ./scripts/run_state_validation_slice.sh` still fails before this regression on the existing Playwright `locked-live-owner` probe
  - if review requires an all-in-one green broad slice, that broad-slice failure still needs a separate owner/task decision
- Next step:
  - move `WI-0011` to `review` with this checkpoint linked as current validation evidence
