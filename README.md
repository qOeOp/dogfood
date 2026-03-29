# dogfood

`dogfood` 是 `harness` 的 consumer runtime wrapper。

它的职责只有三件事：

1. 承载真实的 `.harness/` runtime truth
2. 用真实需求 dogfood `harness` 的 operator flow
3. 把被验证为 framework-generic 的改进晋升回 `harness`

默认规则：

1. `harness` source 通过 `./.agents/skills/harness/` 引入
2. `.harness/` 不预置；第一次 `runtime-required` 的真实任务应触发自动 bootstrap
3. 若自动 bootstrap / task materialization / recovery 断链，默认记为 `harness issue`
