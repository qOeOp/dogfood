# Source Note

- Linked work items: WI-0010


- Date: 2026-03-31
- Source: OpenAI Codex staying in flow task queue and background work
- URL: https://cdn.openai.com/pdf/6a2631dc-783e-479b-b1a4-af0cfbd38630/how-openai-uses-codex.pdf
- Type: official product writeup / PDF
- Accessed date: 2026-03-31
- Trust level: high
- Notes:
  - OpenAI describes Codex as useful when schedules are fragmented and interruptions are common because unfinished work can be captured and revisited without losing context.
  - The same document explicitly recommends using the Codex task queue as a lightweight backlog for tangential or incidental work, instead of forcing the user to swap focus manually.
  - This supports treating entropy compaction as an automatic side-lane that preserves the interrupted task's recovery point rather than surfacing a fresh user choice about whether to switch.

## Optional Detail

- Topic: OpenAI Codex staying in flow task queue and background work
- Publisher or owner: OpenAI
- Published date: none
- Claim area: interruption handling, task queueing, focus preservation
- Supports:
  - When entropy pressure appears mid-task, harness should capture the interrupted state and route the operator into the compaction lane automatically.
  - Tangential maintenance work is better modeled as queued or background follow-up than as a prompt-visible context switch the user must arbitrate.
- Conflicts with:
  - Asking the user whether to stop their current task and handle entropy first.
