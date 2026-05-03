# 模板使用说明

本文档说明如何使用 `multi-agent-project-template` 启动一个新的 Claude Code 多 Agent 协作开发项目。

---

## 1. 模板定位

本模板提供了一个**经过验证的 Claude Code 多 Agent 协作开发框架**。

**来源**：基于 `todo-agent-workflow-demo` 项目的验证经验（21 个任务，100% 通过率）提取。

**核心价值**：
- 提供完整的多 Agent 协作流程规范
- 提供三个经过验证的 Agent 模板
- 提供经验知识库，避免重复踩坑
- 提供示例文档，降低上手难度

**重要说明**：
- 本模板是**协作框架模板**，不是业务代码模板
- 本模板用于 Claude Code 多 Agent 协作开发
- 需要结合具体项目需求编写业务代码

---

## 2. 适用场景

✅ **适合使用本模板的场景**：

- 需要验证或使用 Claude Code 多 Agent 协作开发的项目
- 需要清晰的 Agent 角色分工和流程规范的项目
- 需要独立开发与独立验收机制的项目
- 需要修正循环机制的项目
- 希望积累多 Agent 协作经验的项目

---

## 3. 不适用场景

❌ **不适合使用本模板的场景**：

- 不使用 Claude Code 的项目
- 只需要单一开发者完成的项目
- 不需要独立测试验收的项目
- 项目过于简单，任务少于 3 个

---

## 4. 使用前准备

### 4.1 必读文件

在使用模板前，强烈建议阅读以下文件：

**核心流程规范**：
- `docs/workflow.md`（必读）- 多 Agent 协作流程核心规范

**Agent 模板**：
- `.claude/agents/planner.md` - 计划 Agent 模板
- `.claude/agents/developer.md` - 开发 Agent 模板
- `.claude/agents/tester.md` - 测试 Agent 模板

**经验库**：
- `memory/lessons.md` - 已验证有效的正向经验
- `memory/pitfalls.md` - 踩坑风险和避免方法（包含 Task 012 经典案例）
- `memory/skills-candidates.md` - 未来可抽象为 Skill 的候选

### 4.2 环境准备

**Windows PowerShell 用户**：

如果在 PowerShell 中查看中文文件乱码，需要设置 UTF-8：

```powershell
chcp 65001
[Console]::OutputEncoding = [System.Text.Encoding]::UTF8
Get-Content -Encoding UTF8 docs\workflow.md -TotalCount 40
```

或者优先使用 VS Code 等支持 UTF-8 的工具查看文件。

---

## 5. 推荐目录结构

使用模板初始化项目后，目录结构如下：

```
your-project/
│
├── docs/                           # 项目文档目录
│   ├── workflow.md                 # ✅ 核心流程规范（模板提供）
│   ├── requirements.md             # 📝 需求文档（你编写）
│   ├── plan.md                     # 📝 实施计划（Planner 生成）
│   ├── tasks.md                    # 📝 任务清单（Planner 生成）
│   ├── acceptance.md               # 📝 验收标准（Planner 生成）
│   └── examples/                   # ✅ 示例文档（模板提供）
│       ├── requirements.example.md
│       ├── plan.example.md
│       ├── tasks.example.md
│       └── acceptance.example.md
│
├── .claude/                        # Claude Code 配置
│   └── agents/                     # ✅ Agent 模板（模板提供）
│       ├── planner.md
│       ├── developer.md
│       └── tester.md
│
├── memory/                         # ✅ 经验知识库（模板提供）
│   ├── lessons.md
│   ├── pitfalls.md
│   └── skills-candidates.md
│
├── reports/                        # 报告目录
│   ├── dev/                        # 📝 开发报告（运行时生成）
│   │   └── .gitkeep
│   └── test/                       # 📝 测试报告（运行时生成）
│       └── .gitkeep
│
└── template-usage.md               # ✅ 本文档（模板提供）
```

**图例说明**：
- ✅ 模板提供的文件，可以直接使用
- 📝 需要你创建或生成的文件

---

## 6. 初始化新项目步骤

### 步骤 1: 复制模板到新项目目录

```bash
# 复制整个模板目录到新位置
cp -r multi-agent-project-template your-new-project
cd your-new-project
```

或手动复制模板目录并重命名。

### 步骤 2: 编写需求文档

创建 `docs/requirements.md`，描述项目目标、功能需求、技术约束。

参考：`docs/examples/requirements.example.md`

### 步骤 3: 启动 Planner Agent 拆分任务

将需求文档交给 Planner Agent，让 Planner 拆分任务并生成：
- `docs/plan.md` - 实施计划
- `docs/tasks.md` - 任务清单
- `docs/acceptance.md` - 验收标准

参考：`docs/examples/` 中的其他示例文档

