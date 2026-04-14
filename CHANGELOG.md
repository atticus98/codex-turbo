# 发布日志

## v1.6.0 - 2026-04-14

### 🎯 版本主题
- **终端对话 Skill 深度优化** - 确立源码定位三层策略，严格路径缩写规范，同步中英双语
- **响应契约与引导优化** - 精简响应引导逻辑，强化响应一致性
- **文档品牌化提升** - 润色 README 简介，确立「轻量高效」原则

---

### ✨ 核心更新

#### 1️⃣ 终端对话 Skill (terminal-dialog-style) 深度迭代

**变更内容**：本次更新是对终端输出体验的一次重大重构，旨在彻底解决终端环境下长路径溢出、代码证据缺失以及机械化引导等问题。

**主要调整**：
- **确立源码定位三层策略**：建立「直接贴代码（≤10行） > 节选核心 > 极简引用」的严格降序策略。强调“代码即证据”，严禁仅用文字转述代码逻辑而不贴出原文。
- **强制路径缩写规范**：将「严禁带目录前缀的长路径」提升为绝对禁令。无论上下文路径多长，输出时必须强制缩写为文件名短名（如 `UserService.kt:L35`），确保终端完美对齐。
- **移除「引导下一步」规范**：取消了对话末尾强制性的“下一步建议”，改为按需引导，避免 AI 产生机械化、敷衍的对话结尾。
- **细化视觉排版**：明确 TL;DR 摘要与其后的正文之间必须保留一个空行；重构了所有中英文示例，增加了更复杂的流程解析图示。

**涉及文件**：
- `templates/cn/skills/terminal-dialog-style/SKILL.md`
- `templates/en/skills/terminal-dialog-style/SKILL.md`

#### 2️⃣ 开发原则与配置模板同步

- **优化响应引导逻辑**：对 `AGENTS.template.md` 进行了精简，明确仅在咨询类问答结束时给出建议，保持开发过程中的高效直观。
- **双语同步增强**：同步了 English AGENTS 模板与 V3.2 协议口径，并对 English worker agent 的指令描述进行了对齐。

**涉及文件**：
- `templates/cn/AGENTS.template.md`
- `templates/en/AGENTS.template.en.md`
- `templates/en/agents/worker.toml`

#### 3️⃣ README 体验与品牌润色

- **确立“轻量高效”品牌定位**：润色了 README 的简介部分，强调在不引入复杂依赖的前提下挖掘 CLI 原生能力。
- **排版优化**：对 README 的核心要点和简介部分的文本进行了排版优化，提升视觉呼吸感。

---

### 📊 统计数据

**本次发布主要包含以下提交记录：**
- `b46c737` - docs(skill): update terminal-dialog-style with new examples and synchronize English translation
- `5fcc374` - docs(skill): 强化 terminal-dialog-style 的源码定位三层策略与代码证据规范
- `f3415ef` - feat(skill): 从 terminal-dialog-style 中移除「引导下一步」规范
- `e90314f` - docs(cn): 优化 AGENTS.template.md 响应规范与响应引导逻辑
- `ad66941` - docs: sync English AGENTS template with V3.2 protocol and refine README
- `db8a0d6` - docs: sync english worker agent instructions with chinese version
- `da3504f` - docs: 润色 README 简介部分，增强表达力并强调轻量高效原则
- `b8b5e85` - docs: 优化 README.md 文本排版
- `f0ce797` - docs: sync english terminal-dialog-style skill with chinese version
- `1fd24d7` - docs(skill): 强化终端对话中 ASCII 表格的使用规范并硬性禁止 Markdown 表格

---

### 📋 升级指南

#### 从 v1.5.x 升级

1. **拉取最新代码**
   ```bash
   git pull origin main
   ```

2. **覆盖 Skill 文件（核心推荐）**
   由于 `terminal-dialog-style` 逻辑变动较大，建议直接覆盖：
   ```bash
   cp -r templates/cn/skills/terminal-dialog-style ~/.codex/skills/
   ```

3. **同步 AGENTS 模板**
   ```bash
   cp templates/cn/AGENTS.template.md ~/.codex/AGENTS.md
   ```

---

### ⚠️ 注意事项

