# Process Audit

- Linked work items: WI-0015

- Date: 2026-03-30
- Owner: Workflow & Automation Lead
- Scope: dogfood first-turn harness intake and task materialization
- Signals reviewed: user report about installed harness skill not auto-loading; dogfood `AGENTS.md`; harness `SKILL.md`; harness README bootstrap/runtime guidance; current validation slices starting from explicit script invocation
- Repeated frictions: the repo already had harness installed and `.harness/` materialized, but a new durable harness request still proceeded without first selecting or creating a work item
- Cross-task handoff failures: platform skill activation -> repo-level harness routing -> harness intake -> task materialization currently has no deterministic first-hop owner
- Candidate root causes: installed skill presence is treated like auto-entry but current behavior is still heuristic; harness `SKILL.md` did not explicitly require first-turn task selection/materialization; validation starts after explicit `scripts/*` entrypoints rather than at user-request intake
- Proposed experiments: tighten dogfood `AGENTS.md` and harness `SKILL.md` so the first durable turn must hit harness intake; add a validation slice for first durable request -> selected/created work item; if misses persist, add one thin high-level intake controller instead of more prose
- Risks of change: over-eager task creation for ephemeral asks; duplicating product-router behavior inside the repo; adding one more script surface without deleting an older one
- Recommendation: treat platform auto-load as best-effort only, and make repo-level instructions own a deterministic first-hop intake contract; keep the next implementation slice focused on verification plus one thin intake surface, not a broader workflow redesign
