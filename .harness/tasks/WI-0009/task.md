# Work Item

- Schema version: 2
- State authority: script-only
- State version: 5
- Last operation ID: OP-20260329T214909-95285-WI-0009-backlog-to-planning
- Last transition event: .harness/tasks/WI-0009/history/transitions/TX-20260329T214909-WI-0009-backlog-to-planning.md
- ID: WI-0009
- Title: Entropy reduction effectiveness gap
- Type: control
- Status: planning
- Priority: critical
- Owner: Workflow & Automation Lead
- Sponsor: general-manager
- Assignee: none
- Worktree: none
- Claimed at: none
- Claim expires at: none
- Lease version: 0
- Objective: Determine why harness entropy controls are not producing visible subtractive outcomes, validate the gap against current agent-engineering practice, and define the minimum enforceable improvement slices.
- Ready criteria: Audit source and consumer entropy gates on the real dogfood repo, collect external evidence from official/community practice, and isolate the highest-leverage mechanical fixes.
- Done criteria: Task truth plus attached process-audit and research memo explain the failure modes clearly, distinguish active-surface entropy from expected runtime history growth, and narrow follow-up work to a small set of enforceable control-surface changes.
- Required artifacts: process-audit,research-memo
- Current stage owner: Workflow & Automation Lead
- Current stage role: planner
- Next gate: ready
- Founder escalation: not-needed
- Decision status: none
- Review status: pending
- QA status: not-needed
- UAT status: not-needed
- Acceptance status: pending
- Why it matters: If entropy reduction can pass static gates while users still experience nonstop md/sh churn and consumer audits miss the real runtime, harness loses legibility, credibility, and the ability to compound improvements.
- Decision needed: Adopt an enforceable entropy program centered on real-surface audits, triggered cleanup work, and survivor-state outputs rather than budget-only signaling.
- Deadline: none
- Due review at: none
- Blocked by: none
- Blocks: none
- Current blocker: none
- Next handoff: none
- Linked attachments: .harness/tasks/WI-0009/attachments/2026-03-29-entropy-handling-effectiveness-research-memo.md|research-memo|draft;.harness/tasks/WI-0009/attachments/2026-03-29-entropy-reduction-effectiveness-process-audit.md|process-audit|draft
- Interrupt marker: none
- Resume target: none
- Created at: 2026-03-29
- Updated at: 2026-03-29
- Archived at: none

## Summary

- Problem: the current entropy-reduction posture mostly acts as a static size gate on the harness source surface, but it does not guarantee visible subtractive cleanup, and the consumer-path surface audit currently misroutes back into the source repo instead of auditing the real dogfood runtime.
- Why now: the user reported that recent harness iterations feel like nonstop `md` / `sh` churn with little evidence of pruning, and this audit confirmed both zero-headroom saturation in the source budget and a broken consumer audit path.
- Persistent risk if unfixed: harness can keep passing its own audits while users experience growing coordination drag, stale control surfaces, and low trust that process feedback is actually compounding into a cleaner system.
- Non-goals: replace the local-first runtime with a heavy orchestrator, force subagents into every task, or treat append-only task history as if it were the same problem as active-source entropy.

## Recovery

- Current focus: convert this audit into a small set of enforceable follow-up slices rather than another prose-only complaint.
- Next command: fix consumer surface-diagnostic routing, then decide whether the next slice is survivor-disposition enforcement or zero-headroom compaction triggering.
- Recovery notes: keep source active-surface entropy separate from expected `.harness/tasks/*` append-only history; use subagents only as sidecar auditors or researchers, not as the primary cleanup mechanism.

## Workflow Notes

- Seeded by ./scripts/new_work_item.sh on 2026-03-29.

## Signoff Notes

- Review status starts at pending until the designated reviewer signs off.

## Attachment Notes

- Attach decision, research, review, QA, and output materials under attachments/ as they are created.

## Transition Log

- Created from backlog on 2026-03-29 by ./scripts/new_work_item.sh.

## Notes

- Internal audit highlights:
  - `./scripts/audit_entropy_budget.sh` currently returns `ok` but `saturated`, with total active lines at `26742/26742` and zero line headroom.
  - `./scripts/run_surface_diagnostic.sh --mode source` reports `169` archive markdown snapshots, so subtractive work exists, but it is not coupled strongly enough to new source churn.
  - `./.agents/skills/harness/scripts/run_surface_diagnostic.sh --mode consumer` from this dogfood repo resolves back into the harness source repo because `lib_harness_paths.sh` only detects `source`, which makes the consumer audit path unreliable right where entropy should be observed in real use.