1. **源码定位策略强制化** - 新版 Skill 会更频繁地直接展示代码，若需节省 Token，请在特定对话中手动干预。
2. **路径缩写是硬性约束** - 若观测到子代理仍输出长路径，请检查 Skill 是否已正确加载。

---

> 📅 **发布日期**: 2026-04-14
> 📌 **版本**: v1.6.0
> 🎯 **主题**: 终端对话 Skill 深度优化与响应一致性增强

---

## v1.5.1 - 2026-03-27

### 🎯 版本主题
- **终端表格与规范强化** - 全面禁止 Markdown 表格语法，强化 ASCII 表格作为终端唯一合法表格形式

---

### ✨ 核心更新

#### 1️⃣ 终端对话中硬性禁止 Markdown 表格

**变更原因**：由于终端环境（如 Codex CLI）无法渲染 Markdown 表格语法（`| xxx |`），导致显示效果极其散乱且难以阅读。本次更新将「禁止 Markdown 表格」提升为硬性契约规范。

**主要调整**：
- **规范升级**：在 `terminal-dialog-style` Skill 中明确定义了 Markdown 表格的硬性禁止规则
- **示例重构**：将所有中英文示例中的正反例表格、路径规范表格等全部重构为 `+---+` 框线的 ASCII 表格
- **排版对齐**：统一了路径引用示例的表格样式，确保在等宽字体终端下的完美对齐

**涉及文件**：
- `templates/cn/skills/terminal-dialog-style/SKILL.md`
- `templates/en/skills/terminal-dialog-style/SKILL.md`

---

## v1.5.0 - 2026-03-25

### 🎯 版本主题
- **配置模板持续打磨** - 中文配置模板重排结构并同步到 Codex CLI v0.116.0
- **子代理边界收紧** - 强化 worker 只处理局部任务的契约，补齐运行时管理规则
- **终端输出体验回修** - 修复 terminal-dialog-style 的视觉退步并补齐双语同步
- **文档入口收口** - FAQ 并入 README，手动合并流程独立成专项文档

---

### ✨ 核心更新

#### 1️⃣ 模型与推理强度策略调整（重要变更）

**变更内容**：本次调整了主代理与子代理的默认模型策略，目标是在通用任务场景下取得更好的速度、响应效率与调度体验平衡。

**具体调整**：
- 主代理默认模型保持为 `gpt-5.4`，默认 `model_reasoning_effort` 调整为 `medium`
- `explorer` 子代理默认模型调整为 `gpt-5.4-mini`，`model_reasoning_effort = "medium"`
- `worker` 子代理默认模型调整为 `gpt-5.4-mini`，`model_reasoning_effort = "high"`

**调整思路**：
这次调整本质上是在“性能”与“强推理”之间重新设定默认平衡点。对于大多数通用业务任务，并不需要在起始阶段就使用更重的模型或更高的思考强度；将默认档位落到更均衡的位置，通常可以改善 Codex 的响应速度、任务切换效率以及多代理协作时的整体吞吐表现。

**使用建议**：
- 日常业务开发、常规排查、普通文档整理等通用场景，当前默认配置通常已经足够
- 涉及复杂推理、跨模块重构、长链路分析等高强度任务时，仍建议按任务复杂度主动上调模型规格或推理强度

**涉及文件**：
- `templates/cn/config.template.toml`
- `templates/cn/agents/explorer.toml`
- `templates/cn/agents/worker.toml`
- `templates/en/config.toml.en.example`
- `templates/en/agents/explorer.toml`
- `templates/en/agents/worker.toml`

#### 2️⃣ 配置模板升级到 v0.116.0（重要变更）

**变更原因**：最近两天的改动主要围绕 `templates/cn/config.template.toml` 展开，目标是把配置模板整理成更清晰的层级，同时跟进 Codex CLI v0.116.0 的最新口径。

**核心调整**：
- 重排顶层配置顺序，统一为「全局配置 → 功能开关 → 代理定义」
- `[features]` 新增 `fast_mode = true`
- `[model_providers.cch]` 增加 `env_key = "CCH_API_KEY"`，默认走环境变量管理密钥
- 精简 `model_provider`、`reasoning_effort`、`suppress_unstable_features_warning` 等注释
- 将 `developer_instructions` 中的主代理调度策略重新分组，便于后续维护
- 同步模板版本到 Codex CLI `v0.116.0`

