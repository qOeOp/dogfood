# Process Audit

- Linked work items: WI-0010


- Date: 2026-03-31
- Owner: Workflow & Automation Lead
- Scope: why repeated micro-confirmation phrasing can still leak through even after `WI-0010` task truth explicitly forbids it
- Signals reviewed:
  - repeated user criticism that commentary still contained micro-confirmation phrasing after earlier writeback
  - current `WI-0010` summary and recovery notes, which already classify consent-seeking pauses as regressions
  - observed behavior that task truth changed, but natural-language commentary still occasionally reintroduced the same pattern
- Repeated frictions:
  - soft task-truth guidance can reduce the pattern, but it cannot hard-stop an already-running model from generating the same phrasing again
  - this makes the harness appear forgetful even when the task record is correct, because the control surface and the language surface are not yet equally enforceable
- Cross-task handoff failures:
  - the process audit and recovery updates correctly recorded the regression, but they did not create a hard execution guard at the commentary-generation layer
- Candidate root causes:
  - current harness enforcement mostly lives in scripts, task records, and runtime routing, while commentary phrasing is still controlled by prompt/policy rather than a typed runtime contract
  - there is no fail-closed check that rejects or rewrites micro-confirmation language before it reaches the user
- Proposed experiments:
  - treat this as a framework-level control gap, not as a user misunderstanding
  - later, introduce a stronger runtime or policy guard for commentary-generation on active long-running tasks
- Risks of change:
  - over-hardening could suppress necessary escalation when a real decision boundary exists
  - under-hardening keeps making the harness look less autonomous than the execution substrate actually is
- Recommendation:
  - record the honest boundary now: current harness can soft-constrain but not fully hard-enforce commentary against micro-confirmation phrasing
  - keep executing `WI-0010` without re-asking permission, while treating the absence of a hard language guard as an open framework issue
