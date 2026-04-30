# multi-agent-project-template

> **Claude Code 多 Agent 协作开发项目模板**

经过验证的协作框架，帮助新项目快速建立多 Agent 协作开发流程。

---

## 1. 模板定位

本模板是一个**经过验证的 Claude Code 多 Agent 协作开发框架**。

**核心价值**：
- 提供完整的多 Agent 协作流程规范
- 提供三个经过验证的 Agent 模板
- 提供经验知识库，避免重复踩坑
- 提供示例文档，降低上手难度

**重要说明**：
- 本模板**不是业务项目**，不包含具体业务代码
- 本模板提供的是**多 Agent 协作开发流程骨架**
- 需要结合具体项目需求编写业务代码

---

## 2. 模板来源

本模板基于 `todo-agent-workflow-demo` 项目的验证经验提取。

**验证项目**：todo-agent-workflow-demo

**验证成果**：
- 完成任务：21 个（T001-T022）
- 通过率：100%
- 修正循环：1 次（Task 012，1 轮修复成功）
- 协作循环：12 个（T001-T012）
- 文档整理：8 个任务（T013-T020）

**关键经验**：
- ✅ 验证了多 Agent 协作的可行性
- ✅ 验证了独立开发与独立验收流程
- ✅ 验证了修正循环机制
- ✅ 沉淀了可复用的协作经验
- ✅ 发现了 Task 012 的经典踩坑案例（重构破坏历史功能）

---

## 3. 适合什么项目

✅ **适合使用本模板的项目**：

- 需要验证或使用 Claude Code 多 Agent 协作开发的项目
- 需要清晰的 Agent 角色分工和流程规范的项目
- 需要独立开发与独立验收机制的项目
- 需要修正循环机制的项目
- 希望积累多 Agent 协作经验的项目

---

## 4. 不适合什么项目

❌ **不适合使用本模板的项目**：

- 不使用 Claude Code 的项目
- 只需要单一开发者完成的项目
- 不需要独立测试验收的项目
- 项目过于简单，任务少于 3 个

---

## 5. 内置目录结构

```
multi-agent-project-template/
│
├── README.md                           # 本文件
├── template-usage.md                   # 详细使用说明
├── project-bootstrap-checklist.md      # 新项目初始化检查清单
│
├── docs/                               # 流程文档目录
│   ├── workflow.md                     # ✅ 核心流程规范
│   └── examples/                       # ✅ 示例文档
│       ├── requirements.example.md
│       ├── plan.example.md
│       ├── tasks.example.md
│       └── acceptance.example.md
│
├── .claude/                            # Claude Code 配置
│   └── agents/                         # ✅ Agent 模板
│       ├── planner.md
│       ├── developer.md
│       └── tester.md
│
├── memory/                             # ✅ 经验知识库
│   ├── lessons.md                      # 正向经验
│   ├── pitfalls.md                     # 踩坑风险
│   └── skills-candidates.md            # Skill 候选
│
└── reports/                            # 报告目录
    ├── dev/                            # 开发报告
    │   └── .gitkeep
    └── test/                           # 测试报告
        └── .gitkeep
```

**图例说明**：
- ✅ 模板提供的文件，可以直接使用

---

## 6. 内置 Agent 角色

本模板默认包含 4 个 Agent 角色：

### 6.1 主 Agent (Coordinator)

**职责**：任务调度、流程控制、决策协调

**核心任务**：
- 解析任务列表，选择下一个可执行任务
- 将任务分配给开发 Agent
- 协调测试 Agent 进行验收
- 根据测试结果决定下一步行动
- 更新任务状态和工作日志

**关键原则**：
- 不直接编码
- 不直接测试
- 只做调度和决策

---

### 6.2 计划 Agent (Planner)

**职责**：任务拆分、依赖分析、验收标准规划

**核心任务**：
- 读取 `docs/requirements.md` 需求文档
- 将需求拆分为可独立完成的小任务（每个任务 30 分钟内完成）
- 定义任务依赖关系
- 制定清晰、可测试的验收标准
- 评估任务优先级（P0/P1/P2/P3）

**输出文件**：
- `docs/plan.md` - 实施计划
- `docs/tasks.md` - 任务清单
- `docs/acceptance.md` - 验收标准

**关键原则**：
- 不编码
- 不测试
- 不创建业务代码文件

---

### 6.3 开发 Agent (Developer)

**职责**：独立完成分配的开发任务