**受影响文件**：
- `templates/cn/config.template.toml`
- `templates/en/config.toml.en.example`

#### 3️⃣ worker 局部任务边界强化

**变更内容**：围绕主代理调度与子代理职责，补了一轮更明确的边界约束。

**新增/强化规则**：
- worker 仅处理局部、模块级实现任务
- 明确 5 类不得下发给 worker 的全局性工作
- 新增「完成后及时关闭子代理」约束，避免长期占用线程配额
- 子代理中途受阻时，要求输出结构化交接信息，便于主代理接管
- 中英文模板与 agent 配置同步收口，避免中英文契约漂移

**涉及文件**：
- `templates/cn/config.template.toml`
- `templates/cn/agents/worker.toml`
- `templates/cn/agents/explorer.toml`
- `templates/en/config.toml.en.example`
- `templates/en/agents/explorer.toml`
- `templates/en/agents/worker.toml`

#### 4️⃣ terminal-dialog-style Skill 体验修复

**变更内容**：修复前一版终端输出风格 Skill 的多项体验退步，并同步双语版本。

**修复点**：
- 恢复 emoji 点缀与视觉引导
- 将路径引用规范提升为独立的必须规则，并补充正反例
- 明确 TL;DR 必须使用 `>` 引用块包裹
- 恢复 ASCII 表格与图示 few-shot 示例，解决「规范存在但不容易触发」的问题
- 英文版同步更新 frontmatter 与文案细节

**涉及文件**：
- `templates/cn/skills/terminal-dialog-style/SKILL.md`
- `templates/en/skills/terminal-dialog-style/SKILL.md`

#### 5️⃣ README / FAQ / 手动合并文档收口

**变更内容**：将零散 FAQ 并回主 README，把手动配置合并步骤抽成独立文档。

**结构调整**：
- `docs/faq.md` / `docs/faq.en.md` 删除
- FAQ 内容迁移到 `README.md` / `README.en.md`
- 新增 `docs/manual-merge.md` / `docs/manual-merge.en.md`

**收益**：
- README 成为单一入口，减少跳转
- 手动合并流程有独立文档承载，适合直接链接给使用者

#### 6️⃣ 模板与仓库卫生补充

- 中文 AGENTS 模板重写主代理指令表述，强化 Skills 优先与 KISS / YAGNI 原则
- 中英文子代理模板统一到最新模型与沙箱口径
- `.gitignore` 补充忽略 macOS `.DS_Store`

---

### 📊 统计数据

**本次发布包含 11 个提交：**
- `bc7181a` - chore: 补充 .gitignore 忽略 macOS .DS_Store 文件
- `059f6d3` - docs(template): 重构主代理指令与模板文档，提升表述精确性
- `3a75211` - feat(agents): 调整子代理配置与终端对话风格规范
- `ca59305` - refactor(config): 重排配置项顺序，新增 fast_mode
- `fcead6e` - docs(config): 全面优化配置模板可读性与结构
- `1b42e36` - refactor(cn): 重构调度策略分组，强化 worker 局部任务边界约束
- `c3416c8` - fix(skills): 修复 terminal-dialog-style 的多项体验退步
- `a333c17` - chore(templates/en): sync en templates to match latest cn version
- `53d1a24` - chore(templates): tune sub-agent model and sandbox settings
- `e5c90c0` - docs: migrate FAQ into README and extract manual merge guide
- `a206f89` - chore: sync config template to v0.116.0

**文件变更：**
- 涉及 17 个唯一文件
- 总计约 `+804 / -644`，净增约 `160` 行
- 新增 2 个手动合并文档
- 删除 2 个 FAQ 文档
- 持续修改中英双语模板、README 与子代理配置

---

### 📋 升级指南

#### 从 v1.4.0 升级

1. **拉取最新代码**
   ```bash
   git pull origin main
   ```

