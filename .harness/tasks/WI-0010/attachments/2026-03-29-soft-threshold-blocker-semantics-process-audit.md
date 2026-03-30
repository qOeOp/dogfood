# Process Audit

- Linked work items: WI-0010,WI-0011


- Date: 2026-03-29
- Owner: codex
- Scope: audit why the new source entropy controller is still being represented downstream as a hard validation failure even though the current gate runs in soft-threshold task-trigger mode
- Signals reviewed:
  - [`/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0010/task.md`](/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0010/task.md)
  - [`/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0011/task.md`](/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0011/task.md)
  - current output of [`/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/scripts/audit_entropy_budget.sh`](/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/scripts/audit_entropy_budget.sh): `growth state: soft-threshold`, `control state: task-trigger`, `entropy task trigger: true`
  - current output of [`/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/scripts/validate_source_repo.sh`](/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/scripts/validate_source_repo.sh): `source repo audit: ok`
  - current output of [`/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/scripts/start_work_item.sh`](/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/scripts/start_work_item.sh) for `WI-0011`, which still reports `blocked by WI-0010` because task truth says source acceptance is blocked until entropy falls below thresholds
  - OpenAI, "Harness engineering: leveraging Codex in an agent-first world" (2026-02-11), which argues that repository knowledge must stay mechanically enforced and current rather than rotting into stale instruction blobs
  - Anthropic, "Building Effective AI Agents" (2024-12-19), which recommends simple, composable control patterns grounded in real tool feedback instead of adding framework complexity prematurely
- Repeated frictions:
  - the entropy controller now emits an explicit compaction task trigger at soft threshold, but `WI-0011` still models that state as if `validate_source_repo.sh` were failing hard
  - this misclassification materially changes operator behavior because explicit `start --work-item WI-0011` returns `blocked` from task truth rather than from a real failing validator
  - the recovery text for `WI-0011` therefore points future resumes at the wrong condition: it says to wait for `validate_source_repo.sh` to clear, but that command already passes
- Cross-task handoff failures:
  - `WI-0009` identified that entropy controls were mostly budget signaling rather than visible subtractive cleanup
  - `WI-0010` introduced the task-trigger controller, but the downstream task that was supposed to be gated by it kept the old "hard source validation failure" mental model
  - this means the compounding chain improved the controller but did not keep downstream task truth aligned with the new semantics
- Candidate root causes:
  - the soft-threshold controller is intentionally lighter than a hard validator failure, but downstream blocker text was written as though the older hard-fail model still applied
  - the runtime currently has no typed representation for "explicit compaction decision pending", so a free-text blocker overfit to a validator-shaped explanation
  - adding a new reconciler immediately would increase source surface before we have evidence that the drift is recurrent beyond this concrete task
- Recommendation:
  - treat the current problem as truth drift first, not as a reason to add another controller
  - keep `WI-0010` open as explicit compaction/decision work, but stop representing that soft-threshold state as an automatic source-validation failure on unrelated downstream tasks
  - clear the false blocker semantics from `WI-0011`, update its recovery to the real next step, and only promote a framework-generic typed gate if this drift recurs after truthful task writeback
- Verification boundary:
  - this audit does not claim source entropy is solved; it only establishes that the current downstream blocker wording is stronger than the actual controller state
  - current broad slice validation still fails in [`/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/scripts/run_state_validation_slice.sh`](/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/scripts/run_state_validation_slice.sh) on the existing Playwright `locked-live-owner` check, so the remaining validation risk should stay explicit in task recovery rather than being silently folded into entropy blocking
