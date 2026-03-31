# Research Memo

- Linked work items: WI-0010


- Date: 2026-03-31
- Owner: Workflow & Automation Lead
- Question: should WI-0010 stop adjacent support slices until entropy pressure visibly drops
- Scope:
  1. determine whether the active `WI-0010` problem is still "pick another nearby support slice" or has shifted to "prove the compaction lane visibly lowers pressure"
  2. compare the current dogfood signals with official guidance on reviewable diffs, thin blocker decomposition, and explicit long-running control state
  3. recommend the thinnest next move that preserves framework/runtime layering and does not widen the mixed source boundary
- Research dispatch: n/a
- Verification date: 2026-03-31
- Verification mode: mixed
- Freshness level: volatile
- Sources reviewed:
  1. `.harness/tasks/WI-0010/task.md`
  2. `.harness/tasks/WI-0010/attachments/2026-03-30-selector-json-builder-compaction-checkpoint.md`
  3. `.harness/tasks/WI-0010/attachments/2026-03-31-query-work-items-helper-compaction-process-audit.md`
  4. `.harness/tasks/WI-0010/attachments/2026-03-31-open-work-item-helper-compaction-process-audit.md`
  5. `.harness/tasks/WI-0018/closure/2026-03-30-review-acceptance-controller-acceptance-review-brief.md`
  6. `.harness/tasks/WI-0019/closure/2026-03-30-ownership-safe-mutation-lock-acceptance-review-brief.md`
  7. `cd /Users/vx/WebstormProjects/dogfood/.agents/skills/harness && ./scripts/audit_entropy_budget.sh`
  8. `cd /Users/vx/WebstormProjects/dogfood/.agents/skills/harness && git diff --stat`
  9. `https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests?platform=mac`
  10. `https://docs.github.com/en/issues/tracking-your-work-with-issues/using-issues/browsing-sub-issues`
  11. `https://developers.openai.com/api/docs/guides/background`
- Conflicting sources:
  1. GitHub's pull-request docs explain what a reviewable change set is, but they do not define a numeric threshold for when a system must split the slice.
  2. OpenAI's background-mode docs support explicit long-running lanes, but they do not themselves decide which hotspot file should go first.
  3. Internal task truth shows recent support slices were real and validated, so the conclusion here is not "those slices were useless"; it is "they no longer count as sufficient progress on the active entropy problem."
- Earliest-source check:
  1. 2026-03-30, `WI-0010` checkpointed `pending-active-files=28` and `new-active-files=3`, already warning that one local compaction win would not prove the loop effective.
  2. 2026-03-31 earlier in the task, the `query_work_items.sh` audit recorded `pending-active-files=47` and `new-active-files=9`, showing pressure worsened instead of improving.
  3. 2026-03-31 current GitHub and OpenAI docs still emphasize bounded review surfaces, explicit decomposition, and explicit async state instead of mixed, implicit continuation.
- Strongest evidence:
  1. The current source audit fails in `compaction-only` with dominant pressure on `pending-active-files` at `49/16`, `new-active-files` at `9/3`, and a hotspot on `scripts/validate_source_repo.sh` with `16/10` recent touches.
  2. The embedded harness source worktree is still broadly mixed at `41 files changed, 4516 insertions(+), 1149 deletions(-)`, so the problem is not lack of activity but lack of visible entropy reduction.
  3. `WI-0018` and `WI-0019` improved control correctness, yet their own review artifacts still called out unrelated entropy blockers and broader repo noise.
  4. GitHub's pull-request model centers review on the actual proposed diff, and draft semantics exist for work that is visible but not yet honestly reviewable.
  5. GitHub's sub-issue model supports breaking larger work into smaller explicit units, which maps cleanly to carving one hotspot slice instead of continuing mixed support edits.
  6. OpenAI's background-mode docs reinforce that long-running lanes should expose explicit state until they reach a real terminal boundary.
- Strongest counter-evidence:
  1. The single-active-checkpoint discipline is a real framework improvement and did reduce one class of recovery noise.
  2. Some adjacent support slices, such as acceptance guarding and mutation-lock hardening, were necessary to prevent false progress and silent corruption.
  3. A hotspot slice around `scripts/validate_source_repo.sh` is inferred from current metrics, but this run did not prove it is the only valid next candidate.
- Unknowns:
  1. whether the next subtractive slice should be only `scripts/validate_source_repo.sh` or a tiny coupled pair with one immediately adjacent validation surface
  2. what exact before/after threshold should count as "visible drop" for `WI-0010`
  3. whether a future explicit budget raise will still be needed after the dominant hotspot is cleaned up
- Risks:
  1. freezing adjacent support slices can delay useful ergonomics work if the hotspot is chosen poorly
  2. if the next hotspot slice adds surface instead of deleting or consolidating it, the compaction-only lane will intensify the same failure while claiming discipline
  3. if `WI-0020` or `WI-0017` resumes before `WI-0010` shows visible pressure decline or an explicit budget decision, harness will recreate the same mixed review-boundary problem
- Recommendation:
  1. treat "accepted support slices are not lowering dominant entropy pressure" as the current highest-leverage `WI-0010` problem
  2. stop adjacent support-slice expansion under `WI-0010` until the next slice either lowers the dominant pressure or writes an explicit budget-raise rationale
  3. make the next reviewable source slice target the current hotspot around `scripts/validate_source_repo.sh`, record before/after metrics in the checkpoint, and keep `WI-0020` plus `WI-0017` blocked until that happens