2. **合并最新配置模板（关键步骤）**

   **建议重点检查以下字段**：
   - `templates/cn/config.template.toml` 中新增/调整的 `fast_mode`
   - `[model_providers.cch]` 中的 `env_key = "CCH_API_KEY"`
   - `developer_instructions` 里新增的 worker 边界、子代理关闭规则
   - `templates/cn/agents/*.toml` 与 `templates/en/agents/*.toml` 中的模型、推理强度、沙箱配置

   **已有自定义配置时，建议先对比差异**：
   ```bash
   diff -u templates/cn/config.template.toml ~/.codex/config.toml
   diff -u templates/cn/agents/worker.toml ~/.codex/agents/worker.toml
   diff -u templates/cn/agents/explorer.toml ~/.codex/agents/explorer.toml
   ```

3. **同步 README 与手动合并文档**
   - FAQ 不再单独维护
   - 若你以前引用 `docs/faq.md`，请改为 `README.md` 或 `docs/manual-merge.md`
   - 英文场景对应使用 `README.en.md` 与 `docs/manual-merge.en.md`

4. **验证版本与关键目录**
   ```bash
   codex --version
   ls -la docs/manual-merge.md docs/manual-merge.en.md
   ls -la templates/cn/agents templates/en/agents
   ```

---

### ⚠️ 注意事项

1. **配置模板有顺序调整** - 手动合并时不要只看行 diff，要按区块语义合并
2. **FAQ 文档已移除** - 外部引用旧路径会失效
3. **子代理契约更严格** - 旧自定义 worker 若仍承担全局任务，建议重新审查边界
4. **终端输出 Skill 已更新** - 若你本地已复制旧版 `terminal-dialog-style`，建议重新覆盖同步

---

> 📅 **发布日期**: 2026-03-25
> 📌 **版本**: v1.5.0
> 🎯 **主题**: 配置模板打磨、子代理边界收紧与文档入口收口

---

## v1.4.0 - 2026-03-18

### 🎯 版本主题
- **模板资产重组** - 按语言分离为 `templates/cn` 与 `templates/en` 目录结构
- **输出风格 Skill 化** - 将终端对话风格提取为独立可复用的 Skill
- **全局指令精简** - AGENTS 模板收敛为核心约束，降低上下文占用
- **子代理自定义描述** - 新增 `explorer` 与 `worker` 子代理配置模板，最大化节省上下文

---

### ✨ 核心更新

#### 1️⃣ 模板目录结构重构（重要变更）

**变更原因**：按语言分离模板资产，便于维护与复制，同时为中英文版本提供独立的 agents 和 skills 扩展能力。

**新目录结构**：
```
templates/
├── cn/                              # 中文模板集
│   ├── AGENTS.template.md           # 全局共享规范（精简版）
│   ├── config.template.toml         # 配置模板
│   ├── agents/                      # 子代理配置
│   │   ├── explorer.toml            # 只读探索型子代理
│   │   └── worker.toml              # 局部实现型子代理
│   └── skills/                      # Skills 集合
│       └── terminal-dialog-style/   # 终端对话风格
│           └── SKILL.md
└── en/                              # 英文模板集（同结构）
    ├── AGENTS.template.en.md
    ├── config.toml.en.example
    ├── agents/
    │   ├── explorer.toml
    │   └── worker.toml
    └── skills/
        └── terminal-dialog-style/
            └── SKILL.md
```

**迁移路径**：
- `templates/AGENTS.template.md` → `templates/cn/AGENTS.template.md`
- `templates/config.toml.example` → `templates/cn/config.template.toml`
- `templates/AGENTS.template.en.md` → `templates/en/AGENTS.template.en.md`
- `templates/config.toml.en.example` → `templates/en/config.toml.en.example`

#### 2️⃣ 输出风格 Skill 化

**变更内容**：将 AGENTS 模板中的「对话输出风格指南」章节（约 100 行）提取为独立 Skill。

**优势**：
- **按需加载** - 仅在需要时激活，节省主对话上下文
- **可复用** - 可跨项目、跨语言复用
- **独立演进** - 风格规范可独立更新，不影响核心契约

**使用方式**：复制到 `~/.codex/skills/terminal-dialog-style/SKILL.md`

#### 3️⃣ 全局指令精简

**变更前**：AGENTS 模板包含完整的输出风格、并发规范、子代理契约等，约 200+ 行。

**变更后**：收敛为核心约束，约 100 行：
- 全局共享规范（沟通输出、项目规范、完成口径）
- 开发原则（语言规范、基本原则、质量标准）
- 危险操作确认机制
- 输出结尾建议

