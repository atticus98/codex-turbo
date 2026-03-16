# 发布日志

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
