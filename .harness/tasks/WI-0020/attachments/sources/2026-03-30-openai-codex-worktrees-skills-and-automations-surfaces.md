# Source Note

- Linked work items: WI-0020


- Date: 2026-03-30
- Source: OpenAI Codex worktrees skills and automations surfaces
- URL: https://openai.com/codex/
- Type: official product documentation / overview
- Accessed date: 2026-03-30
- Trust level: high
- Notes:
  - OpenAI positions Codex as designed for multi-agent workflows with built-in worktrees and cloud environments so agents can work in parallel.
  - The same page presents Skills as the place for reusable, team-aligned operating knowledge.
  - Automations are framed as always-on background work for routine but important lanes such as issue triage and monitoring.

## Optional Detail

- Topic: OpenAI Codex worktrees skills and automations surfaces
- Publisher or owner: OpenAI
- Published date: none
- Claim area: parallel isolation, reusable instruction surfaces, always-on routine work
- Supports:
  - Mixed source changes should be isolated into explicit work items or worktrees rather than silently bundled into one acceptance boundary.
  - Routine cleanup and triage are valid automation targets, so a blocker task is a thinner response than manual review archaeology.
- Conflicts with:
  - Letting one review item stand in for many unrelated pending framework mutations.
