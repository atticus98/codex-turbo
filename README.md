# codex-turbo

抛砖引玉，让 Codex CLI 用得更快、更稳、更可复用。

> 当前项目适配版本：**Codex CLI v0.114.0**

## 核心要点

- 💡 **并行工作流**：`multi_agent = true` 最大并行度与最小阻塞设计
- 🔧 **系统级契约**：在 `config.toml` 中通过 `developer_instructions` 注入 Agent 并行工作规范，优先级高于 `AGENTS.md`
- 🧠 **原生记忆**：`memories = true` 自动提取和归并对话记忆，提升上下文连贯性
- 🔌 **WebSocket 支持**：`responses_websockets_v2 = true` 启用实时流式响应，不支持自动回退
- 🎯 **对话风格**：强视觉边界、emoji 编号、直而短句的终端输出规范
- 📝 **标准契约**：子代理任务下发的清晰指令模板（名称/目标/动作/结果）
- ⚙️ **并发控制**：`max_threads = 5` 保守限制单轮最大子任务数
- ⚠️ **风险管控**：危险操作确认机制与不可变原则
- 📋 **可复制模板**：开箱即用的 `AGENTS.template.md` 与 `config.toml.example`

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

- 确保 Codex CLI 版本为 `v0.114.0`（本文档按该版本适配）
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

### 4. 启用原生记忆功能


检查 `~/.codex/config.toml` 是否包含：

```toml
[features]
memories = true

[memories]
extract_model = "gpt-5.4"
consolidation_model = "gpt-5.4"
```

> 原生记忆功能支持从对话中提取记忆，并在多会话间自动归并，提升上下文连贯性。

### 5. 开启 WebSocket 支持

检查 `~/.codex/config.toml` 是否包含：

```toml
[features]
responses_websockets_v2 = true
```

> 如果没有这段，可以手动补上。

> **注意**：WebSocket 模式启用后，若中转站不支持会会回退到普通模式。

### 6. 放置模板

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

### 7. 最小验证

用一个 20~30 分钟的小任务测试：

- 任务可拆成 2~3 个独立子任务
- 子任务无写冲突
- 最后统一汇总结果

验证标准：

- 并行任务确实同时执行
- 输出质量可控，不是“快但乱”
- token 成本在你的预算范围内

### 8. 推荐迭代节奏

1. 先抄模板直接跑
2. 跑完一轮再裁剪规则
3. 每周复盘一次 AGENTS 文档

做到这三步，基本就进入正循环了。

### 9. 推荐最小配置（已合并）

下面这份 `~/.codex/config.toml` 最小配置，够你先稳定跑起来：

```toml
model_provider = "cch"
model = "gpt-5.4"
model_reasoning_effort = "high"
sandbox_mode = "workspace-write"

personality = "pragmatic"
web_search = "live"

[features]
multi_agent = true
memories = true
responses_websockets_v2 = true

[sandbox_workspace_write]
network_access = true

[agents]
max_threads = 5
max_depth = 1

[memories]
extract_model = "gpt-5.4"
consolidation_model = "gpt-5.4"
```

关键参数速记：

- `multi_agent = true`：多代理总开关（最重要）
- `memories = true`：启用原生记忆功能，提升上下文连贯性
- `responses_websockets_v2 = true`：启用 WebSocket 实时流式响应，不支持自动回退
- `model_reasoning_effort`：推理深度，越高通常越贵
- `sandbox_mode`：建议先用 `workspace-write`，兼顾安全和效率
- `web_search = "live"`：需要实时信息时更有用
- `max_threads = 5`：单轮最大并行子任务数（保守限制）
- `max_depth = 1`：禁止子代理再开子代理，避免递归失控

> 说明：本文档按 Codex CLI `v0.114.0` 适配；不同版本或供应商字段名可能有差异，请以你本地 CLI 支持为准。

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

本仓库是方法论与模板参考，当前按 Codex CLI v0.114.0 验证。
