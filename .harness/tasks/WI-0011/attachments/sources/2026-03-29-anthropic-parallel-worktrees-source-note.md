# Source Note

- Linked work items: WI-0011


- Work Item: WI-0011
- Date: 2026-03-29
- Source: [Anthropic Claude Code Docs - Common workflows](https://code.claude.com/docs/en/tutorials)
- Captured at: 2026-03-29
- Freshness window: 30 days
- Claim area: parallel task execution and worktree isolation

## Claim

- Anthropic's official Claude Code workflow docs treat parallel sessions with isolated Git worktrees, plus subagent worktrees, as a normal operating mode for working on multiple tasks at once.

## Evidence

- The docs include a dedicated section on running parallel sessions with Git worktrees and explain that separate working directories prevent changes from colliding.
- The same page also says subagents can use worktree isolation to work in parallel without conflicts.

## Relevance

- This supports the judgment that harness should not imply a global single-active-task model at the shared selector/start surface.
- If harness chooses one top open item and turns an unrelated `review` item into a global start blocker, that is a control-surface mismatch rather than a necessary concurrency rule.

## Limits

- This source establishes that parallel task/worktree execution is a valid workflow pattern.
- It does not by itself specify the exact selector or claim semantics harness should adopt.