**核心任务**：
- 读取任务文档和验收标准
- 进行最小必要修改
- 进行自测（基本功能验证）
- 编写开发报告
- 在开发报告中记录 DEV_ID

**输出文件**：
- 修改后的业务代码
- `reports/dev/task-xxx-dev-report.md`

**关键原则**：
- 只处理一个明确任务
- 不擅自扩展功能
- 不修改任务状态

---

### 6.4 测试 Agent (Tester)

**职责**：独立验收开发成果

**核心任务**：
- 根据验收标准逐项测试
- 读取实际代码，不盲信开发报告
- 记录测试结果
- 发现问题时提供详细反馈
- 在测试报告中记录 TEST_ID

**输出文件**：
- `reports/test/task-xxx-test-report.md`

**关键原则**：
- 不能只看开发报告就 PASS
- 必须读取实际代码并逐项对照验收标准
- 不修改业务代码

---

## 7. 标准协作流程

### 7.1 单任务执行流程

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
   ├─► 5. 生成开发报告
   └─► 6. 返回简洁格式给主 Agent
   │
   ▼
分配给 Tester Agent
   │
   ├─► 1. 读取任务文档和验收标准
   ├─► 2. 读取开发报告
   ├─► 3. 读取实际代码
   ├─► 4. 逐项对照验收标准
   ├─► 5. 检查历史功能（重构任务）
   ├─► 6. 判定 PASS / FAIL
   ├─► 7. 生成测试报告
   └─► 8. 返回简洁格式给主 Agent
   │
   ▼
主 Agent 根据测试结果决策
   │
   ├─ PASS → 更新状态 → 下一个任务
   │
   └─ FAIL → 进入修正循环（最多 3 轮）
