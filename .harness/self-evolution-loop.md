# Harness Self-Evolution Loop（Task-local）

> 目标：把“发现问题 → 修复链路 → 验证复利”落到当前 runtime 的最小可执行路径。

## 0) 入口与真相边界

- Canonical task truth: `.harness/tasks/<task-id>/task.md`
- 运行恢复顺序：`.harness/README.md` → `task.md` → `task.md` 的 `## Recovery`
- 所有 durable 结论必须回写到 task record 或 task-local 附件

## 1) Discover（发现）

在真实工作流中出现以下任一信号时，进入闭环：

- bootstrap / materialization / recovery 断链
- 并发/锁/状态机导致 task truth 风险
- 审核、验收或恢复步骤出现不可解释漂移

执行要求：

- 先写清“现象 + 最小复现边界”
- 无法继续时，统一按 `harness issue` 记录

## 2) Materialize（立项）

在对应 `task.md` 的 `## Summary` 至少补齐：

- Problem（问题是什么）
- Why now（为什么现在处理）
- Persistent risk（不修会造成什么可持续风险）
- Non-goals（本轮不做什么）

并在元数据中明确：

- Objective / Ready criteria / Done criteria
- 当前 stage owner 与 next gate

## 3) Patch（修复）

修复策略：

- 先修“task truth 正确性”再修“吞吐和体验”
- 优先做 ownership-safe / fail-closed / idempotent 的边界
- 不引入第二套并行 runtime 目录或流程

## 4) Validate（验证）

每次修复必须至少沉淀两类证据：

- 复现证据（问题可被稳定触发）
- 回归证据（修复后同路径不再失真）

证据落点：

- `.harness/tasks/<task-id>/attachments/*.md`（checkpoint / process-audit / review brief 等）
- `task.md` 的 `## Recovery` 记录下一条可执行命令和阻塞信息

## 5) Promote（晋升）

仅当满足下列条件，才晋升回 `harness` source：

- 结论是 framework-generic，不依赖本仓库私有上下文
- 在 dogfood 场景已有明确收益与回归证据
- 不会破坏 wrapper repo “保持薄”原则

否则：

- 改动与事实保持在本仓库 `.harness/` 作为 runtime truth
