# 发布日志

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
- 升级适配版本至 **Codex CLI v0.106.0**
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
- `5696e04` - chore: 升级适配版本至 Codex CLI v0.106.0
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
   - 确保 Codex CLI 版本为 `v0.106.0`
   - 执行 `codex --version` 检查

---

### ⚠️ 注意事项

1. **并发限制更保守** - 单轮最大并行子任务从 6 个降为 5 个，更稳定
2. **配置结构变更** - 新增 `[sandbox_workspace_write]` 和 `[agents]` 区块
3. **版本依赖** - 基于 Codex CLI `v0.106.0` 验证，低版本可能存在字段差异

---

### 🎓 使用建议

1. **首次使用** - 直接复制模板，跑通一轮后再裁剪规则
2. **团队项目** - 建议评估 `max_threads` 和 `sandbox_mode` 配置
3. **成本敏感** - 可将 `model_reasoning_effort` 降级为 `medium`

---

> 📅 **发布日期**: 2026-03-03  
> 📌 **版本**: v1.1.0  
> 🎯 **主题**: 对话风格与配置标准化