**效果**：降低主对话上下文占用，复杂契约按需通过 Skill 或子代理配置加载。

#### 4️⃣ 子代理自定义描述

**新增文件**：
- `templates/cn/agents/explorer.toml` - 只读探索型子代理
- `templates/cn/agents/worker.toml` - 局部实现型子代理

**核心设计**：通过 `developer_instructions` 覆盖子代理描述，精准限定职责边界：

| 子代理 | 职责定位 | 禁止事项 |
|--------|----------|----------|
| explorer | 只读探索、证据收集、调用链追踪 | 修改文件、生成补丁、调度其他代理 |
| worker | 局部实现、授权范围内修改 | 擅自扩大范围、调度其他代理 |

**上下文节省**：子代理描述精简至 10-15 行，避免加载完整的 AGENTS 模板。

#### 5️⃣ README 文档完善

- **目录结构说明** - 更新为 `templates/cn` 和 `templates/en` 分离布局
- **配置合并步骤** - 补充完整的配置自检命令与预期结果
- **备份与回滚指南** - 新增 `~/.codex/agents` 与 `~/.codex/skills` 目录级备份操作
- **WebSocket Fallback 说明** - 统一中英文文档，明确后端不支持时自动回退到传统模式
- **契约描述更新** - 将「标准契约」改为「动态契约」，强调主代理动态下发指令

#### 6️⃣ 中英文文档同步

- 以中文 README 为基准重写 README.en.md
- 同步英文文档至当前 Codex CLI v0.115.0 口径
- 移除已删除的 `docs/faq.md` 引用

---

### 📊 统计数据

**本次发布包含 9 个提交：**
- `ff7ff1b` - feat: 拆分多语言 Codex 模板资产
- `d5bff34` - feat: align English templates with the CN source set
- `7433c45` - docs: 更新 README.md 以反映新的目录结构
- `6b3e936` - docs: 完善 README 的模板复制说明
- `b6c47fa` - docs: 格式调整
- `413da1e` - docs: 补充 codex 配置目录备份与回滚说明
- `2b82712` - docs: 完善配置合并自检步骤并更新契约描述
- `8cf8e67` - docs: 重构英文文档以对齐中文版本
- `dcf57d6` - docs: 同步中英文 README 并统一 websocket fallback 说明

**文件变更：**
- 新增 8 个文件（cn/en 目录下的模板、agents、skills）
- 删除 4 个文件（根级中英文模板）
- 修改 2 个 README 文件
- 净增约 218 行（+960 / -742）

---

### 📋 升级指南

#### 从 v1.3.0 升级

1. **拉取最新代码**
   ```bash
   git pull origin main
   ```

2. **更新配置（关键步骤）**

   **首次使用（直接复制）**：
   ```bash
   # 创建必要目录
   mkdir -p ~/.codex/agents ~/.codex/skills

   # 复制中文模板
   cp templates/cn/AGENTS.template.md ~/.codex/AGENTS.md
   cp templates/cn/config.template.toml ~/.codex/config.toml
   cp -r templates/cn/agents/* ~/.codex/agents/
   cp -r templates/cn/skills/* ~/.codex/skills/
   ```

   **已有配置（手动合并）**：
   ```bash
   # 备份现有配置
   cp ~/.codex/config.toml ~/.codex/config.toml.bak
   cp ~/.codex/AGENTS.md ~/.codex/AGENTS.md.bak

   # 对比差异后合并关键配置项
   diff templates/cn/config.template.toml ~/.codex/config.toml
   ```

3. **验证配置**
   ```bash
   # 检查关键配置块
   grep -E "^\[|^model|^developer_instructions" ~/.codex/config.toml | head -20

   # 确认关联文件存在
   ls -la ~/.codex/AGENTS.md ~/.codex/config.toml
   ls -la ~/.codex/agents/
   ls -la ~/.codex/skills/
   ```

4. **验证版本**
   - 确保 Codex CLI 版本为 `v0.115.0`
   - 执行 `codex --version` 检查

---

### ⚠️ 注意事项

1. **路径变更** - 模板路径从根级迁移至 `templates/cn/` 和 `templates/en/`
2. **文件重命名** - `config.toml.example` → `config.template.toml`（命名更规范）
3. **Skill 独立** - 输出风格已独立为 Skill，需复制到 `~/.codex/skills/` 目录
4. **子代理可选** - `agents/` 目录下的子代理配置为可选增强，按需启用

