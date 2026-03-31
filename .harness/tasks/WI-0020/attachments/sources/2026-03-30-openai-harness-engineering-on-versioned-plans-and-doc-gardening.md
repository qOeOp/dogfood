# Source Note

- Linked work items: WI-0020


- Date: 2026-03-30
- Source: OpenAI harness engineering on versioned plans and doc-gardening
- URL: https://openai.com/index/harness-engineering/
- Type: official engineering article
- Accessed date: 2026-03-30
- Trust level: high
- Notes:
  - OpenAI describes a short `AGENTS.md` as a map, with structured repo docs as the real system of record.
  - The article explicitly says active plans, completed plans, and known technical debt are versioned and co-located in the repository.
  - OpenAI also says they enforce this mechanically and run recurring doc-gardening agents that open cleanup PRs for stale or obsolete docs.

## Optional Detail

- Topic: OpenAI harness engineering on versioned plans and doc-gardening
- Publisher or owner: OpenAI
- Published date: 2026-02-11
- Claim area: repo-local system of record, mechanical enforcement, cleanup discipline
- Supports:
  - If a framework slice cannot be reviewed as a versioned, co-located unit, acceptance should stop rather than relying on conversational memory.
  - A recurring cleanup lane is compatible with explicit task-local blockers and does not require broad new governance surfaces.
- Conflicts with:
  - Treating a mixed dirty worktree as “good enough” review context for an acceptance decision.
