# dogfood

`dogfood` 是 `harness` 的 consumer runtime wrapper。

它的职责只有三件事：

1. 承载真实的 `.harness/` runtime truth
2. 用真实需求 dogfood `harness` 的 operator flow
3. 把被验证为 framework-generic 的改进晋升回 `harness`

## 自进化最小闭环（已接入当前 harness 运行方式）

为避免“只记录问题、不形成复利”，本仓库把 dogfood 过程固定为 5 步闭环，并直接复用现有 `.harness/tasks/<task-id>/task.md` 结构，不新增平行系统：

1. **发现（Discover）**：在真实需求执行中识别断链/退化/异常，并按 `harness issue` 归因到具体链路。
2. **立项（Materialize）**：创建或更新一个 work item，在 `## Summary` 明确问题、风险、非目标。
3. **修复（Patch）**：在最小边界内修复链路问题，优先保障 task truth 与 recovery 的一致性。
4. **验证（Validate）**：将复现与回归验证结果沉淀为 task-local 附件，并更新 `## Recovery` 的下一步。
5. **晋升（Promote）**：仅当改动被证明是 framework-generic 时，才晋升回 `harness` source；否则保留在 dogfood runtime truth。

该闭环的执行与恢复入口见 `.harness/self-evolution-loop.md`。

默认规则：

1. `harness` source 通过 `./.agents/skills/harness/` 引入
2. `.harness/` 不预置；第一次 `runtime-required` 的真实任务应触发自动 bootstrap
3. 若自动 bootstrap / task materialization / recovery 断链，默认记为 `harness issue`
