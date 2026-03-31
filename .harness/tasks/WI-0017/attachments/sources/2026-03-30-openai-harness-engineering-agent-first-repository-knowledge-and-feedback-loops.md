# Source Note

- Linked work items: WI-0017


- Date: 2026-03-30
- Source: OpenAI harness engineering agent-first repository knowledge and feedback loops
- URL: https://openai.com/index/harness-engineering/
- Type: primary engineering writeup
- Accessed date: 2026-03-30
- Trust level: high
- Notes:
  - The article frames repository knowledge as system-of-record and feedback loops as the core mechanism for compounding agent reliability.
  - It explicitly argues that when something fails, the fix should be a capability or control-surface improvement, not "try harder next time."
  - This supports turning residual execution debt into agent-legible issue objects instead of leaving it in chat memory or scattered prose artifacts.

## Optional Detail

- Topic: OpenAI harness engineering agent-first repository knowledge and feedback loops
- Publisher or owner: OpenAI
- Published date: 2026-02-11
- Claim area: agent-first repos need explicit knowledge surfaces and feedback loops
- Supports:
  - task-local issue capture as a feedback-loop primitive
  - fail-closed residual disposition before declaring closeout complete
- Conflicts with:
  - informal "remember this next time" handling
