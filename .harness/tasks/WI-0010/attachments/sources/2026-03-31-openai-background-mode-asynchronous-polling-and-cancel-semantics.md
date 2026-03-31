# Source Note

- Linked work items: WI-0010


- Date: 2026-03-31
- Source: OpenAI background mode asynchronous polling and cancel semantics
- URL: https://developers.openai.com/api/docs/guides/background
- Type: official API documentation
- Accessed date: 2026-03-31
- Trust level: high
- Notes:
  - OpenAI documents background mode as the way to run long-running tasks asynchronously and check status by polling over time instead of holding a fragile foreground interaction open.
  - The guide also defines explicit cancel and stream-resume handles, which means interruption and re-entry should be modeled as first-class runtime state rather than conversational improvisation.
  - This supports treating entropy compaction as a resumable control lane with explicit pause/resume state, not as a user-facing question about whether to switch tasks.

## Optional Detail

- Topic: OpenAI background mode asynchronous polling and cancel semantics
- Publisher or owner: OpenAI
- Published date: none
- Claim area: async execution, polling, cancel, resumability
- Supports:
  - Long-running control work should move into an explicit background or interruptible lane with durable status and resume handles.
  - A compaction interrupt should be recoverable without asking the user to restate intent after the pressure is cleared.
- Conflicts with:
  - Treating entropy pressure as an ad hoc conversational fork that depends on the operator asking the user what to do next.
