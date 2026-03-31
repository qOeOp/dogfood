# Process Audit

- Linked work items: WI-0010


- Date: 2026-03-31
- Owner: Workflow & Automation Lead
- Scope: why the entropy auto-interrupt fix is behaviorally validated but still lacks an honest reviewer entrypoint when the harness source worktree is mixed
- Signals reviewed:
  - current `WI-0010` task truth, checkpoint, and recovery
  - `git status --short` in `./.agents/skills/harness/`, showing many unrelated dirty paths outside the entropy slice
  - `git diff --stat` on the five touched source files, showing a 2700+ line mixed diff instead of a thin review surface
  - function-level locations of the actual entropy auto-interrupt change points and their paired regressions
  - existing `WI-0020` stop-the-line history around review-boundary collapse
- Repeated frictions:
  - the implementation is real, but the default review entry still collapses back to raw full-file diffs that include unrelated earlier work
  - this forces the operator or reviewer to reconstruct scope from chat memory, which is exactly the kind of implicit boundary the harness is supposed to eliminate
  - without a thin carrier, the system can claim "ready for review" while the reviewer still cannot explain what was actually validated
- Cross-task handoff failures:
  - `WI-0020` already proved that unclear framework promotion boundaries should stop acceptance, but `WI-0010` still lacked a reviewer-facing carrier once its own changes lived inside mixed files
  - earlier compaction progress reduced user-facing entropy arbitration, but it did not reduce review-surface ambiguity for the next handoff
- Candidate root causes:
  - review handoff is still too tightly coupled to file-level diffs instead of an explicit bounded slice
  - `WI-0010` changed behavior inside heavily edited shared scripts, so raw diff size no longer matches the logical slice the task actually owns
  - there is no dedicated review-summary primitive yet, so the operator falls back to either oversized diffs or chat reconstruction
- Proposed experiments:
  - attach a task-local checkpoint that names the exact entropy auto-interrupt functions and regressions under review
  - repoint `WI-0010` recovery and next handoff to that bounded artifact instead of to generic `git diff` commands
  - keep the task `in-progress` until a later round either physically compacts the source slice or promotes a reusable review-carrier primitive
- Risks of change:
  - an artifact-defined boundary can under-specify hidden side effects if the reviewer never inspects surrounding code
  - if overused, this could normalize artifact-only review instead of fixing the underlying source entropy
  - the worktree can still accumulate more unrelated edits before review happens, so the carrier must stay explicit about being a temporary boundary
- Recommendation:
  - treat the checkpoint/process-audit pair as an honest temporary review carrier for `WI-0010`
  - do not move `WI-0010` to `review` yet, and do not claim the mixed full-file diffs are acceptable review surfaces
  - make the next compaction step either a physical slice cleanup or a generic review-summary primitive, not another round of implicit reviewer reconstruction
