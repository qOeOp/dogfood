# Process Audit

- Linked work items: WI-0010


- Date: 2026-03-31
- Owner: Workflow & Automation Lead
- Scope: clarify that when entropy pressure materializes or reuses a compaction task that blocks current work, operator focus must transfer to that compaction task immediately
- Signals reviewed:
  - user pushback that a newly created de-entropy task should take over once it blocks other work
  - current `WI-0010` task truth and recovery wording
  - existing entropy auto-interrupt / selector-routing artifacts under `WI-0010`
  - the current runtime behavior where selector/open already routes back into `WI-0010`
- Repeated frictions:
  - if the system only marks `Blocked by` but leaves the operator mentally attached to the interrupted task, the user still has to act as scheduler
  - saying "inspect the support slice first" can read as optional sequencing instead of mandatory focus transfer into the compaction lane
- Cross-task handoff failures:
  - the prior auto-interrupt work fixed pause/resume mechanics, but the user correctly pointed out that the scheduling consequence also needs to be stated plainly: blocking compaction work should become the active object immediately
- Candidate root causes:
  - the system had already gained the mechanics for pause, blocker creation, and selector priority, but the task-local wording did not state the invariant strongly enough
  - "future review boundary" language pulled attention toward artifacts instead of toward the blocking cleanup task itself
- Proposed experiments:
  - restate in task truth that if entropy creates or reuses a blocking compaction task, intake/open/select must jump there first
  - describe the interrupted task as paused background work that resumes only after the compaction blocker clears
- Risks of change:
  - if overstated, this could hide exceptional cases where multiple higher-order blockers exist simultaneously
  - if left implicit, operators may keep treating compaction as advisory instead of mandatory once it blocks active work
- Recommendation:
  - make the invariant explicit: newly created or reused entropy compaction work becomes the immediate active lane when it blocks another task
  - treat any user-visible need to manually choose that jump as a regression in the interrupt controller
