# codex-turbo

让 Codex CLI 用得更快、更稳、更可复用。

> 当前项目适配版本：**Codex CLI v0.104.0**

核心要点

- `multi_agent = true` 的并行工作流
- 可复制的 `AGENTS.md` 协作模板
- 可落地的 `config.toml` 示例与风险说明

## 为什么做这个仓库

原帖信息`https://linux.do/t/topic/1603762`，但偏“长文流”，此次优化为：

- 按主题查阅（上手 / 配置 / FAQ / 模板）
- 按团队二次定制（模板直接复制改）
- 持续迭代（PR/Issue 留痕）

## 目录结构

```text
.
├── README.md
├── docs
│   └── faq.md
└── templates
    ├── AGENTS.template.md
    └── config.toml.example
```

## 快速上手（5 分钟）

目标：把你的 Codex CLI 切到“并行 + 模板化”工作模式。

### 1. 克隆仓库

```bash
git clone <your-repo-url>
cd codex-turbo
```

### 2. 准备

- 确保 Codex CLI 版本为 `v0.104.0`（本文档按该版本适配）
- 本地有 `~/.codex/` 目录

### 3. 启用多代理

在 Codex CLI 内执行：

1. 进入 `/experimental`
2. 勾选 `Multi-agents`

然后检查 `~/.codex/config.toml` 是否包含：

```toml
[features]
multi_agent = true
```

> 如果没有这段，可以手动补上。

### 4. 放置模板

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

### 5. 最小验证

用一个 20~30 分钟的小任务测试：

- 任务可拆成 2~3 个独立子任务
- 子任务无写冲突
- 最后统一汇总结果

验证标准：

- 并行任务确实同时执行
- 输出质量可控，不是“快但乱”
- token 成本在你的预算范围内

### 6. 推荐迭代节奏

1. 先抄模板直接跑
2. 跑完一轮再裁剪规则
3. 每周复盘一次 AGENTS 文档

做到这三步，基本就进入正循环了。

### 7. 推荐最小配置（已合并）

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

## 文档导航

- `README.md`：快速上手（本页）
- `docs/faq.md`：常见坑与排查
- `templates/AGENTS.template.md`：开箱可改模板
- `templates/config.toml.example`：参考配置

## 适用范围提醒

- 个人项目：可激进，迭代快
- 团队/公司项目：以团队规范、发布流程、兼容策略为准

特别是“修改功能不保留旧兼容代码”这条：

- 对可控项目是提效利器
- 对企业项目必须评估影响并走评审流程

## 免责声明

本仓库是方法论与模板参考，当前按 Codex CLI v0.104.0 验证。