---

> 📅 **发布日期**: 2026-03-18
> 📌 **版本**: v1.4.0
> 🎯 **主题**: 模板重组与上下文优化

---

## v1.3.0 - 2026-03-16

### 🎯 版本主题
- **系统级提示词配置** - 将并行工作规范迁移至 `developer_instructions`，优先级高于 `AGENTS.md`
- **适配版本升级** - 全面适配 Codex CLI v0.114.0

---

### ✨ 核心更新

#### 1️⃣ 系统级提示词迁移（重要变更）

**变更原因**：`developer_instructions` 是 Codex CLI 的系统级配置，优先级高于项目级 `AGENTS.md`，能确保核心契约始终生效。

**删除位置**：`templates/AGENTS.template.md`
- 移除「Agent 并行工作规范」完整契约章节（约 88 行）

**新增位置**：`templates/config.toml.example`
- 新增 `developer_instructions` 配置项，包含完整的并行工作规范契约（约 133 行）

**迁移内容**：
- 主代理与子代理分工细则
- 子任务智能体契约（代理名称/任务定义/执行动作/禁止事项/预期结果）
- 并行调度与子任务下发流程
- 等待策略与防死锁熔断机制
- 失败处理与接管协商策略
- 串行回退条件决策表

#### 2️⃣ AGENTS.template.md 重构 v1.4.0
- 精简为开发原则与输出风格指南
- 新增 SIMPLE 架构原则，强调代码可读性
- 细化 ASCII 表格/图示使用规则
- 更新版本至 v1.4.0

#### 3️⃣ 适配版本升级至 v0.114.0
- 更新 README.md 版本引用（4 处）

---

### 📊 统计数据

**文件变更：**
- `templates/config.toml.example` - +133 行（新增 developer_instructions）
- `templates/AGENTS.template.md` - -88 行（移除并行工作规范），+57 行（重构内容）
- `README.md` - 更新版本引用（4 处）

---

### 📋 升级指南

#### 从 v1.2.0 升级

1. **拉取最新代码**
   ```bash
   git pull origin main
   ```

2. **更新配置（关键步骤）**

   ⚠️ **必须操作**：将 `developer_instructions` 合并到你的 `~/.codex/config.toml`

   ```bash
   # 方式一：直接复制（首次使用或无自定义配置）
   cp templates/config.toml.example ~/.codex/config.toml

   # 方式二：手动合并（已有自定义配置）
   # 从 templates/config.toml.example 复制 developer_instructions 配置项
   # 到你的 ~/.codex/config.toml 文件顶部
   ```

3. **可选操作**：清理 `AGENTS.md` 中的冗余内容
   - 由于 `developer_instructions` 已包含并行工作规范
   - 可删除 `~/.codex/AGENTS.md` 中重复的契约内容
   - 或直接使用新的精简版模板：
     ```bash
     cp templates/AGENTS.template.md ~/.codex/AGENTS.md
     ```

4. **验证版本**
   - 确保 Codex CLI 版本为 `v0.114.0`
   - 执行 `codex --version` 检查

---

### ⚠️ 注意事项

1. **优先级说明** - `developer_instructions` > `AGENTS.md`，系统级配置优先于项目级
2. **配置合并** - 务必将 `developer_instructions` 添加到 `config.toml`，保证尽可能高的遵循度
3. **版本依赖** - 基于 Codex CLI `v0.114.0` 验证，低版本可能不支持 `developer_instructions` 字段

---

> 📅 **发布日期**: 2026-03-16
> 📌 **版本**: v1.3.0
> 🎯 **主题**: 系统级提示词配置与版本升级

---

## v1.2.0 - 2026-03-08

### 🎯 版本主题
- **模型升级至 GPT-5.4** - 同步最新模型能力，优化成本与性能平衡
- **原生记忆功能支持** - 启用 memories 实现跨会话上下文连贯性
- **WebSocket 支持** - 实现实时流式响应，提升交互体验
- **适配版本升级** - 全面适配 Codex CLI v0.111.0 新特性

---

### ✨ 核心更新

