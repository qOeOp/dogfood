# Process Audit

- Linked work items: WI-0008

- Date: 2026-03-29
- Owner: codex
- Scope: `WI-0008` compounding target semantics in harness canonical instructions
- Signals reviewed: user correction in the dogfood thread; current `WI-0008` task truth; `SKILL.md`; `docs/workflows/process-compounding-cadence.md`; `scripts/validate_source_repo.sh`
- Repeated frictions: the framework first over-triggered self-compounding, then overcorrected into a harness-only boundary, because the rule was keyed to repo type instead of the current work object
- Cross-task handoff failures: `WI-0005` fixed the immediate trigger, `WI-0007` narrowed scope, but neither encoded the more general target-selection rule the user expected
- Candidate root causes: compounding semantics were framed around harness identity instead of the active thing being improved; validator wording anchored that narrower framing once it landed
- Proposed experiments: bind "current work object" into canonical instruction + cadence + validator; keep dogfood-specific harness targeting explicit only as the active work object for this round, not as a universal default
- Risks of change: ambiguous user feedback can still require judgment if the active work object is unclear; stronger typed routing may still be worth exploring if this ambiguity recurs
- Recommendation: accept work-object-relative compounding as the default semantics, then resume `WI-0004` once source/runtime validation passes
