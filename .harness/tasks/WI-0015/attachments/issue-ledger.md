# Issue Ledger

- Linked work items: WI-0015


- Date: 2026-03-30
- Owner:
- Scope: task-local residual issues only
- Current issue status (update-only ledger; archive gate summary): open
- Gate policy: archive blocks while any issue row is not closed, or while a promoted-to-followup row lacks a follow-up work item
- Covered trigger paths in this slice: tool-failure / user-criticism

## Issues

| ID | Source | Summary | Evidence / artifact reference | Status | Disposition | Follow-up | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- |
| ISSUE-001 | user-criticism | installed harness skill did not deterministically intercept the first durable user request, so task materialization did not happen before deeper work began | chat:2026-03-30-user-report-harness-skill-not-auto-loaded | open | open | none | Observed in dogfood: the repo had harness installed and .harness already materialized, but the conversation still proceeded without first selecting or creating a work item. This is an intake/control-surface miss, not just a missing artifact writeback. |
