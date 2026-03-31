# Process Audit

- Linked work items: WI-0020



- Date: 2026-03-30
- Owner: codex
- Scope: why the selected `WI-0017` review lane should stop and become an explicit blocker task instead of forcing acceptance from a mixed embedded harness source worktree
- Signals reviewed:
  - `STATE_ACTOR=codex ./.agents/skills/harness/scripts/work_item_ctl.sh intake --json shared`
  - `STATE_ACTOR=codex ./.agents/skills/harness/scripts/query_work_items.sh --json`
  - `git -C ./.agents/skills/harness status --short`
  - `git -C ./.agents/skills/harness diff --name-only`
  - `cd ./.agents/skills/harness && ./scripts/validate_source_repo.sh`
  - `cd ./.agents/skills/harness && ./scripts/audit_entropy_budget.sh`
  - `.harness/tasks/WI-0010/task.md`
  - `.harness/tasks/WI-0017/task.md`
  - OpenAI, `Harness engineering: leveraging Codex in an agent-first world` (verified 2026-03-30)
  - OpenAI, `Codex` product page (verified 2026-03-30)
  - GitHub Docs, `About issues` (verified 2026-03-30)
- Repeated frictions:
  - intake keeps surfacing a `review` item even when the underlying framework diff is no longer a clean reviewable slice
  - source validation continues to stop on entropy pressure, so downstream review repeatedly inherits an already-breached source surface
  - the dogfood wrapper now has multiple accepted or review-stage ideas reflected in one dirty embedded harness worktree, which forces human archaeology before any honest gate decision
- Cross-task handoff failures:
  - `WI-0017` correctly moved the issue-ledger slice to review, but the surrounding source repo never returned to a boundary where that slice could be accepted on its own merits
  - `WI-0010` identified entropy effectiveness and subtractive cleanup as a live lane, yet the selector still steers attention to `WI-0017` because status outranks review-boundary integrity
  - earlier compounding fixes improved writeback semantics, but they did not yet create a thin carrier for “this review item cannot be accepted until the framework diff is isolated again”
- Candidate root causes:
  - acceptance currently assumes a selected review item still maps to a reviewable source slice
  - entropy controls detect source growth, but they do not automatically re-establish per-task promotion boundaries once several framework slices accumulate locally
  - selector priority is status-first, so `review` can outrank `in-progress` cleanup even when the review lane is no longer trustworthy
- Proposed experiments:
  - make review-boundary collapse a first-class blocker task instead of a chat-only observation
  - pause `WI-0017` with an explicit blocked-by relationship to `WI-0020`
  - in `WI-0020`, test the thinnest mechanism that can re-establish clean acceptance boundaries, such as a promotion bundle inventory or an acceptance preflight for mixed framework diffs
- Risks of change:
  - if the boundary check is too blunt, it will create false pauses and slow harmless work
  - if the fix becomes a broad release-management layer, the wrapper will grow a second harness instead of staying thin
  - if no durable blocker is written, the same review-stop reasoning will be rediscovered and re-argued next run
- Recommendation:
  - stop the `WI-0017` acceptance lane now
  - treat reviewable framework promotion boundary as the single highest-leverage blocker
  - keep the next slice narrowly focused on restoring honest acceptance, not on merging every open entropy concern into one mega-task