### 步骤 4: 检查任务清单和验收标准

检查 `docs/tasks.md` 和 `docs/acceptance.md`，确保：
- 任务粒度合理（每个任务 30 分钟内完成）
- 验收标准清晰、可测试
- 依赖关系明确

### 步骤 5: 开始多 Agent 协作开发

主 Agent 开始调度任务，执行标准协作流程。

---

## 7. 编写需求文档

### 7.1 需求文档核心内容

`docs/requirements.md` 应包含：

**项目说明**：
- 项目名称、类型、目标
- 核心目标和次要目标

**功能需求**：
- 核心功能列表
- 每个功能的简要描述

**非功能需求**：
- 技术约束（如技术栈、框架限制）
- 质量要求

**边界说明**：
- 什么在范围内
- 什么不在范围内

**不做什么**：
- 明确说明本项目不做什么，避免范围蔓延

### 7.2 需求文档模板

参考：`docs/examples/requirements.example.md`

**关键原则**：
- 描述清晰，避免歧义
- 适度约束，不要过度限制实现方式
- 明确边界，避免范围蔓延

---

## 8. 启动 Planner Agent

### 8.1 Planner 的职责

Planner Agent 负责：
- 理解需求文档
- 将需求拆分为可独立完成的小任务（每个任务 30 分钟内完成）
- 定义任务依赖关系
- 制定清晰、可测试的验收标准
- 评估任务优先级（P0/P1/P2/P3）

### 8.2 Planner 的输出

Planner Agent 会生成：
- `docs/plan.md` - 实施计划
- `docs/tasks.md` - 任务清单
- `docs/acceptance.md` - 验收标准

### 8.3 使用 Planner 的建议

**给 Planner 的提示**：
- 强调任务粒度：每个任务应在 30 分钟内完成
- 强调验收标准：必须明确、可测试，避免模糊描述
- 强调依赖关系：写清任务之间的依赖
- 如需重构任务，强调必须做历史功能回归检查

**Planner 输出检查**：
- 任务数量是否合理（建议 5-20 个任务）
- 任务粒度是否合适
- 验收标准是否清晰
- 依赖关系是否明确

---

## 9. 执行 Developer / Tester 协作流程

### 9.1 标准工作流程

```
主 Agent 选择任务
   │
   ▼
分配给 Developer Agent
   │
   ├─► 1. 读取任务文档和验收标准
   ├─► 2. 读取 memory 文件（避免踩坑）
   ├─► 3. 进行最小必要修改
   ├─► 4. 自测（基本功能验证）
   ├─► 5. 生成开发报告（reports/dev/task-xxx-dev-report.md）
   └─► 6. 返回简洁格式给主 Agent
   │
   ▼
分配给 Tester Agent
   │
   ├─► 1. 读取任务文档和验收标准
   ├─► 2. 读取开发报告（了解 Developer 声称做了什么）
   ├─► 3. 读取实际代码（确认实际做了什么）
   ├─► 4. 逐项对照验收标准
   ├─► 5. 检查历史功能是否被破坏（重构任务）
   ├─► 6. 判定 PASS / FAIL
   ├─► 7. 生成测试报告（reports/test/task-xxx-test-report.md）
   └─► 8. 返回简洁格式给主 Agent
   │
   ▼
主 Agent 根据测试结果决策
   │
   ├─ PASS → 更新状态 → 下一个任务
   │
   └─ FAIL → 进入修正循环（最多 3 轮）
```

### 9.2 核心规则

**Developer 完成不等于任务完成**：
- Developer 完成 → 生成开发报告 → 等待 Tester 验收
- Tester 验收 → 生成测试报告 → 判定 PASS 或 FAIL
- **只有 Tester PASS 后，任务才算真正完成**

**修正循环规则**：
- 如果 Tester FAIL → 进入修正循环
- 最多 3 轮修正
- 谁写的 bug 谁修复（resume 原 Developer）
- 谁提出的 bug 谁复测（resume 原 Tester）

**信息交接方式**：
- 子 Agent 有独立上下文，通过文件系统交接信息
- Agent 之间通过 `docs/`、`reports/`、`memory/` 交接信息

---

## 10. 修正循环处理

### 10.1 修正循环触发条件

Tester Agent 返回 `RESULT=fail`

### 10.2 修正循环流程

```
测试失败
   │
   ▼
主 Agent 通知原开发 Agent（通过 DEV_ID resume）
   │
   ▼
开发 Agent 阅读测试报告
   │
   ▼
开发 Agent 修复问题
   │
   ▼
开发 Agent 更新开发报告（追加修复记录）
   │
   ▼
原测试 Agent（通过 TEST_ID resume）重新验收
   │
   ▼
   ├─ 通过 → 结束循环，沉淀经验（如有）
   └─ 失败 → 轮次+1，继续下一轮
```