#### 1️⃣ 模型与推理配置升级
- **模型升级**：`gpt-5.3-codex` → `gpt-5.4`
- **推理强度调整**：`xhigh` → `high`
  - 在 GPT-5.4 上 `high` 已能提供优秀的推理质量
  - 降低 token 成本，提升响应速度
- **新增规划模式推理强度**：`plan_mode_reasoning_effort = "xhigh"`
  - 规划阶段使用更高推理强度，避免方向性错误

#### 2️⃣ 原生记忆功能 (Memories)
- 新增 `[features]` 区块配置：`memories = true`
- 新增 `[memories]` 配置区块：
  - `extract_model` - 单对话线程记忆提取模型
  - `consolidation_model` - 多线程记忆归并/整理模型
- 支持从对话中自动提取关键信息
- 跨会话自动归并记忆，提升长期上下文连贯性

#### 3️⃣ WebSocket 实时流式响应支持
- 新增 `[features]` 区块配置：`responses_websockets_v2 = true`
- 启用 WebSocket 实现实时流式响应，提升交互体验
- 自动回退机制：若中转站不支持 WebSocket，自动降级到常规 HTTP 响应
- ⚠️ **注意**：并非所有中转站都支持 WebSocket，请根据实际情况测试

#### 4️⃣ 新增配置项
- `suppress_unstable_features_warning = true` - 抑制开发中功能警告
- `[tui]` 区块 - 状态栏自定义配置
  - `status_line` - 可配置显示模型、分支、剩余上下文等信息

#### 5️⃣ 适配版本升级至 v0.111.0
- 更新 README.md 版本引用（4 处）
- 更新 CHANGELOG.md 历史版本记录
- 更新 AGENTS.template.md 版本信息
- 更新 config.toml.example 配置模板

#### 6️⃣  README 文档完善
- 新增"启用原生记忆功能"步骤说明
- 更新最小配置示例，加入 memories 配置
- 在核心要点中新增原生记忆要点（🧠）
- 在关键参数速记中补充 memories 说明




---

### 📊 统计数据

**文件变更：**
- `README.md` - 新增记忆功能和 WebSocket 指南，更新配置示例
- `CHANGELOG.md` - 新增 v1.2.0 版本记录
- `templates/AGENTS.template.md` - 更新版本信息
- `templates/config.toml.example` - 升级模型配置，新增 memories 和 WebSocket 配置

---

### 📋 升级指南

#### 从 v1.1.0 升级

1. **拉取最新代码**
   ```bash
   git pull origin main
   ```

2. **更新配置（手动合并关键项）**
   ```toml
   # 模型升级
   model = "gpt-5.4"
   model_reasoning_effort = "high"
   
   # 新增规划模式推理强度
   plan_mode_reasoning_effort = "xhigh"
   
   # 启用原生记忆
   [features]
   multi_agent = true
   memories = true
   responses_websockets_v2 = true

   [memories]
   extract_model = "gpt-5.4"
   consolidation_model = "gpt-5.4"
   ```

3. **验证版本**
   - 确保 Codex CLI 版本为 `v0.111.0`
   - 执行 `codex --version` 检查

---

### ⚠️ 注意事项

1. **模型变更** - GPT-5.4 与 GPT-5.3-codex 的响应风格可能略有差异，建议先小范围测试
2. **成本优化** - `high` 相比 `xhigh` 显著降低成本，但复杂任务可考虑临时提升至 `xhigh`
3. **记忆功能** - 首次启用可能需要一定时间积累记忆，效果随使用次数提升
4. **WebSocket 支持** - `responses_websockets_v2 = true` 启用实时流式响应；若中转站不支持，会报错但不会自动回退
5. **版本依赖** - 基于 Codex CLI `v0.111.0` 验证，低版本可能存在字段差异

---

### 🎓 使用建议

1. **成本敏感场景** - 默认使用 `high`，复杂规划任务临时提升至 `xhigh`
2. **记忆功能** - 适合需要长期维护的项目，能自动记住代码规范和偏好
3. **团队项目** - 建议统一配置 `memories` 模型参数，确保记忆提取一致性

---

> 📅 **发布日期**: 2026-03-08  
> 📌 **版本**: v1.2.0  
> 🎯 **主题**: 模型升级与原生记忆支持

---

## v1.1.0 - 2026-03-03

