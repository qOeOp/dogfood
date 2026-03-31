# Process Audit

- Linked work items: WI-0010


- Date: 2026-03-31
- Owner: Workflow & Automation Lead
- Scope: clarify the difference between "the task has executed meaningful implementation work" and "the task has entered its formal review gate"
- Signals reviewed:
  - user pushback that `WI-0010` was still `in-progress` while the handoff text had already started talking about review
  - current `WI-0010` objective, done criteria, and next gate
  - recent `WI-0010` artifacts covering the entropy auto-interrupt implementation and the mixed-worktree review boundary
  - transition history showing only `in-progress -> in-progress` field updates during the latest review-carrier writeback
- Repeated frictions:
  - "prepare a review boundary" and "the task is now in review" were described too loosely, so the operator language implied a gate transition that did not happen
  - this makes real task execution look fake, because implementation work and validation already happened even though the overall control task is not yet review-ready
- Cross-task handoff failures:
  - the latest handoff text correctly pointed to the bounded carrier, but it omitted the explicit statement that the carrier exists to prepare a future review gate while `WI-0010` itself remains `in-progress`
- Candidate root causes:
  - gate vocabulary was overloaded: "review" was used both for a future handoff target and for the current lifecycle state
  - `WI-0010` is a control task with a larger done condition than the sub-slice that was already implemented and validated
- Proposed experiments:
  - rewrite `WI-0010` handoff/recovery wording so it says "prepare or inspect the future review boundary" instead of implying the task has already entered `review`
  - keep explicit references to the completed implementation work and validation so the task does not look like pure paperwork
- Risks of change:
  - if the wording becomes too defensive, it can hide the fact that a real reviewer still needs a bounded slice later
  - if the wording stays vague, the same confusion will recur whenever a sub-slice is implemented before the parent task is formally review-ready
- Recommendation:
  - state the distinction explicitly: `WI-0010` has already executed the entropy auto-interrupt implementation and validation work, but the parent compaction/control task remains `in-progress`
  - reserve "enter review" language for the actual state transition, not for preparation of a review carrier