### 10.3 修正循环上限

- 最多 3 轮修正
- 第 3 轮失败后，主 Agent 介入处理

### 10.4 修正循环后的经验沉淀

修正循环结束后，判断是否需要沉淀经验：
- 如果是因为**遗漏需求**导致的失败 → 沉淀到 `memory/pitfalls.md`
- 如果是因为**重构破坏历史功能**导致的失败 → 沉淀到 `memory/pitfalls.md`
- 如果形成了**可复用的修复方法** → 沉淀到 `memory/lessons.md`

---

## 11. 经验沉淀方式

### 11.1 memory/lessons.md

**记录内容**：已经验证有效、后续值得复用的正向经验

**何时记录**：
- 每次形成可复用的成功经验
- 每次发现可以标准化的流程
- 每次有效的测试方法
- 每次好的代码组织方式

**记录格式**：参考 `memory/lessons.md` 现有格式

### 11.2 memory/pitfalls.md

**记录内容**：错误细节、踩坑案例、风险模式、避免方法

**何时记录**：
- 每次出现 bug 导致返工
- 每次误改业务代码
- 每次遗漏需求细节
- 重构引发的历史功能破坏
- 修正循环失败（主 Agent 介入）

**记录格式**：参考 `memory/pitfalls.md` 现有格式

**经典案例**：Task 012 的 trim() 案例（已记录在 `memory/pitfalls.md` 第 10 章）

### 11.3 memory/skills-candidates.md

**记录内容**：未来可能抽象为 Claude Code Skill 的候选流程和方法

**何时记录**：
- 发现可复用的开发流程
- 发现可复用的测试方法
- 发现可复用的检查清单
- 发现可复用的报告模板

**记录格式**：参考 `memory/skills-candidates.md` 现有格式

**当前候选**：7 个（workflow-controller、task-report-generator、fix-loop-controller、agent-id-recorder、regression-test-checklist、memory-updater、project-summary-generator）

---

## 12. Skill 候选记录

### 12.1 当前候选列表

本模板的 `memory/skills-candidates.md` 记录了 7 个候选 Skill：

1. **workflow-controller** - 控制主 Agent 按照固定流程执行
2. **task-report-generator** - 生成标准化的开发报告和测试报告
3. **fix-loop-controller** - 控制测试失败后的修正循环
4. **agent-id-recorder** - 记录 Agent ID 用于修正循环
5. **regression-test-checklist** - 自动生成回归测试清单
6. **memory-updater** - 自动沉淀经验到 memory/
7. **project-summary-generator** - 自动生成项目总结

### 12.2 当前阶段策略

**只记录候选，不立即实现**：
- 当前阶段只记录到文档，作为 Skill 候选
- 不立即创建真正的 Claude Code Skill
- 经过多个项目验证后，再评估哪些候选值得实现

---

## 13. 常见注意事项

### 13.1 核心原则

**职责清晰**：
- 主 Agent：调度和决策，不编码、不测试
- Planner Agent：任务拆分和验收标准制定，不编码
- Developer Agent：开发一个明确任务，不测试、不修改状态
- Tester Agent：独立验收，不修改代码、不修改状态

**最小必要修改**：
- Developer 只做当前任务需要的内容
- 验收标准写什么，就做什么
- 不擅自扩展功能

**独立验收**：
- Tester 不能只看开发报告就 PASS
- 必须读取实际代码并逐项对照验收标准
- Task 012 证明了独立验收的价值

**重构任务防护**：
- 重构必须做历史功能回归检查
- 对"用户输入"保持原值，不要擅自使用 trim()、toLowerCase()
- 完整的代码案例记录在 `memory/pitfalls.md` 第 10 章

### 13.2 Git 提交注意事项

**不要提交本地私有配置**：
- `.claude/settings.local.json` 是本地配置文件
- 应该在 `.gitignore` 中添加此文件
- 避免将个人配置提交到 Git

**Windows LF / CRLF 警告**：
- 在 Windows 上，Git 可能提示 "LF will be replaced by CRLF"
- 这通常是行尾符转换的警告，不是业务错误
- 一般可以忽略

### 13.3 PowerShell 中文文件查看

如果查看中文文件时出现乱码：
```powershell
chcp 65001
[Console]::OutputEncoding = [System.Text.Encoding]::UTF8
Get-Content -Encoding UTF8 docs\workflow.md -TotalCount 40
```

或优先使用 VS Code 等支持 UTF-8 的工具查看文件。

---

## 14. 推荐后续验证

### 14.1 用第二个项目验证模板

**强烈推荐**：使用本模板启动第二个项目，验证模板的稳定性和可复用性。

