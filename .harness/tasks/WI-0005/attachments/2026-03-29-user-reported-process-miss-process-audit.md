# Process Audit

- Linked work items: WI-0005


- Date: 2026-03-29
- Owner: codex
- Scope: audit why a live user-reported harness workflow miss did not automatically become compounding work during this dogfood self-evolution run
- Signals reviewed:
  - the accepted closure path for `WI-0002` and `WI-0003`
  - the follow-up creation of `WI-0004` after the Playwright issue was discussed
  - the user's explicit correction that the framework should have fixed the compounding workflow itself, not only the surfaced issue
  - current harness skill instructions and process-compounding workflow docs
- Repeated frictions:
  - a user had to point out that a workflow miss was being handled as a one-off conversational correction rather than a framework compounding trigger
  - the system successfully opened a follow-up task for the surfaced symptom, but not for the meta-failure in harness process semantics
  - compounding behavior remained more implied than mandatory at the exact moment it should have become default
- Cross-task handoff failures:
  - `WI-0004` was opened as the next issue, but it took another user intervention to redirect attention to the higher-priority framework-process defect
  - the intended handoff from "user feedback" to "process-audit plus framework follow-up" had no enforced trigger, so operator judgment drifted toward symptom repair
- Candidate root causes:
  - current canonical instructions describe post-acceptance compounding and weekly process audit cadence, but they do not explicitly state that a user-reported harness/process miss triggers immediate compounding writeback in the current run
  - source validation did not bind that trigger rule to any required instruction text, so the behavior could regress silently
  - the framework had a closure-oriented compounding loop, but not a clear mid-run correction loop for process/control-surface misses discovered by the user
- Proposed experiments:
  - make the root harness skill explicitly require immediate task truth plus process-audit escalation when the user reports a harness/process/control-surface miss
  - update process-compounding cadence so user-reported process misses are immediate triggers rather than weekly-only inputs
  - bind both rules into `validate_source_repo.sh` so the trigger cannot disappear without failing source validation
- Risks of change:
  - over-triggering process audits for trivial style comments could create noise if the rule is phrased too broadly
  - if the rule is limited only to accepted-task closeout, the same failure will recur during active execution
  - if the rule is too vague, agents will keep rationalizing away the trigger as optional judgment
- Recommendation: treat user-reported harness/process/control-surface misses as a P0 compounding trigger that must immediately create or update task truth plus a process-audit artifact before symptom-level continuation
