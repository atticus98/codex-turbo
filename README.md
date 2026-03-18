# codex-turbo

[English](./README.en.md) | 简体中文

本仓库是 Codex CLI 的个人配置模板集，旨在充分利用 CLI 原生能力，实现多智能体自主协调下的并行任务调度。

> 💡 **不知道如何操作？** 可以将以项目地址发送给 AI 助手（如 Claude Code CLI、Codex CLI 等），让其根据你的实际情况协助合并或新建。

> 当前项目适配版本：**Codex CLI v0.115.0**
>
> 原帖 [《Codex CLI 多智能体并行调度配置分享》](https://linux.do/t/topic/1603762) 已无法编辑，本项目作为后续维护版本持续迭代。


## 核心要点

- 💡 **并行工作流**：`multi_agent = true` 最大并行度与最小阻塞设计
- 🔧 **系统级契约**：在 `config.toml` 中通过 `developer_instructions` 注入 Agent 并行工作规范，优先级高于 `AGENTS.md`
- 🧠 **原生记忆**：`memories = true` 自动提取和归并对话记忆，提升上下文连贯性
- 🔌 **WebSocket 支持**：`responses_websockets_v2 = true` 启用实时流式响应；如果当前后端服务或提供商不支持 WebSocket，会自动回退到传统模式
- 🎯 **对话风格**：强视觉边界、emoji 编号、直而短句的终端输出规范
- 📝 **动态契约**：主代理任务动态下发清晰的指令模板（目标/动作/结果）
- ⚙️ **并发控制**：`max_threads = n` 自定义单轮最大子任务数
- ⚠️ **风险管控**：危险操作确认机制与不可变原则
- 🤖 **自定义智能体**：手动配置子代理的模型、推理强度、职责描述
- 📋 **可复制模板**：开箱即用的 `AGENTS.template.md` 与 `config.template.toml`

## 目录结构

```text
.
├── README.md                  # 中文文档（本页）
├── README.en.md               # English Documentation
└── templates/
    ├── cn/                        # 中文模板
    │   ├── AGENTS.template.md         # 开发原则与输出风格
    │   ├── config.template.toml       # 系统配置模板
    │   ├── agents/                    # 子代理配置
    │   │   ├── explorer.toml
    │   │   └── worker.toml
    │   └── skills/                    # 技能模板
    │       └── terminal-dialog-style/
    └── en/                        # English Templates
        ├── AGENTS.template.en.md
        ├── config.toml.en.example
        ├── agents/
        └── skills/
```

## 快速上手（5 分钟）

目标：把你的 Codex CLI 切到”并行 + 模板化”工作模式。

### 1. 克隆仓库

```bash
git clone <your-repo-url>
cd codex-turbo
```

### 2. 复制模板配置

本仓库提供以下模板文件：

| 文件 | 用途 | 目标位置 |
|------|------|----------|
| `templates/cn/config.template.toml` | 核心的系统配置（含 `developer_instructions` 并行工作规范） | `~/.codex/config.toml` |
| `templates/cn/AGENTS.template.md` | 开发原则与输出风格指南 | `~/.codex/AGENTS.md` |
| `templates/cn/agents/` | 子代理配置（explorer、worker） | `~/.codex/agents/` |
| `templates/cn/skills/` | 技能模板（terminal-dialog-style 等） | `~/.codex/skills/` |

> config.toml 请根据服务商的要求自行完善 key 等供应商信息。

**首次使用（直接复制）**：

```bash
# 创建目标目录（如不存在）
mkdir -p ~/.codex

# 复制核心配置文件
cp templates/cn/AGENTS.template.md ~/.codex/AGENTS.md
cp templates/cn/config.template.toml ~/.codex/config.toml

# 复制子代理和技能目录
cp -r templates/cn/agents ~/.codex/
cp -r templates/cn/skills ~/.codex/
```

**已有配置（手动合并）**：

不要直接覆盖现有的 `~/.codex`，建议按下面的步骤合并。


> - 你的现有配置：`~/.codex/config.toml`、`~/.codex/AGENTS.md`
> - 本仓库模板：`templates/cn/config.template.toml`、`templates/cn/AGENTS.template.md`

1. **先备份现有配置**

```bash
cp ~/.codex/config.toml ~/.codex/config.toml.bak
cp ~/.codex/AGENTS.md ~/.codex/AGENTS.md.bak
[ -d ~/.codex/agents ] && cp -R ~/.codex/agents ~/.codex/agents.bak
[ -d ~/.codex/skills ] && cp -R ~/.codex/skills ~/.codex/skills.bak
```

> 如果你本地已经存在 `~/.codex/agents.bak` 或 `~/.codex/skills.bak`，请先手动处理旧备份，避免再次执行 `cp -R` 时把目录复制成嵌套结构。

2. **先看差异，再决定怎么合**

```bash
diff -u ~/.codex/config.toml templates/cn/config.template.toml
diff -u ~/.codex/AGENTS.md templates/cn/AGENTS.template.md
```

3. **`config.toml` 至少合并这些关键块**

- `developer_instructions`
- `[agents.explorer]`
- `[agents.worker]`
- `[features]`
- `[agents]`
- `[memories]`

4. **同步关联文件（强制检查项），不要只改主配置**

`[agents.explorer]` 和 `[agents.worker]` 中的这两行属于必合并项：

- `config_file = "agents/explorer.toml"`
- `config_file = "agents/worker.toml"`

因此，下面这些文件也必须同时存在：

```bash
mkdir -p ~/.codex/agents ~/.codex/skills/terminal-dialog-style
cp templates/cn/agents/explorer.toml ~/.codex/agents/explorer.toml
cp templates/cn/agents/worker.toml ~/.codex/agents/worker.toml
cp templates/cn/skills/terminal-dialog-style/SKILL.md ~/.codex/skills/terminal-dialog-style/SKILL.md
```

5. **合并完成后，做一次快速自检**

```bash
# 检查 config.toml 关键块和 config_file 声明
rg -n "developer_instructions|\\[agents\\.explorer\\]|\\[agents\\.worker\\]|\\[features\\]|\\[agents\\]|\\[memories\\]|config_file" ~/.codex/config.toml

# 检查关联文件是否存在
test -f ~/.codex/agents/explorer.toml && echo "OK: agents/explorer.toml"
test -f ~/.codex/agents/worker.toml && echo "OK: agents/worker.toml"
test -f ~/.codex/skills/terminal-dialog-style/SKILL.md && echo "OK: skills/terminal-dialog-style/SKILL.md"

# 可选：查看目录结构
ls -R ~/.codex/agents ~/.codex/skills
```

预期结果：

- 第一个命令应至少匹配出这些块或字段：`developer_instructions`、`[agents.explorer]`、`[agents.worker]`、`[features]`、`[agents]`、`[memories]`、`config_file`
- 后三个 `test -f` 命令都应输出对应的 `OK: ...`
- 如果 `ls -R` 报 `No such file or directory`，说明关联目录没有准备完整，需要回到上一步补齐

6. **如果需要回滚，按下面恢复**

先确认这些备份文件或目录存在：

- `~/.codex/config.toml.bak`
- `~/.codex/AGENTS.md.bak`
- `~/.codex/agents.bak`
- `~/.codex/skills.bak`

然后执行：

```bash
cp ~/.codex/config.toml.bak ~/.codex/config.toml
cp ~/.codex/AGENTS.md.bak ~/.codex/AGENTS.md

rm -rf ~/.codex/agents
rm -rf ~/.codex/skills

cp -R ~/.codex/agents.bak ~/.codex/agents
cp -R ~/.codex/skills.bak ~/.codex/skills
```

> ⚠️ `rm -rf ~/.codex/agents` 和 `rm -rf ~/.codex/skills` 会直接删除当前目录内容。执行前请先确认 `~/.codex/agents.bak` 与 `~/.codex/skills.bak` 确实存在，且里面是你要恢复的旧配置。

> 不建议直接覆盖你本地已有的供应商配置、API key、MCP 服务配置或其他带环境依赖的字段；模板负责“工作方式”，你本地配置负责“运行环境”。

> ⚠️ **重点**：`config.template.toml` 中的 `developer_instructions` 是系统级契约，优先级高于 `AGENTS.md`，务必确保已合并。

> 说明：本文档按 Codex CLI `v0.115.0` 适配；不同版本或供应商字段名可能有差异，请以你本地 CLI 支持为准。


## 免责声明

本仓库提供的是配置方法论与模板参考，基于 Codex CLI `v0.115.0` 验证。

**成本提示**：多智能体并发模式下，Token 消耗可能上升 20%~30%，请根据实际情况合理评估使用。

**风险提示**：LLM 可能产生错误判断，导致数据误删或代码被错误修改。建议：
- 合理配置沙箱权限与操作确认机制
- 在可控环境中先行测试
- 对重要数据做好备份

使用本模板所产生的一切后果由使用者自行承担。
