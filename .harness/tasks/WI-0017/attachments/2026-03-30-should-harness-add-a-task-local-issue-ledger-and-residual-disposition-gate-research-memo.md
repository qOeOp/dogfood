# Research Memo

- Linked work items: WI-0017


- Date: 2026-03-30
- Owner: codex
- Question: Should harness add a task-local issue ledger and residual disposition gate?
- Scope: external official docs plus internal runtime/control-surface inspection for the thinnest first slice only
- Research dispatch: .harness/tasks/WI-0017/attachments/2026-03-30-task-local-issue-ledger-and-residual-disposition-controller-external-sensing-research-dispatch.md
- Verification date: 2026-03-30
- Verification mode: mixed
- Freshness level: volatile
- Sources reviewed:
  - .harness/tasks/WI-0017/attachments/sources/2026-03-30-github-issues-dependencies-and-work-hierarchy.md
  - .harness/tasks/WI-0017/attachments/sources/2026-03-30-openai-harness-engineering-agent-first-repository-knowledge-and-feedback-loops.md
  - .harness/tasks/WI-0017/attachments/sources/2026-03-30-jira-work-item-model-as-issue-carrier.md
- Conflicting sources: none on the need for structured issue objects; disagreement is only about how much hierarchy the first slice should encode
- Earliest-source check: internal accepted tasks WI-0005, WI-0014, WI-0015, and WI-0019 still show residual process debt scattered across checkpoints, audits, and planned follow-up lanes
- Strongest evidence:
  - GitHub now treats sub-issues and blocking relationships as first-class issue features, which supports explicit parent/child and blocked-by semantics instead of prose reconstruction.
  - OpenAI's harness engineering writeup argues that repository knowledge and feedback loops must be explicit and agent-legible to compound reliably.
  - Internal sensing found that `record_tool_failure.sh` wrote checkpoints and recovery, but not a reusable issue object; archive obligations also had no residual-disposition gate.
- Strongest counter-evidence:
  - Jira-style hierarchy proves that issue systems can grow deep quickly; copying that full model into harness now would overbuild the carrier and enlarge the active surface.
- Unknowns:
  - Whether a later slice should expose a higher-level criticism controller instead of a narrow wrapper script
  - Whether archive should eventually require an approved issue ledger whenever one exists, not just "no unresolved rows"
- Risks:
  - A per-issue file tree under `refs/` would activate an only-partially-materialized runtime surface and force broader contract churn.
  - A purely prose checkpoint strategy would keep the current archaeology problem alive under a new name.
- Recommendation:
  - Yes. Add a single task-local, update-only `issue-ledger` under `attachments/`, not a per-issue `refs/` tree.
  - Route one existing tool-failure path and one explicit user-criticism path into that ledger.
  - Add a done-to-archived blocking obligation that fails closed while any ledger row is still open, or while a `promoted-to-followup` row lacks a follow-up work item pointer.
  - Keep richer hierarchy, automatic criticism ingestion, and broader closeout ritual design out of this slice.
