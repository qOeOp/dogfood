# Status Snapshot

- Linked work items: WI-0010

- Date: 2026-03-30
- Label: wrapper-aware-recovery-path
- Flush boundary: wrapper-aware command recovery and minimum-core consumer surface-audit writeback are now durably linked to `WI-0010`; the checkpoint captures the exact state after real-runtime validation and before choosing the next entropy slice.
- Crash-safe through: [`/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/scripts/lib_harness_paths.sh`](/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/scripts/lib_harness_paths.sh) now emits cwd-correct command paths for the embedded harness source repo, [`/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/scripts/run_surface_diagnostic.sh`](/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/scripts/run_surface_diagnostic.sh) can write and auto-link a consumer `surface-audit` directly to a task via `--work-item`, and a real run produced [`/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0010/attachments/2026-03-30-consumer-surface-diagnostic.md`](/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0010/attachments/2026-03-30-consumer-surface-diagnostic.md).
- New decisions: prioritize fixing recovery/writeback path correctness over another immediate local subtractive cleanup slice, because compounding evidence is worthless if the default next-step command and default durable sink are wrong in the dogfood wrapper.
- Open risks: `validate_source_repo.sh` still fails because the entropy pressure gate is already breached in the dirty harness source worktree, and the new consumer surface diagnostic surfaced existing freshness-gate failures in older research memos.
- Follow-ups: choose between a bounded freshness-follow-up slice for the surfaced research artifacts and the next subtractive active-surface cleanup slice only after using the new task-local diagnostic lane to compare leverage.
- What changed in current state: usage/help text from the dogfood root now resolves to `./.agents/skills/harness/scripts/...` instead of the nonexistent `./scripts/...`, and minimum-core consumer audits no longer need to pretend shared writeback exists before they can leave behind reviewable task-local evidence.
