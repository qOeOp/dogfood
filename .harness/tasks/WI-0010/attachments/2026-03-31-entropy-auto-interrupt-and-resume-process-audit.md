# Process Audit

- Linked work items: WI-0010


- Date: 2026-03-31
- Owner: Workflow & Automation Lead
- Scope: why entropy pressure still surfaces a user-visible task-switch decision instead of becoming an automatic interrupt / compaction / resume loop
- Signals reviewed:
  - live user criticism that harness asked whether to switch to entropy work mid-task
  - current `WI-0010` runtime truth and attached checkpoints
  - selector/intake behavior that still prefers unrelated review work over the active entropy lane
  - transition hook implementation and validation coverage
  - fresh official OpenAI notes on background execution and Codex task-queue flow
- Repeated frictions:
  - entropy pressure is represented as `Blocked by`, but not as a first-class interrupted execution state for the task that was in flight
  - selector/intake can still route the operator to an unrelated `review` task while `WI-0010` is the real system-level blocker
  - this makes the operator reconstruct intent in chat and increases the chance of asking the user for a manual choice
- Cross-task handoff failures:
  - accepted pause/resume kernel work (`WI-0012`) and accepted review-acceptance controller work (`WI-0018`) did not compound all the way into entropy handling
  - `WI-0020` added review-boundary stop-the-line behavior, but the more general “dump current task, handle entropy, then come back” path still was not productized
- Candidate root causes:
  - the transition entropy hook only appends `Blocked by` and never upgrades an active task into a paused, resumable interrupt state
  - selector priority is status-first and does not reserve top attention for an unresolved entropy compaction task
  - interrupt taxonomy lacks an entropy-specific marker, so open/resume surfaces cannot express the intended next action cleanly
- Proposed experiments:
  - auto-pause active tasks when the entropy hook creates a new compaction blocker, preserving the requested next status as `Resume target`
  - prioritize unresolved entropy compaction tasks over unrelated review items in selector/open surfaces
  - release the interrupt by deterministic resume behavior instead of treating entropy as a user arbitration point
- Risks of change:
  - auto-resume semantics can be wrong if the preserved resume target or claim metadata are not handled carefully
  - selector priority changes can starve other high-priority review items if the compaction lane is not clearly bounded
- Recommendation:
  - fix this inside `WI-0010`, not as a new broad workflow task
  - make entropy compaction behave like a system interrupt with durable pause/resume semantics and a reserved selector priority
  - treat any future user-facing “should I switch to entropy first?” prompt as a harness regression, not a neutral UX choice
