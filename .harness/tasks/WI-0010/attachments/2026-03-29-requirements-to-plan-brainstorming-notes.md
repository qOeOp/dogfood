# Brainstorming Notes

- Linked work items: WI-0010


- Date: 2026-03-29
- Host: codex
- Topic: should harness require brainstorming before turning requirements into a plan
- Ideas generated:
  - add an ideation gate so `requirements-meeting` must either reference brainstorming input or explain why the request is already converged enough to skip it
  - route to `brainstorming-session` whenever the user is asking for candidate cuts, tradeoff exploration, or experiments instead of a settled iteration slice
  - keep the gate local to planning surfaces and avoid creating a repo-wide new ceremony or global board state
  - treat "number of plausible options still on the table" as the practical signal, not a fixed meeting taxonomy keyword
- Strongest ideas:
  - `requirements` should not be used to invent the option set
  - a single "brainstorming reference or skip rationale" field is cheap and forces a useful moment of honesty
- Weakest ideas:
  - make brainstorming mandatory for every requirement handoff
  - create a separate new planning role just to host ideation
- Open questions:
  - what is the cleanest threshold for "multiple plausible cuts" in day-to-day use
  - whether the same ideation gate should also apply to internal technical planning, not just founder-facing requirement work
- External claims needing freshness check:
  - none
- Candidate experiments:
  - patch `meeting-router` and `requirements-meeting` to prefer `brainstorming-session` for still-open asks
  - add a `Brainstorming reference or skip rationale` line to the requirements brief template
  - watch whether later requirement rewrites and scope churn drop after this guard lands
- What requires formal research:
  - whether other agent teams see measurable throughput gains from making ideation gates explicit rather than implicit
