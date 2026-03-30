# Process Audit

- Linked work items: WI-0010



- Date: 2026-03-30
- Owner: codex
- Scope: why the highest-leverage entropy-control slice this round was wrapper-aware recovery/writeback path correction instead of another local subtractive cleanup in `start/open`
- Signals reviewed:
  - [`/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/scripts/lib_harness_paths.sh`](/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/scripts/lib_harness_paths.sh)
  - [`/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/scripts/lib_state.sh`](/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/scripts/lib_state.sh)
  - [`/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/scripts/run_surface_diagnostic.sh`](/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/scripts/run_surface_diagnostic.sh)
  - [`/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/docs/workflows/surface-audit.md`](/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/docs/workflows/surface-audit.md)
  - [`/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0009/task.md`](/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0009/task.md)
  - [`/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0010/task.md`](/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0010/task.md)
  - [`/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0010/attachments/2026-03-30-consumer-surface-diagnostic.md`](/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0010/attachments/2026-03-30-consumer-surface-diagnostic.md)
  - OpenAI, [Harness engineering: leveraging Codex in an agent-first world](https://openai.com/index/harness-engineering/) (verified 2026-03-30)
  - LangChain, [Long-term memory](https://docs.langchain.com/oss/python/deepagents/long-term-memory) (verified 2026-03-30)
- Repeated frictions:
  - from the dogfood wrapper root, harness usage/help text still emitted `./scripts/...` commands even though the executable surface actually lives under `./.agents/skills/harness/scripts/...`
  - consumer `run_surface_diagnostic.sh` still recommended `.harness/workspace/status/process-audits/` even when the runtime is `minimum-core` and the canonical durable surface is task-local attachments
  - this meant a surface-audit result could be mechanically generated but still leave the operator with the wrong recovery command or the wrong persistence lane
- Cross-task handoff failures:
  - `WI-0009` correctly identified the broken consumer audit path as part of the entropy-effectiveness gap, but the next active slice still drifted toward local code-duplication cleanup before the recovery/writeback entrypoint itself was trustworthy
  - `WI-0010` had already improved detection and compaction triggering, yet recovery still depended on command/path archaeology in the dogfood wrapper
  - the new consumer surface diagnostic proves the loop can now leave behind a task-local artifact, but it also surfaced existing freshness failures that still need follow-up
- Candidate root causes:
  - `harness_command_path` assumed source-repo-relative invocation and did not adapt when the harness lived as an embedded source repo inside a consumer wrapper
  - consumer surface-audit guidance kept a shared-writeback path in the default recommendation even though `minimum-core` makes task-local attachments the canonical first sink
  - compounding work had improved detection, but not every high-level recommendation surface had been audited for wrapper-aware recovery correctness
- Proposed experiments:
  - make `harness_command_path` emit a cwd-correct path when the harness is invoked from a consumer wrapper and fall back to an absolute path only when needed
  - add a narrow `--work-item` lane to `run_surface_diagnostic.sh` so consumer audits can write directly into `.harness/tasks/<task-id>/attachments/` and auto-link the artifact
  - use the real dogfood runtime, not a synthetic note, to validate that the new lane creates a linked `surface-audit` artifact on an active task
- Risks of change:
  - helper-level path rendering is shared by many scripts, so any path regression would affect usage/help text broadly even if core state mutation still works
  - adding task-local writeback to `run_surface_diagnostic.sh` introduces a new state-mutation path that must continue requiring explicit `STATE_ACTOR`
  - this slice does not solve the underlying entropy-pressure breach or the existing freshness failures reported by the new diagnostic
- Recommendation:
  - treat wrapper-aware command recovery plus minimum-core task-local audit writeback as the highest-leverage control-surface fix before another adjacent subtractive cleanup slice
  - keep the non-goal explicit: do not widen this round into a universal task-linking abstraction or a broader freshness remediation sweep
  - resume WI-0010 from the new consumer diagnostic and process audit boundary, then decide whether the next slice should be freshness-follow-up or another subtractive cleanup based on which one most reduces repeated operator archaeology
