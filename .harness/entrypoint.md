# Harness Entrypoint

Read in this order:

1. `.harness/README.md`
2. `.harness/self-evolution-loop.md` (闭环执行约束)
3. `.harness/tasks/<task-id>/task.md` when a task exists
4. `.harness/tasks/<task-id>/task.md` `## Recovery` section when a task is active or paused

Runtime notes:

- Mode: minimum-core
- Task truth lives under `.harness/tasks/<task-id>/`
- Recovery lives inside each task record
- Long-running tasks should carry an explicit budget / stop boundary in `## Recovery`
- Steady-state resume should run a cheap baseline check before the recorded next command
- Slow human approval / review should pause the task and resume later, not hide in session wait state
- Resume is checkpoint-relative re-entry; do not assume exactly-once execution before the boundary
- Async wakeups should assume at-least-once delivery and use dedupe / idempotency handles
- Provider-side stored state and auto-injected project memory are continuity aids, not task truth
- Built-in tracing defaults should be treated as opt-in capture policy, not implicit baseline
- Harness does not manage consumer root/provider entry files or skill install location
