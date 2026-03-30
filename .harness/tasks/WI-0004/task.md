# Work Item

- Schema version: 2
- State authority: script-only
- State version: 18
- Last operation ID: WI-0004-to-archived
- Last transition event: .harness/tasks/WI-0004/history/transitions/TX-20260329T221458-WI-0004-done-to-archived.md
- ID: WI-0004
- Title: Playwright browser profile conflict
- Type: control
- Status: archived
- Priority: high
- Owner: codex
- Sponsor: general-manager
- Assignee: none
- Worktree: none
- Claimed at: none
- Claim expires at: none
- Lease version: 2
- Objective: Add a framework-generic Playwright preflight/repair path so shared persistent browser-profile lock conflicts become a handled runtime condition instead of blank tabs plus silent tool failure.
- Ready criteria: Confirm the persistent profile conflict as the current failure mode, choose one bounded intervention point, and keep the fix inside harness source rather than wrapper-specific workaround.
- Done criteria: The Playwright path either preflights and reports profile-lock conflicts with actionable recovery or repairs the runtime path safely, and source/runtime validation covers the chosen behavior.
- Required artifacts: none
- Current stage owner: codex
- Current stage role: archive
- Next gate: none
- Founder escalation: not-needed
- Decision status: approved
- Review status: approved
- QA status: not-needed
- UAT status: not-needed
- Acceptance status: approved
- Why it matters: If Playwright fails by opening blank tabs and exiting, dogfood rounds under-cover UI/runtime surfaces and still need manual interpretation to understand what failed.
- Decision needed: Adopt Playwright browser-profile preflight or equivalent safe repair as the next bounded self-evolution slice.
- Deadline: none
- Due review at: none
- Blocked by: none
- Blocks: none
- Current blocker: none
- Next handoff: none
- Linked attachments: .harness/tasks/WI-0004/attachments/sources/2026-03-29-playwright-persistent-user-data-dir-warning.md|source-note|approved;.harness/tasks/WI-0004/attachments/sources/2026-03-29-chrome-remote-debugging-non-standard-user-data-dir-requirement.md|source-note|approved;.harness/tasks/WI-0004/attachments/2026-03-29-playwright-profile-conflict-reproduction.md|reproduction-note|approved;.harness/tasks/WI-0004/closure/2026-03-29-playwright-profile-preflight-acceptance-review-brief.md|acceptance-review-brief|approved;.harness/tasks/WI-0004/attachments/2026-03-29-playwright-profile-preflight-acceptance-closeout-checkpoint.md|checkpoint|approved
- Interrupt marker: none
- Resume target: none
- Created at: 2026-03-29
- Updated at: 2026-03-29
- Archived at: 2026-03-29T22:14:58+0800

## Summary

- Problem: the current Playwright MCP path can open blank tabs and exit when its shared persistent Chrome profile is locked, but that failure still lacks a dedicated preflight/repair control surface inside harness.
- Why now: `WI-0002` and `WI-0003` already proved that skipped failures and incomplete lifecycle coverage must become task truth immediately, so the next highest-leverage unresolved issue is the still-unhandled Playwright profile conflict.
- Persistent risk if unfixed: future dogfood rounds will continue under-covering UI automation while operators manually infer that the true cause was a persistent browser-profile collision rather than a product/runtime bug.
- Non-goals: redesign all browser automation, force-kill user browser sessions blindly, or broaden this task into generic UI testing strategy.

## Recovery
- Current focus: Closed after accepted Playwright persistent-profile preflight slice.
- Next command: none
- Recovery notes: If reopened, start from the reproduction note plus the two approved source notes, rerun `./scripts/research/runtime_status.sh` and `./scripts/run_state_validation_slice.sh`, and only escalate to stronger repair automation if preflight+writeback proves insufficient. The next gating item in the runtime is currently `WI-0006` in review.
## Workflow Notes

- Seeded by ./scripts/new_work_item.sh on 2026-03-29.

## Signoff Notes

- Review status starts at pending until the designated reviewer signs off.

## Attachment Notes

- Attach decision, research, review, QA, and output materials under attachments/ as they are created.

## Transition Log

- Created from backlog on 2026-03-29 by ./scripts/new_work_item.sh.

## Notes

- none
