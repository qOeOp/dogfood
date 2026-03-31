# Status Snapshot

- Linked work items: WI-0010

- Date: 2026-03-31
- Label: open-work-item-helper-compaction
- Flush boundary: `scripts/open_work_item.sh` now uses the canonical recovery-loader and JSON/record helper surface from `lib_state.sh` instead of keeping local copies of `recovery_recommended_action()`, `json_escape()`, `json_string_or_null()`, `record_sanitize()`, and `emit_record()`.
- Crash-safe through: the slice is validated by `sh -n scripts/open_work_item.sh`, plus live dogfood runtime smokes for `open_work_item.sh --json shared` and `open_work_item.sh --record shared`.
- New decisions: treat the `open_work_item.sh` helper dedupe as the next bounded subtractive slice under `WI-0010`. This is larger than the `query_work_items.sh` slice, but it still reduces repeated control-surface logic instead of creating new files or new controller layers.
- Open risks: the diff is not pure deletion because the script also now exposes claim/worktree metadata through the canonical JSON object path, so this slice is "deletion-dominant" rather than deletion-only. The broader entropy breach remains unresolved.
- Follow-ups: review the bounded `open_work_item.sh` helper-compaction diff, then continue selecting deletion-oriented hotspots where canonical helper reuse can retire more local logic.
- What changed in current state: `WI-0010` now has a second validated subtractive boundary, extending helper compaction from `query_work_items.sh` into a higher-traffic runtime entrypoint without expanding framework surface.
