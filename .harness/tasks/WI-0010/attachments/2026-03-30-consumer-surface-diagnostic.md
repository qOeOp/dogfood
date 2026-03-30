# Surface Diagnostic

- Linked work items: WI-0010

- Date: 2026-03-30
- Mode: consumer
- Scope: harness-owned runtime docs, workspace baseline, state system, optional brief layer
- Canonical capability surface: `.harness/`

## Baseline Checks

- `validate_workspace`: pass | workspace baseline (core): ok
- `audit_document_system`: pass | document system audit: ok
- `audit_doc_style`: pass | doc style audit: ok
- `audit_role_schema`: skip | minimum-core runtime does not materialize a consumer role directory by default
- `audit_state_system`: pass | state system audit: ok
- `validate_freshness_gate`: fail | freshness gate failed: .harness/tasks/WI-0001/attachments/2026-03-29-dogfood-runtime-bootstrap-path-research-memo.md is 'mixed' but 'Research dispatch' does not reference a dispatch artifact freshness gate failed: .harness/tasks/WI-0001/attachments/2026-03-29-dogfood-runtime-bootstrap-path-research-memo.md is 'mixed' but 'Sources reviewed' has no URL or source-note reference freshness gate failed: .harness/tasks/WI-0009/attachments/2026-03-29-entropy-handling-effectiveness-research-memo.md is 'mixed' but 'Research dispatch' does not reference a dispatch artifact

## Capability Inventory

- Active tasks: 9
- Archived-status tasks: 9
- Task records with Recovery: 18
- Transition events: 199
- Shared workspace directories: 0

## Brief Layer Snapshot

- Brief registry status: not materialized
- Reason: minimum-core runtime does not include the shared brief workspace by default

## Usage Notes

1. consumer 模式只评估 harness-owned runtime surface，不评估 provider adapters 或 skill install location。
2. minimum-core runtime 默认先把 consumer surface audit 写回当前 task；可运行：
   `STATE_ACTOR=<actor> ./.agents/skills/harness/scripts/run_surface_diagnostic.sh --mode consumer --work-item <WI-xxxx>`
3. 只有显式启用 shared writeback 后，才应该改用 `.harness/workspace/status/process-audits/` 这类跨任务路径。
4. 若要在 source surface 达到软阈值或硬阈值时自动 create/reuse 减熵 task，可运行：
   `./.agents/skills/harness/scripts/sync_entropy_compaction_task.sh`
5. 若要审计 framework source repo，请在 source repo 运行：
   `./scripts/run_surface_diagnostic.sh --mode source`
