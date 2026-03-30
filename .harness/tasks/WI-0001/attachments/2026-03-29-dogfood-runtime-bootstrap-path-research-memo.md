# Research Memo

- Linked work items: WI-0001


- Date: 2026-03-29
- Owner: codex
- Question: What is the highest-leverage bootstrap fix for a fresh dogfood consumer runtime?
- Scope: Minimum-core runtime bootstrap only; exclude shared writeback, task taxonomy expansion, and wrapper-specific convenience layers.
- Research dispatch: n/a
- Verification date: 2026-03-29
- Verification mode: mixed
- Freshness level: volatile
- Sources reviewed: internal repro in this repo; task-local source notes for Anthropic `/init`, MCP roots, and OpenAI background mode
- Conflicting sources: none
- Earliest-source check: current official docs only; no conflicting earlier contract was needed to explain the observed regression
- Strongest evidence: internal repro showed `new_work_item.sh` created a partial `.harness/` and `validate_workspace.sh --mode core` failed immediately because `.harness/README.md` and `.harness/entrypoint.md` were missing
- Strongest counter-evidence: `materialize_runtime_fixture.sh` already knows how to generate the correct minimum-core surface, so the defect is not the target shape but the lack of a safe in-place bootstrap path during real consumer execution
- Unknowns: whether future shared-writeback runtime modes should actively resync bootstrap docs instead of only creating them when missing
- Risks: the lazy bootstrap text now exists in both the fixture script and `lib_state.sh`, so wording can drift unless later centralized
- Recommendation: make missing minimum-core runtime docs a create-if-missing side effect of `ensure_core_runtime_dirs()`, add a regression that bootstraps inside a non-empty consumer repo, and keep the fix strictly inside the framework source boundary
