# 快速上手（5 分钟）

目标：把你的 Codex CLI 切到“并行 + 模板化”工作模式。

## 1. 准备

- 确保 Codex CLI 版本为 `v0.104.0`（本文档按该版本适配）
- 本地有 `~/.codex/` 目录

## 2. 启用多代理

在 Codex CLI 内执行：

1. 进入 `/experimental`
2. 勾选 `Multi-agents`

然后检查 `~/.codex/config.toml` 是否包含：

```toml
[features]
multi_agent = true
```

> 如果没有这段，可以手动补上。

## 3. 放置模板

把本仓库模板放到你的用户目录。你可以按场景二选一：

1. 首次使用（直接复制）

```bash
cp templates/AGENTS.template.md ~/.codex/AGENTS.md
cp templates/config.toml.example ~/.codex/config.toml
```

2. 已有本地配置（建议手动合并，不直接覆盖）

```bash
cp templates/AGENTS.template.md ~/.codex/AGENTS.template.md
cp templates/config.toml.example ~/.codex/config.toml.template
```

然后自行对比并合并关键差异（按你习惯用 diff 或编辑器 merge）。

## 4. 最小验证

用一个 20~30 分钟的小任务测试：

- 任务可拆成 2~3 个独立子任务
- 子任务无写冲突
- 最后统一汇总结果

验证标准：

- 并行任务确实同时执行
- 输出质量可控，不是“快但乱”
- token 成本在你的预算范围内

## 5. 推荐迭代节奏

1. 先抄模板直接跑
2. 跑完一轮再裁剪规则
3. 每周复盘一次 AGENTS 文档

做到这三步，基本就进入正循环了。

## 6. 推荐最小配置（已合并）

下面这份 `~/.codex/config.toml` 最小配置，够你先稳定跑起来：

```toml
model_provider = "cch"
model = "gpt-5.3-codex"
model_reasoning_effort = "xhigh"
sandbox_mode = "workspace-write"

personality = "pragmatic"
web_search = "live"
network_access = true
disable_response_storage = true

[features]
multi_agent = true
```

关键参数速记：

- `multi_agent = true`：多代理总开关（最重要）
- `model_reasoning_effort`：推理深度，越高通常越贵
- `sandbox_mode`：建议先用 `workspace-write`，兼顾安全和效率
- `web_search = "live"`：需要实时信息时更有用

> 说明：本文档按 Codex CLI `v0.104.0` 适配；不同版本或供应商字段名可能有差异，请以你本地 CLI 支持为准。
