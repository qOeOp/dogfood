# Source Note

- Linked work items: WI-0017


- Date: 2026-03-30
- Source: GitHub issues dependencies and work hierarchy
- URL: https://docs.github.com/en/issues/tracking-your-work-with-issues/using-issues/creating-issue-dependencies ; https://docs.github.com/en/issues/tracking-your-work-with-issues/using-issues/adding-sub-issues
- Type: official product docs
- Accessed date: 2026-03-30
- Trust level: high
- Notes:
  - GitHub issue dependencies explicitly model `blocked by` and `blocking` relationships.
  - GitHub sub-issues explicitly model parent/child decomposition and nested work hierarchies.
  - This supports keeping residual issues as structured objects with relationship/disposition fields instead of only prose notes.

## Optional Detail

- Topic: GitHub issues dependencies and work hierarchy
- Publisher or owner: GitHub
- Published date: docs page current as of 2026-03-30
- Claim area: issue objects should preserve both decomposition and dependency semantics
- Supports:
  - a thin issue ledger should at least preserve blocked/follow-up disposition, even if it does not implement full hierarchy in v1
- Conflicts with:
  - building a second full work-item system inside `.harness/`
