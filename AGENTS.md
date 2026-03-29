# Dogfood

当前仓库是 `harness` 的 dogfood consumer runtime。

规则：

1. 用户需求默认先命中 `harness`。
2. 若当前工作需要 durable runtime，而 `.harness/` 尚不存在，`harness` 应先自动 bootstrap 最小 runtime，再继续同一轮任务。
3. 若只是一次性问答或短分析，可保持 ephemeral，不必创建 `.harness/`。
4. 一旦 `.harness/` 已存在，后续默认以 `.harness/README.md`、`.harness/entrypoint.md`、当前 `task.md`、`## Recovery` 为 canonical 读序。
5. 不要求用户知道底层脚本名；若必须人工直接调用底层脚本才能继续，默认记为 `harness issue`。
6. 只有 framework-generic 的改动才允许晋升回 `./.agents/skills/harness/`。
7. dogfood runtime truth 留在本 repo，不回灌到 harness source repo。
8. wrapper repo 必须保持薄，不要在根部再长出第二套大型 `scripts/`、`docs/`、`contracts/`、`roles/`。
