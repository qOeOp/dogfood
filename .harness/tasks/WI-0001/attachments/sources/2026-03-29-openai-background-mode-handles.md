# Source Note

- Linked work items: WI-0001


- Date: 2026-03-29
- Source: OpenAI background mode handles
- URL: https://developers.openai.com/api/docs/guides/background
- Type: official-doc
- Accessed date: 2026-03-29
- Trust level: high
- Notes: OpenAI describes background mode as asynchronous long-running execution where developers poll response objects over time, and it explicitly calls out retained response data plus Zero Data Retention implications, reinforcing that transport continuity and retained provider state are separate from local canonical task truth.

## Optional Detail

- Topic: OpenAI background mode handles
- Publisher or owner: OpenAI
- Published date: none
- Claim area: resumability / transport-state boundary
- Supports: Harness should rely on explicit local runtime state for recovery and not assume hidden session continuity or provider-managed state is a substitute for consumer task truth.
- Conflicts with: none
