# Research Memo

- Linked work items: WI-0020


- Date: 2026-03-30
- Owner: Workflow & Automation Lead
- Question: Should harness block acceptance when framework promotion boundary is unclear
- Scope:
  1. verify whether the current dogfood wrapper can honestly accept `WI-0017` when the embedded harness source worktree contains many unrelated pending mutations
  2. compare that situation with current official guidance on repo-local system-of-record design, parallel isolation, and explicit task/dependency carriers
  3. recommend the thinnest valid next move that preserves framework/runtime layering
- Research dispatch: .harness/tasks/WI-0020/attachments/2026-03-30-reviewable-framework-promotion-boundary-external-sensing-research-dispatch.md
- Verification date: 2026-03-30
- Verification mode: mixed
- Freshness level: volatile
- Sources reviewed:
  1. `.harness/tasks/WI-0010/task.md`
  2. `.harness/tasks/WI-0017/task.md`
  3. `git -C ./.agents/skills/harness status --short`
  4. `git -C ./.agents/skills/harness diff --name-only`
  5. `cd ./.agents/skills/harness && ./scripts/validate_source_repo.sh`
  6. `cd ./.agents/skills/harness && ./scripts/audit_entropy_budget.sh`
  7. `STATE_ACTOR=codex ./.agents/skills/harness/scripts/work_item_ctl.sh intake --json shared`
  8. `https://openai.com/index/harness-engineering/`
  9. `https://openai.com/codex/`
  10. `https://docs.github.com/en/issues/tracking-your-work-with-issues/about-issues`
- Conflicting sources:
  1. OpenAI’s harness-engineering posture favors very high throughput and recurring cleanup work, but it couples that with versioned plans, co-located technical debt, and mechanical doc enforcement rather than “review it from a mixed worktree later.”
  2. Codex product guidance encourages parallel worktrees and always-on automations, but those features argue for better isolation of routine lanes, not for approving one review item against many unrelated source changes.
  3. GitHub’s issue hierarchy and dependency model is lightweight, but it does not itself say where a framework should draw its acceptance boundary; that inference comes from combining it with the repo-local system-of-record guidance above.
- Earliest-source check:
  1. 2024, Anthropic’s “Building effective agents” guidance said the best systems start with simple, composable patterns and add complexity only when it demonstrably improves outcomes.
  2. 2026, OpenAI’s harness-engineering writeup sharpened that into repo-local, versioned artifacts plus mechanical cleanup and validation.
  3. 2026, current GitHub docs emphasize explicit sub-issues and blocked-by relationships rather than hidden textual follow-up state.
- Strongest evidence:
  1. Internal sensing shows the current embedded harness source repo has a broad mixed worktree: 29 modified source files plus 9 untracked source files, spanning scripts, docs, contracts, and skill surfaces rather than one bounded review slice.
  2. `validate_source_repo.sh` still fails immediately on `entropy pressure audit failed`, and `audit_entropy_budget.sh` reports dominant pressure on `new-active-files` with `actual 9 | hard 3`, so the source surface is not in a clean review state.
  3. `work_item_ctl.sh intake --json shared` selected `WI-0017` because it is in `review`, but that selection says nothing about whether the underlying framework diff is isolated enough for honest acceptance.
  4. OpenAI’s harness-engineering article says short maps should point to a structured repo system of record, and that active plans, completed plans, and technical debt should be versioned and co-located with mechanical checks.
  5. The OpenAI Codex page says parallel work should run in built-in worktrees and that routine maintenance belongs in automations, reinforcing that mixed background mutations should be isolated instead of silently inherited by a review gate.
  6. GitHub’s official issues docs show that explicit blockers and sub-issues are the thin mainstream carrier for follow-up dependencies, which maps cleanly to a blocker work item for this review-stop condition.
- Strongest counter-evidence:
  1. `WI-0017` already has a bounded objective, fresh external research, and at least one prior targeted validation checkpoint saying the issue-ledger slice passed the intended runtime regression path.
  2. A harder acceptance stop can slow throughput if it fires on every harmless adjacent modification instead of only on genuinely mixed framework slices.
  3. This round did not yet prove the exact long-term mechanism, such as a promotion ledger, diff inventory, or selector change; it only proved the current boundary is too unclear to accept safely.
- Unknowns:
  1. whether the thinnest durable fix is a per-task framework diff inventory, a promotion-bundle ledger, or a selector/acceptance preflight that detects mixed source slices
  2. whether `WI-0010` should eventually absorb the implementation because entropy pressure and review-boundary integrity are coupled in practice
  3. how strict the stop condition should be so it blocks unsafe mixed slices without turning every nearby edit into bureaucracy
- Risks:
  1. over-correcting into a heavy promotion ritual could itself increase source-surface entropy
  2. under-correcting would invite false approvals, where a review item is marked accepted even though the real framework change set was never isolated
  3. if the blocker remains only conversational, the next operator will again have to reconstruct why `WI-0017` could not be accepted
- Recommendation:
  1. block acceptance whenever the framework promotion boundary is unclear enough that the review item no longer maps to a reviewable source slice
  2. materialize that stop condition as an explicit blocker work item and pause the selected review task against it
  3. keep the next implementation slice thin: restore a clean, reviewable boundary first, then return to `WI-0017` acceptance instead of widening into another general process rewrite
