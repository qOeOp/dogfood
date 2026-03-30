# Process Audit

- Linked work items: WI-0010


- Date: 2026-03-29
- Owner: codex
- Scope: source active-surface entropy trigger handling and the planning-shape side effect caused by hardening requirements before option generation is finished
- Signals reviewed:
  - [`/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/scripts/audit_entropy_budget.sh`](/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/scripts/audit_entropy_budget.sh)
  - [`/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/scripts/run_surface_diagnostic.sh`](/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/scripts/run_surface_diagnostic.sh)
  - [`/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/scripts/sync_entropy_compaction_task.sh`](/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/scripts/sync_entropy_compaction_task.sh)
  - [`/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/references/contracts/active-surface-entropy-budget-v1.toml`](/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/references/contracts/active-surface-entropy-budget-v1.toml)
  - [`/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/skills/meeting-router/SKILL.md`](/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/skills/meeting-router/SKILL.md)
  - [`/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/skills/requirements-meeting/SKILL.md`](/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/skills/requirements-meeting/SKILL.md)
  - [`/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/skills/brainstorming-session/SKILL.md`](/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/skills/brainstorming-session/SKILL.md)
  - [`/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/docs/workflows/founder-meeting-taxonomy.md`](/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/docs/workflows/founder-meeting-taxonomy.md)
- Repeated frictions:
  - entropy control historically behaved more like a passive budget line than a triggered cleanup controller, so users mostly saw ongoing `md` and `sh` growth instead of paired subtraction
  - before the routing fix, the consumer surface diagnostic could inspect the source repo instead of the real dogfood runtime, which hid the actual place where entropy should be judged
  - the current planning lane has a `brainstorming-session` bundle, but `requirements-meeting` is not preceded by an explicit ideation gate, so partially explored asks can harden into briefs too early and then get rewritten later
- Cross-task handoff failures:
  - user-reported entropy frustration first appeared as a trust complaint, but the framework had no automatic cleanup work item until this round's trigger script created `WI-0010`
  - meeting routing distinguishes `brainstorming` from `requirements`, yet the downstream `requirements` surface did not force a "why this is past brainstorming" check, so intent could drift from exploration into premature planning
- Candidate root causes:
  - the budget audit emitted useful numbers but lacked task-trigger semantics and compaction-only consequences
  - consumer/runtime truth and source-repo truth were conflated in one diagnostic path
  - the planning control surface over-valued formal requirement artifacts and under-specified when option generation must happen first
- Proposed experiments:
  - keep the new `soft threshold -> entropy task` and `hard threshold -> compaction-only` controller active, and track whether follow-up work now produces visible merge/archive/delete outcomes
  - add a lightweight ideation gate so `requirements-meeting` either references brainstorming input or records why direct scoping is safe
  - keep brainstorming conditional rather than universal: use it when scope is still open, there are multiple plausible cuts, or the user is asking for options/tradeoffs rather than a locked iteration slice
- Risks of change:
  - if brainstorming becomes mandatory for every requirement, the framework will simply trade code entropy for artifact entropy
  - if the ideation gate is too weak, the system will continue formalizing fuzzy requests and generate rewrite churn later
  - if compaction work expands into a broad governance rewrite, it can miss the immediate subtractive cleanup objective that triggered this task
- Recommendation: keep the entropy controller mechanical, but tighten the planning surface with an explicit ideation gate; `brainstorming` should be a required precursor only for unresolved scope, not a blanket ceremony before every planning pass
