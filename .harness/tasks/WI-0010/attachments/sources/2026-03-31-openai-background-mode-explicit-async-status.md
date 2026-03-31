# Source Note

- Linked work items: WI-0010


- Date: 2026-03-31
- Source: OpenAI background mode explicit async status
- URL: https://developers.openai.com/api/docs/guides/background
- Type: official API documentation
- Accessed date: 2026-03-31
- Trust level: high
- Notes:
  - OpenAI documents background mode as the way to run long-running tasks asynchronously instead of depending on a fragile foreground session.
  - The guide says background requests should be polled while they are `queued` or `in_progress`, and only treated as complete after they reach a terminal state.
  - The same guide exposes explicit cancel semantics, reinforcing that long control lanes need visible status and termination boundaries.

## Optional Detail

- Topic: OpenAI background mode explicit async status
- Publisher or owner: OpenAI
- Published date: none
- Claim area: explicit async state, long-running control lanes, terminal-state discipline
- Supports:
  - `WI-0010` should remain an explicit compaction lane until the dominant pressure actually drops or a budget decision is written.
  - Stop-the-line and resume semantics are healthier than conversationally acting as if the lane is already complete.
- Conflicts with:
  - Counting adjacent support work as enough progress while the governing entropy lane is still getting worse.