**第二个项目建议**：
- 选择与 Todo List 不同的业务
- 任务数量建议 5-15 个
- 验证 Agent 模板在不同场景下的适应性
- 记录模板需要调整的地方

### 14.2 向经验库添加新发现

第二个项目运行后：
- 向 `memory/lessons.md` 添加新的正向经验
- 向 `memory/pitfalls.md` 添加新的踩坑案例
- 向 `memory/skills-candidates.md` 添加新的 Skill 候选
- 评估是否需要调整 Agent 模板

### 14.3 验证模板成熟度

通过多个项目验证后，评估模板的成熟度：
- 哪些流程是稳定的，无需修改
- 哪些流程需要调整或补充
- 哪些 Skill 候选值得实现为真正的 Skill

---

## 附录：快速参考

### Agent 角色快速参考

| Agent | 职责 | 输入 | 输出 |
|-------|------|------|------|
| 主 Agent | 调度和决策 | `docs/tasks.md`、测试报告 | 任务分配、状态更新 |
| Planner Agent | 任务拆分 | `docs/requirements.md` | `docs/plan.md`、`docs/tasks.md`、`docs/acceptance.md` |
| Developer Agent | 开发任务 | 任务文档、验收标准、memory | 业务代码、`reports/dev/` |
| Tester Agent | 独立验收 | 任务文档、验收标准、开发报告、业务代码 | `reports/test/` |

### 文件路径快速参考

| 文件/目录 | 用途 | 谁创建/修改 |
|-----------|------|------------|
| `docs/requirements.md` | 需求文档 | 你编写 |
| `docs/plan.md` | 实施计划 | Planner 生成 |
| `docs/tasks.md` | 任务清单 | Planner 生成，主 Agent 更新状态 |
| `docs/acceptance.md` | 验收标准 | Planner 生成 |
| `docs/workflow.md` | 核心流程规范 | 模板提供，不要修改 |
| `.claude/agents/*.md` | Agent 模板 | 模板提供，不要修改 |
| `memory/*.md` | 经验知识库 | 模板提供，可追加新经验 |
| `reports/dev/` | 开发报告 | Developer 生成 |
| `reports/test/` | 测试报告 | Tester 生成 |

### 核心流程口诀

- Developer 完成不等于任务完成
- 只有 Tester PASS 后任务才算完成
- 谁写的 bug 谁修复，谁提出的 bug 谁复测
- 最多 3 轮修正循环
- 重构任务必须做历史功能回归检查

---

## 15. 特殊任务类型建议

### 15.1 README 任务

**经验**：README.md 编写任务不应该读取所有历史 reports 全文。

**推荐做法**：
1. **优先读取核心文档**：
   - `docs/requirements.md` - 了解需求
   - `docs/tasks.md` - 了解任务状态
   - `docs/workflow.md` - 了解协作流程
   - `worklog.md` - 了解整体进展

2. **选择性读取核心代码**：
   - 对于前端项目：`index.html`、`style.css`、`script.js`
   - 对于后端项目：主要入口文件和核心逻辑

3. **报告目录只统计数量**：
   - 使用 `ls` 或 `dir` 统计报告文件数量
   - 不读取全部报告内容

**原因**：大量上下文可能导致 Claude Code 长时间 thinking 或卡住。

**来源**：mini-notes-agent-demo T012 经验

---

### 15.2 优化任务

**经验**：优化类任务最容易越界，必须有明确边界。

**推荐做法**：
1. **明确允许的优化范围**：
   - 轻量样式调整（颜色、间距、字体大小）
   - 轻量交互改进（hover 效果、focus 状态）
   - 代码注释改进
   - 变量命名优化

2. **明确禁止的改动**：
   - 重写业务逻辑
   - 改变历史功能行为
   - 改动数据结构
   - 提前实现扩展功能

3. **验收标准必须包含**：
   - "不允许改变历史功能行为"
   - "不允许改动数据结构"
   - "不允许提前实现后续功能"

**来源**：mini-notes-agent-demo T011 经验

---

### 15.3 验证性质任务

**经验**：如果前序任务已经实现目标功能，后续任务可以是"确认 + 最小补强"。

**推荐做法**：
1. 先检查前序任务是否已经实现了目标功能
2. 如果已实现，确认当前功能正常
3. 只做最小必要的补强（如添加注释、改进可读性）
4. 在报告中明确说明"前序任务已实现，本次为确认"
5. 不要为了"有改动"而强行重写代码

**来源**：mini-notes-agent-demo T009 经验

---

**文档版本**: v1.1

**创建日期**: 2026-04-30

**更新日期**: 2026-05-03

**基于项目**: todo-agent-workflow-demo（21 个任务，100% 通过率）、mini-notes-agent-demo（12 个任务，100% 通过率）

**适用场景**: Claude Code 多 Agent 协作开发项目
