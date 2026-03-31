# Process Audit

- Linked work items: WI-0010


- Date: 2026-03-31
- Owner: Workflow & Automation Lead
- Scope: user-visible consent-seeking pauses during a long-running, already-selected compaction lane
- Signals reviewed:
  - live user criticism that progress kept pausing on phrases like "if you want" / "if you agree"
  - current `WI-0010` recovery state, which already had a clear active compaction lane and next slice
  - recent interaction pattern where execution updates sometimes drifted into permission-seeking language instead of direct continuation
- Repeated frictions:
  - once the active lane is already clear, asking the user to approve the next micro-step turns the user back into the scheduler
  - this breaks the expectation of long-running autonomous execution and makes the harness feel less reliable than simpler always-continue agents
- Cross-task handoff failures:
  - interrupt-routing and focus-transfer semantics were improved, but the conversational execution layer still occasionally reintroduced manual arbitration at the wrong level
- Candidate root causes:
  - progress updates blurred "I am informing you what I am doing next" with "I am asking permission to continue"
  - the agent over-corrected toward politeness even when no real decision boundary remained
- Proposed experiments:
  - treat consent-seeking pauses as regressions whenever the active work object and next slice are already clear
  - reserve user re-alignment prompts only for real boundary uncertainty, risk, or non-obvious tradeoffs
- Risks of change:
  - if taken too far, the agent could skip necessary escalation when a true decision boundary exists
  - if not corrected, long-running execution will keep degrading into stop-start micro-confirmation
- Recommendation:
  - continue `WI-0010` directly once the next subtractive slice is selected
  - use commentary updates to announce the next action, not to request permission for already-decided work
