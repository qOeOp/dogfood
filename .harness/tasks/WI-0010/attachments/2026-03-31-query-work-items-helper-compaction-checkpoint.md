# Status Snapshot

- Linked work items: WI-0010

- Date: 2026-03-31
- Label: query-work-items-helper-compaction
- Flush boundary: `scripts/query_work_items.sh` now depends on the canonical JSON/record helper surface in `lib_state.sh` instead of keeping its own local copies of `json_escape()`, `record_sanitize()`, and `emit_record()`.
- Crash-safe through: the slice is validated by `sh -n scripts/query_work_items.sh`, plus live dogfood runtime smokes for `query_work_items.sh --json --task-id WI-0010` and `query_work_items.sh --record --status in-progress`.
- New decisions: treat the `query_work_items.sh` helper dedupe as the current subtractive compaction slice under `WI-0010`. Keep the parent task `in-progress`, because this removes one duplication site but does not clear the broader entropy-pressure breach.
- Open risks: this slice does not reduce the `new-active-files` pressure or the `scripts/validate_source_repo.sh` hotspot by itself; it only shrinks one repeated implementation surface.
- Follow-ups: review the bounded `query_work_items.sh` diff, then choose the next subtractive cleanup slice based on which remaining hotspot removes the most repeated active surface without expanding the framework.
- What changed in current state: the worktree now carries a 59-line pure deletion slice in `scripts/query_work_items.sh`, turning one pending compaction candidate into a validated, reviewer-addressable boundary.
