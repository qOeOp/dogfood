# Status Snapshot

- Linked work items: WI-0010

- Date: 2026-03-31
- Label: entropy-auto-interrupt-and-selector-routing
- Flush boundary: `lib_state.sh`, `transition_work_item.sh`, `select_work_item.sh`, `complete_work_item.sh`, and `run_state_validation_slice.sh` now treat entropy pressure as a real interrupt lane: active tasks pause with resume metadata, compaction gets reserved selector priority, and release can return an interrupted task to its preserved target.
- Crash-safe through: `audit_role_schema.sh` passed, `run_state_validation_slice.sh` passed with the new active-task interrupt/resume regression, and real dogfood intake/open now route to `WI-0010` instead of an unrelated legacy review item.
- New decisions: Keep this inside `WI-0010`; do not create a separate broad workflow task. Treat user-visible “should I switch to entropy first?” prompts as harness regressions. Use `entropy-compaction-required` as the dedicated interrupt marker for this lane.
- Open risks: The harness source worktree is still a mixed slice, so this implementation is validated but not yet a clean review candidate. Auto-resume semantics now exist only for entropy-triggered pauses released by blocker completion; other interruption classes stay manual.
- Follow-ups: Carve a reviewable framework slice around the touched scripts, decide whether `WI-0020` should inherit the new interrupt marker semantics for review-boundary pauses, and then review/accept the bounded entropy lane honestly.
- What changed in current state: User criticism about manual entropy arbitration is now durable task truth under `WI-0010`; selector priority, transition semantics, and validation coverage all changed so entropy compaction behaves like an automatic interrupt instead of a user-facing branch choice.