### 🎯 版本主题
- **对话风格与配置标准化** - 建立完整的 Codex CLI 并行工作规范与可视化文档体系
- **子代理并发数限制** - 结合最新项目规范，通过配置限制子代理最大并发数
- **移除部分过期配置** - 精简配置，移除过期配置

---

### ✨ 核心更新

#### 1️⃣ AGENTS 文档全面优化
- 重构 `AGENTS.template.md` 使用更一致的 emoji 编号系统（1️⃣ 2️⃣ 3️⃣ 4️⃣）
- 优化对话输出风格指南，增强可读性和视觉边界
- 标准化危险操作确认机制的格式模板
- 新增"标准契约"要求：子代理任务下发必须包含代理名称/任务定义/执行动作/预期结果

#### 2️⃣ 配置模板完善
- 为 `config.toml.example` 所有配置项添加清晰的简体中文注释
- 新增 `[sandbox_workspace_write]` 区块明确网络访问配置
- 新增 `[agents]` 区块配置：
  - `max_threads = 5` - 单轮最大并行子任务数（保守限制）
  - `max_depth = 1` - 禁止子代理再开子代理，避免递归失控
- 提供保守模式参考配置（read-only 沙箱、medium 推理强度）

#### 3️⃣ 版本升级
- 升级适配版本至 **Codex CLI v0.111.0**
- 更新所有文档中的版本引用

#### 4️⃣ 并发控制统一
- 统一 AGENTS 文档与配置文件的并行度上限为 **5 个**
- 与 `max_threads = 5` 配置保持一致

#### 5️⃣ README 同步更新
- 核心要点新增并发控制、标准契约、风险管控说明
- 同步 README 配置模板与 `config.toml.example` 保持一致
- 补充关键参数速记：`max_threads` 与 `max_depth` 说明

---

### 📊 统计数据

**本次发布包含 6 个提交：**
- `3bc82bc` - docs: 优化 AGENTS 文档格式与风格
- `2d21ed8` - docs: 更新核心要点，补充并发控制说明
- `6fc90c0` - docs: 统一并行度上限为 5 个
- `5696e04` - chore: 升级适配版本至 Codex CLI v0.111.0
- `b54dcdf` - docs: 完善配置模板注释与结构
- `cba0758` - docs: 同步 README 配置模板与 example 保持一致

**文件变更：**
- `templates/AGENTS.template.md` - +140 行，-93 行
- `templates/config.toml.example` - +23 行，-7 行
- `README.md` - +19 行，-5 行

---

### 📋 升级指南

#### 从 v1.0.x 升级

1. **拉取最新代码**
   ```bash
   git pull origin main
   ```

2. **更新配置（二选一）**
   
   首次使用（直接复制）：
   ```bash
   cp templates/AGENTS.template.md ~/.codex/AGENTS.md
   cp templates/config.toml.example ~/.codex/config.toml
   ```
   
   已有配置（手动合并）：
   ```bash
   cp templates/AGENTS.template.md ~/.codex/AGENTS.template.md
   cp templates/config.toml.example ~/.codex/config.toml.template
   # 然后使用 diff 工具合并关键配置
   ```

3. **推荐合并的关键配置项**
   ```toml
   [agents]
   max_threads = 5
   max_depth = 1
   
   [sandbox_workspace_write]
   network_access = true
   ```

4. **验证版本**
   - 确保 Codex CLI 版本为 `v0.111.0`
   - 执行 `codex --version` 检查

---

### ⚠️ 注意事项

1. **并发限制更保守** - 单轮最大并行子任务从 6 个降为 5 个，更稳定
2. **配置结构变更** - 新增 `[sandbox_workspace_write]` 和 `[agents]` 区块
3. **版本依赖** - 基于 Codex CLI `v0.111.0` 验证，低版本可能存在字段差异

---

### 🎓 使用建议

1. **首次使用** - 直接复制模板，跑通一轮后再裁剪规则
2. **团队项目** - 建议评估 `max_threads` 和 `sandbox_mode` 配置
3. **成本敏感** - 可将 `model_reasoning_effort` 降级为 `medium`

---

> 📅 **发布日期**: 2026-03-03  
> 📌 **版本**: v1.1.0  
> 🎯 **主题**: 对话风格与配置标准化
