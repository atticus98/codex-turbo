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
│   ├── quick-start.md
│   └── faq.md
└── templates
    ├── AGENTS.template.md
    └── config.toml.example
```

## 快速开始

1. 克隆仓库

```bash
git clone <your-repo-url>
cd codex-turbo
```

2. 先看 5 分钟上手

- `docs/quick-start.md`

3. 复制 / 合并模板到你的 Codex 环境

```bash
cp templates/AGENTS.template.md ~/.codex/AGENTS.md
cp templates/config.toml.example ~/.codex/config.toml
```

> 如果你本地已经有 `~/.codex/AGENTS.md` 或 `~/.codex/config.toml`，建议先复制为
> `*.template` 后手动合并，避免直接覆盖自定义配置。

4. 打开 Codex CLI，确认已开启多代理

- 在 `/experimental` 中勾选 `Multi-agents`
- 或直接检查 `~/.codex/config.toml`：

```toml
[features]
multi_agent = true
```

## 文档导航

- `docs/quick-start.md`：最短路径跑起来
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