```

---

## 8. 关键规则

### 8.1 核心原则

**Developer 完成不等于任务完成**：
- Developer 完成 → 生成开发报告 → 等待 Tester 验收
- Tester 验收 → 生成测试报告 → 判定 PASS 或 FAIL
- **只有 Tester PASS 后，任务才算真正完成**

### 8.2 修正循环规则

如果 Tester FAIL → 进入修正循环：
- 最多 3 轮修正
- 谁写的 bug 谁修复（resume 原 Developer）
- 谁提出的 bug 谁复测（resume 原 Tester）
- 第 3 轮失败后，主 Agent 介入处理

### 8.3 信息交接规则

子 Agent 有独立上下文，通过文件系统交接信息：
- Agent 之间通过 `docs/`、`reports/`、`memory/` 交接信息
- 项目文件系统是 Agent 之间的共享工作区

---

## 9. 如何开始使用

### 9.1 快速开始（5 步）

**步骤 1**：复制本模板到新项目目录

```bash
cp -r multi-agent-project-template your-new-project
cd your-new-project
```

**步骤 2**：阅读 `template-usage.md`

了解详细的模板使用说明和协作流程。

**步骤 3**：按 `project-bootstrap-checklist.md` 初始化项目

逐项检查，确保不遗漏关键步骤。

**步骤 4**：编写 `docs/requirements.md`

参考 `docs/examples/requirements.example.md`，描述项目需求。

**步骤 5**：启动 Planner Agent 生成计划

让 Planner 根据需求生成 `docs/plan.md`、`docs/tasks.md`、`docs/acceptance.md`。

**步骤 6**：开始多 Agent 协作开发

主 Agent 开始调度任务，按 `docs/workflow.md` 执行协作流程。

---

### 9.2 详细指引

**快速参考**：
- `template-usage.md` - 详细的使用说明（推荐首先阅读）
- `project-bootstrap-checklist.md` - 新项目初始化检查清单
- `docs/workflow.md` - 核心流程规范（必读）

**示例文档**：
- `docs/examples/requirements.example.md` - 需求文档示例
- `docs/examples/plan.example.md` - 实施计划示例
- `docs/examples/tasks.example.md` - 任务清单示例
- `docs/examples/acceptance.example.md` - 验收标准示例

---

## 10. 重要文件说明

### 10.1 核心流程文档

| 文件 | 说明 | 必读性 |
|------|------|--------|
| `docs/workflow.md` | 多 Agent 协作流程核心规范 | ⭐⭐⭐ 必读 |

### 10.2 Agent 模板

| 文件 | 说明 |
|------|------|
| `.claude/agents/planner.md` | 计划 Agent 模板（613 行，充分验证） |
| `.claude/agents/developer.md` | 开发 Agent 模板（502 行，充分验证） |
| `.claude/agents/tester.md` | 测试 Agent 模板（600 行，充分验证） |

### 10.3 经验知识库

| 文件 | 说明 | 内容量 |
|------|------|--------|
| `memory/lessons.md` | 已验证有效的正向经验 | 587 行，9 个部分 |
| `memory/pitfalls.md` | 踩坑风险和避免方法 | 827 行，11 个部分 |
| `memory/skills-candidates.md` | 未来可抽象为 Skill 的候选 | 519 行，7 个候选 |

**经典案例**：
- Task 012 的 trim() 案例（记录在 `memory/pitfalls.md` 第 10 章）
- 修正循环经验（记录在 `memory/lessons.md` 第 5 章）

### 10.4 报告目录

| 目录 | 说明 |
|------|------|
| `reports/dev/` | 开发报告存放目录 |
| `reports/test/` | 测试报告存放目录 |

**报告格式**：
- `reports/dev/task-xxx-dev-report.md`
- `reports/test/task-xxx-test-report.md`

### 10.5 辅助文档

| 文件 | 说明 |
|------|------|
| `template-usage.md` | 详细的模板使用说明 |
| `project-bootstrap-checklist.md` | 新项目初始化检查清单 |

---

## 11. 后续验证建议

### 11.1 用第二个项目验证模板

**强烈推荐**：使用本模板启动第二个项目，验证模板的稳定性和可复用性。

**第二个项目建议**：
- 选择与 Todo List 不同的业务
- 任务数量建议 5-15 个
- 验证 Agent 模板在不同场景下的适应性
- 记录模板需要调整的地方

### 11.2 向经验库添加新发现

第二个项目运行后：
- 向 `memory/lessons.md` 添加新的正向经验
- 向 `memory/pitfalls.md` 添加新的踩坑案例
- 向 `memory/skills-candidates.md` 添加新的 Skill 候选
- 评估是否需要调整 Agent 模板

### 11.3 验证模板成熟度

通过多个项目验证后，评估模板的成熟度：
- 哪些流程是稳定的，无需修改
- 哪些流程需要调整或补充
- 哪些 Skill 候选值得实现为真正的 Skill

---

## 12. 典型使用场景

### 12.1 场景 1：Web 应用开发

使用模板开发 Web 应用，通过多 Agent 协作：
- Planner 拆分前端开发任务
- Developer 实现页面和功能
- Tester 独立验收每个功能

### 12.2 场景 2：后端 API 开发

使用模板开发后端 API：
- Planner 拆分 API 端点开发任务
- Developer 实现 API 逻辑
- Tester 独立测试 API 响应

### 12.3 场景 3：代码重构项目

使用模板进行代码重构：
- Planner 拆分重构任务，明确不改变功能行为
- Developer 执行重构，进行回归测试
- Tester 重点检查历史功能是否被破坏

---

## 13. 核心优势

### 13.1 经过验证

- 基于 21 个任务的完整验证
- 100% 任务通过率
- 包含 1 次修正循环成功案例

### 13.2 职责清晰

- 四个 Agent 角色分工明确
- 开发与测试完全分离
- 主 Agent 只做调度和决策

### 13.3 质量保证

- 独立验收机制
- 修正循环机制
- 详细的经验库

### 13.4 可复用性

- 提供完整流程规范
- 提供三个 Agent 模板
- 提供示例文档和经验库

---

## 14. 注意事项

### 14.1 本模板不包含

- ❌ 具体业务代码
- ❌ 特定技术栈实现
- ❌ 部署脚本
- ❌ CI/CD 配置

### 14.2 本模板包含

- ✅ 多 Agent 协作流程规范
- ✅ 三个 Agent 模板
- ✅ 经验知识库
- ✅ 示例文档

### 14.3 使用前提

- 熟悉 Claude Code 基本操作
- 了解多 Agent 协作概念
- 愿意遵循模板规范

---

## 15. 相关链接

**验证项目**：
- todo-agent-workflow-demo（21 个任务，100% 通过率）

**核心文档**：
- `template-usage.md` - 详细使用说明
- `docs/workflow.md` - 核心流程规范

**检查清单**：
- `project-bootstrap-checklist.md` - 新项目初始化检查清单

---

**模板版本**: v1.0

**创建日期**: 2026-04-30

**基于项目**: todo-agent-workflow-demo（T001-T022 完整验证）

**适用场景**: Claude Code 多 Agent 协作开发项目

**维护状态**: 活跃维护，持续优化
