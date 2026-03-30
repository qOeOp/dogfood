# Research Memo

- Linked work items: WI-0009
- Date: 2026-03-29
- Owner: Workflow & Automation Lead
- Question: entropy-handling-effectiveness
- Scope:
  1. audit the current harness entropy controls in the dogfood repo rather than assuming the source docs describe reality
  2. compare the current posture with recent official guidance from OpenAI, Anthropic, LangGraph, and Microsoft on context management, cleanup cadence, subagents, and memory separation
  3. converge on the minimum practical improvement plan for this harness
- Research dispatch: n/a
- Verification date: 2026-03-29
- Verification mode: mixed
- Freshness level: volatile
- Sources reviewed:
  1. `/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/README.md`
  2. `/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/docs/workflows/surface-audit.md`
  3. `/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/docs/workflows/process-compounding-cadence.md`
  4. `/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/scripts/audit_entropy_budget.sh`
  5. `/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/scripts/run_surface_diagnostic.sh`
  6. `/Users/vx/WebstormProjects/dogfood/.agents/skills/harness/scripts/lib_harness_paths.sh`
  7. `/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0005/task.md`
  8. `/Users/vx/WebstormProjects/dogfood/.harness/tasks/WI-0007/task.md`
  9. `https://openai.com/index/harness-engineering/`
  10. `https://cdn.openai.com/pdf/6a2631dc-783e-479b-b1a4-af0cfbd38630/how-openai-uses-codex.pdf`
  11. `https://www.anthropic.com/engineering/building-effective-agents`
  12. `https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents`
  13. `https://code.claude.com/docs/en/sub-agents`
  14. `https://docs.langchain.com/oss/python/langgraph/memory`
  15. `https://learn.microsoft.com/en-us/semantic-kernel/frameworks/agent/agent-memory`
- Conflicting sources:
  1. OpenAI’s 2026 harness guidance favors recurring background cleanup tasks and mechanical repo checks, while Anthropic continues to warn against unnecessary framework complexity; the synthesis is not “more machinery,” but “small mechanical controllers with tight scopes.”
  2. Claude Code subagents are valuable for context isolation and constrained delegation, but neither Anthropic nor OpenAI present subagents as the primary answer to repository entropy; cleanup still depends on explicit audits, tool design, and recurring enforcement.
  3. Internal harness docs describe weekly surface audits and audit-the-auditors loops, but the current dogfood runtime does not show durable surface-audit artifacts and the consumer audit entrypoint is presently unreliable.
- Earliest-source check:
  1. 2024, Anthropic advised that the most successful agent systems use simple, composable patterns rather than complex frameworks.
  2. 2025, Anthropic emphasized minimal-overlap toolsets and tight context as a prerequisite for reliable long-running agent behavior.
  3. 2026, OpenAI described repo knowledge as the system of record, short `AGENTS.md` maps, recurring doc-gardening agents, and background cleanup tasks as necessary to control entropy.
- Strongest evidence:
  1. Current internal audit shows the source entropy budget is not comfortably healthy; it is saturated. `audit_entropy_budget.sh` reports `26742/26742` active lines with zero line headroom, which means the system is frozen at the ceiling rather than actively reducing surface.
  2. Current internal audit also shows a real control-path bug: running `./.agents/skills/harness/scripts/run_surface_diagnostic.sh --mode consumer` from this dogfood repo reports source-repo warnings and zero runtime tasks, because `lib_harness_paths.sh` only resolves `source`. This makes the consumer entropy loop unreliable.
  3. OpenAI’s harness-engineering writeup says a giant instruction file fails because it crowds out relevant context, rots quickly, and is hard to verify; they instead keep a short map plus structured docs, enforce those docs mechanically, and run a recurring doc-gardening agent that opens cleanup PRs.
  4. OpenAI’s “How OpenAI uses Codex” memo describes using Codex for code cleanup, follow-up tasks, and a lightweight backlog, which supports treating cleanup as ongoing queued work instead of a rare retrospective.
  5. Anthropic’s “Building effective agents” argues for simple, composable patterns first, with workflows, routing, parallelization, and evaluator loops added only when they demonstrably improve outcomes.
  6. Anthropic’s context-engineering guidance says bloated tool sets and laundry-list context create ambiguous decisions and worse maintenance; this supports reducing surfaces and tightening selection instead of merely adding more rules.
  7. Claude Code’s subagent docs position subagents as isolated context windows with specific tool access and permissions, helpful for preserving context and running parallel research, but not as a substitute for repository cleanup policy.
  8. LangGraph and Semantic Kernel both separate thread-scoped short-term state from long-term memory or whiteboard memory, reinforcing that append-only task history and active-source working surfaces must be managed as different layers.
- Strongest counter-evidence:
  1. The current harness is not doing nothing. The source diagnostic reports `169` archive markdown snapshots, there are multiple redirect stubs, and several recent commits reduce or rename surfaces instead of only adding them.
  2. Some recent budget revisions actually lowered ceilings instead of only inflating them, which shows at least partial subtractive intent rather than pure goalpost moving.
  3. Durable `.harness/tasks/*` growth is expected append-only runtime truth and should not be mistaken for active-source entropy by default.
- Unknowns:
  1. whether the best first fix after the routing bug is a mandatory survivor-disposition artifact, a zero-headroom compaction trigger, or a churn-aware budget extension
  2. whether recurring entropy work should materialize as explicit work items, background tasks, or closeout obligations on source-surface changes
  3. how much of the survivor decision should be encoded in a typed contract versus a lightweight markdown artifact
- Risks:
  1. if harness keeps optimizing for “budget passes” instead of “surface gets smaller or clearer,” it will reward churn that rewrites text without materially reducing working-set complexity
  2. if consumer audits do not inspect the real consumer runtime, the dogfood loop cannot prove whether entropy controls work where users actually feel the pain
  3. if subagents are treated as the missing magic, harness may add orchestration complexity without fixing ownership, routing, or cleanup obligations
  4. if zero-headroom saturation is allowed to pass without triggered cleanup work, the repo will keep operating in a brittle state where every new change must borrow space from something else informally
- Recommendation:
  1. keep the current entropy budget and archive split, but reclassify them as a first-layer freeze gate rather than a sufficient entropy program
  2. fix consumer diagnostic routing immediately so dogfood can audit the actual `.harness/` runtime
  3. require a diff-scoped survivor-disposition output for source changes touching docs, scripts, roles, skills, or contracts when headroom is zero or near zero
  4. turn zero-headroom saturation into a triggered compaction workflow, not just a passing status line
  5. add churn-aware metrics to the entropy audit so repeated rewrite volume becomes visible alongside file and line ceilings
  6. use subagents only as bounded sidecars for research or candidate generation after the control path above exists
