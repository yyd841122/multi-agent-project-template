# 项目初始化检查清单

本文档提供使用 `multi-agent-project-template` 初始化新项目的分步检查清单。

按顺序完成各阶段检查项，确保不遗漏关键步骤。

---

## 1. 使用说明

**适用场景**：使用 multi-agent-project-template 启动新的 Claude Code 多 Agent 协作开发项目。

**使用方法**：
1. 按顺序完成各阶段检查项
2. 每完成一项，在 [ ] 中标记为 [x]
3. 遇到阻塞问题时，参考 `template-usage.md` 或 `docs/workflow.md`

**推荐工作流**：
- 完成阶段 1-3 后，开始编写需求文档
- 完成阶段 4-6 后，开始多 Agent 协作开发
- 阶段 7-10 在开发过程中持续进行
- 阶段 11 在所有任务完成后进行

---

## 2. 阶段 1：复制模板

### 2.1 基础目录检查

- [ ] 复制 `multi-agent-project-template` 到新项目目录
- [ ] 重命名为新项目名称
- [ ] 确认 `docs/` 目录存在
- [ ] 确认 `docs/examples/` 目录存在
- [ ] 确认 `.claude/agents/` 目录存在
- [ ] 确认 `memory/` 目录存在
- [ ] 确认 `reports/dev/` 目录存在
- [ ] 确认 `reports/test/` 目录存在

### 2.2 核心文件检查

- [ ] 确认 `docs/workflow.md` 存在（核心流程规范）
- [ ] 确认 `.claude/agents/planner.md` 存在
- [ ] 确认 `.claude/agents/developer.md` 存在
- [ ] 确认 `.claude/agents/tester.md` 存在
- [ ] 确认 `memory/lessons.md` 存在
- [ ] 确认 `memory/pitfalls.md` 存在
- [ ] 确认 `memory/skills-candidates.md` 存在

### 2.3 辅助文档检查

- [ ] 确认 `template-usage.md` 存在（模板使用说明）
- [ ] 确认 `project-bootstrap-checklist.md` 存在（本文档）

### 2.4 示例文档检查

- [ ] 确认 `docs/examples/requirements.example.md` 存在
- [ ] 确认 `docs/examples/plan.example.md` 存在
- [ ] 确认 `docs/examples/tasks.example.md` 存在
- [ ] 确认 `docs/examples/acceptance.example.md` 存在

---

## 3. 阶段 2：初始化 Git

### 3.1 Git 仓库初始化

- [ ] 在项目根目录执行 `git init`
- [ ] 检查 `.gitignore` 文件是否存在
- [ ] 如不存在，创建 `.gitignore` 并添加以下内容：

```gitignore
# Claude Code 本地配置
.claude/settings.local.json

# 操作系统文件
.DS_Store
Thumbs.db

# 编辑器配置
.vscode/
.idea/
*.swp
*.swo

# 临时文件
*.tmp
*.log
```

### 3.2 Git 配置检查

- [ ] 确认 `.claude/settings.local.json` 在 `.gitignore` 中
- [ ] 确认不会提交本地私有配置文件
- [ ] 执行 `git status` 确认没有不应提交的文件

### 3.3 初始提交

- [ ] 执行 `git add .`
- [ ] 执行 `git commit -m "Initial commit from multi-agent-project-template"`
- [ ] 确认提交成功

---

## 4. 阶段 3：编写需求文档

### 4.1 需求文档创建

- [ ] 参考 `docs/examples/requirements.example.md`
- [ ] 创建 `docs/requirements.md`
- [ ] 编写项目说明
- [ ] 编写用户目标
- [ ] 编写功能需求
- [ ] 编写非功能需求
- [ ] 编写边界说明
- [ ] 编写"不做什么"（避免范围蔓延）
- [ ] 编写可交付物清单

### 4.2 需求文档质量检查

- [ ] 描述清晰，避免歧义
- [ ] 适度约束，不过度限制实现方式
- [ ] 明确边界，避免范围蔓延
- [ ] 功能需求与次要目标区分清楚

### 4.3 需求文档完成确认

- [ ] 需求文档已保存到 `docs/requirements.md`
- [ ] 文档格式规范，易于阅读
- [ ] 文档内容完整，覆盖所有必要信息

---

## 5. 阶段 4：启动 Planner Agent

### 5.1 准备工作

- [ ] 确认已阅读 `docs/workflow.md`（核心流程规范）
- [ ] 确认已阅读 `template-usage.md`（模板使用说明）
- [ ] 确认已阅读 `memory/lessons.md`（正向经验）
- [ ] 确认已阅读 `memory/pitfalls.md`（踩坑风险）

### 5.2 启动 Planner Agent

- [ ] 将需求文档 (`docs/requirements.md`) 提供给 Planner Agent
- [ ] 明确告诉 Planner 任务拆分要求：
  - 每个任务应在 30 分钟内完成
  - 验收标准必须明确、可测试
  - 重构任务必须写明"不改变历史功能行为"

### 5.3 Planner 输出检查

- [ ] Planner 已读取 `docs/requirements.md`
- [ ] Planner 已读取 `docs/workflow.md`
- [ ] Planner 已生成 `docs/plan.md`
- [ ] Planner 已生成 `docs/tasks.md`
- [ ] Planner 已生成 `docs/acceptance.md`

### 5.4 Planner 输出质量检查

- [ ] 任务数量合理（建议 5-20 个任务）
- [ ] 任务粒度合适（每个任务 30 分钟内完成）
- [ ] 任务依赖关系清晰
- [ ] 验收标准明确、可测试
- [ ] 没有使用"美观"、"友好"等模糊词

---

## 6. 阶段 5：检查计划、任务和验收标准

### 6.1 docs/plan.md 检查

- [ ] 实施目标清晰
- [ ] 技术约束明确
- [ ] 阶段划分合理
- [ ] 风险点识别准确
- [ ] 验收策略完整

### 6.2 docs/tasks.md 检查

- [ ] 每个任务都有唯一任务 ID（如 T001、T002）
- [ ] 每个任务都有任务名称
- [ ] 每个任务都有任务描述
- [ ] 每个任务都有优先级（P0/P1/P2/P3）
- [ ] 每个任务都有依赖关系说明
- [ ] 每个任务都有验收要点或验收标准引用
- [ ] 任务足够小（30 分钟内完成）
- [ ] 任务可以独立完成
- [ ] 任务可以独立验收

### 6.3 docs/acceptance.md 检查

- [ ] 整体验收标准清晰
- [ ] 每个任务都有对应验收标准
- [ ] 验收标准明确具体
- [ ] 验收标准可验证
- [ ] 验收标准可测试
- [ ] 包含回归验收要求（重构任务）
- [ ] 包含 PASS / FAIL 判定标准

### 6.4 重构任务专项检查

如有重构类任务（如"代码重构"、"样式重构"）：
- [ ] 任务描述中明确写明"重构不得改变历史功能行为"
- [ ] 任务描述中明确写明"只改代码结构，不改功能行为"
- [ ] 验收标准中包含"历史功能回归测试要求"
- [ ] 验收标准中包含"行为一致性检查要求"

---

## 7. 阶段 6：启动 Developer / Tester 协作流程

### 7.1 主 Agent 调度检查

- [ ] 主 Agent 只分配一个明确任务给 Developer
- [ ] 主 Agent 不直接编码
- [ ] 主 Agent 不直接测试
- [ ] 主 Agent 只做调度和决策

### 7.2 Developer Agent 执行检查

- [ ] Developer 已读取任务文档 (`docs/tasks.md`)
- [ ] Developer 已读取验收标准 (`docs/acceptance.md`)
- [ ] Developer 已读取 `memory/lessons.md`
- [ ] Developer 已读取 `memory/pitfalls.md`
- [ ] Developer 只做当前任务需要的内容
- [ ] Developer 没有擅自扩展功能
- [ ] Developer 没有提前实现后续功能
- [ ] Developer 已生成开发报告 (`reports/dev/task-xxx-dev-report.md`)
- [ ] 开发报告包含 DEV_ID
- [ ] 开发报告包含任务信息、完成内容、自测结果

### 7.3 Tester Agent 验收检查

- [ ] Tester 已读取任务文档 (`docs/tasks.md`)
- [ ] Tester 已读取验收标准 (`docs/acceptance.md`)
- [ ] Tester 已读取开发报告 (`reports/dev/task-xxx-dev-report.md`)
- [ ] Tester 已读取 `memory/lessons.md`
- [ ] Tester 已读取 `memory/pitfalls.md`
- [ ] Tester 已读取实际代码
- [ ] Tester 已逐项对照验收标准
- [ ] Tester 已检查历史功能是否被破坏（重构任务）
- [ ] Tester 已生成测试报告 (`reports/test/task-xxx-test-report.md`)
- [ ] 测试报告包含 TEST_ID
- [ ] 测试报告包含测试信息、验收结果、测试详情

### 7.4 独立验收核心检查

- [ ] Tester 没有只看开发报告就 PASS
- [ ] Tester 已读取实际代码并确认
- [ ] Tester 已独立验收，不盲信 Developer 报告
- [ ] 只有 Tester PASS 后，主 Agent 才标记任务完成

---

## 8. 阶段 7：修正循环检查

### 8.1 修正循环触发检查

如果 Tester 判定 FAIL：
- [ ] 主 Agent 确认测试报告中的失败原因
- [ ] 主 Agent 通过 DEV_ID resume 原 Developer Agent
- [ ] 原 Developer Agent 阅读测试报告
- [ ] 原 Developer Agent 修复问题
- [ ] 原 Developer Agent 更新开发报告（追加修复记录）
- [ ] 主 Agent 通过 TEST_ID resume 原 Tester Agent
- [ ] 原 Tester Agent 复测问题

### 8.2 修正循环规则检查

- [ ] 谁写的 bug 谁修复（resume 原 Developer）
- [ ] 谁提出的 bug 谁复测（resume 原 Tester）
- [ ] 修正循环最多 3 轮
- [ ] 第 1 轮失败 → 第 2 轮
- [ ] 第 2 轮失败 → 第 3 轮
- [ ] 第 3 轮失败 → 主 Agent 介入处理

### 8.3 修正循环后的经验沉淀

修正循环结束后（无论成功还是主 Agent 介入）：
- [ ] 判断是否需要沉淀经验
- [ ] 如果是遗漏需求导致的失败 → 记录到 `memory/pitfalls.md`
- [ ] 如果是重构破坏历史功能导致的失败 → 记录到 `memory/pitfalls.md`
- [ ] 如果形成了可复用的修复方法 → 记录到 `memory/lessons.md`

---

## 9. 阶段 8：报告与日志检查

### 9.1 开发报告检查

- [ ] `reports/dev/` 目录中有开发报告
- [ ] 开发报告文件名格式正确：`task-xxx-dev-report.md`
- [ ] 开发报告包含必要章节：
  - [ ] 任务信息（任务 ID、任务名称、DEV_ID）
  - [ ] 任务描述
  - [ ] 完成内容
  - [ ] 自测结果
  - [ ] 技术要点（可选）
  - [ ] 修复记录（如有）

### 9.2 测试报告检查

- [ ] `reports/test/` 目录中有测试报告
- [ ] 测试报告文件名格式正确：`task-xxx-test-report.md`
- [ ] 测试报告包含必要章节：
  - [ ] 测试信息（任务 ID、测试 Agent、TEST_ID）
  - [ ] 验收结果（PASS / FAIL）
  - [ ] 验收标准测试详情
  - [ ] 发现的问题（如有）
  - [ ] 开发报告核对
  - [ ] 测试结论

### 9.3 子 Agent 输出简洁性检查

- [ ] Developer 返回给主 Agent 的内容简洁
  - [ ] 只返回 `DEV_REPORT=reports/dev/task-xxx-dev-report.md`
  - [ ] 只返回 `STATUS=done`
  - [ ] 只返回 `DEV_ID`
  - [ ] 没有返回大段代码或解释
- [ ] Tester 返回给主 Agent 的内容简洁
  - [ ] 只返回 `TEST_REPORT=reports/test/task-xxx-test-report.md`
  - [ ] 只返回 `RESULT=pass` 或 `RESULT=fail`
  - [ ] 只返回 `TEST_ID`
  - [ ] FAIL 时返回简要原因（不超过 50 字）
  - [ ] 没有返回大段测试详情

### 9.4 工作日志检查

- [ ] 主 Agent 更新 `worklog.md`
- [ ] 每个任务完成后记录任务执行情况
- [ ] 记录交付成果
- [ ] 记录测试结果
- [ ] 记录技术亮点（可选）

---

## 10. 阶段 9：memory 经验沉淀检查

### 10.1 memory/lessons.md 检查

- [ ] 正向经验已写入 `memory/lessons.md`
- [ ] 每条经验包含：
  - [ ] 经验描述
  - [ ] 适用场景
  - [ ] 实施步骤
  - [ ] 相关任务和形成时间
- [ ] 只记录多 Agent 协作相关的正向经验
- [ ] 没有记录普通代码技巧

### 10.2 memory/pitfalls.md 检查

- [ ] 踩坑风险已写入 `memory/pitfalls.md`
- [ ] 每条陷阱包含：
  - [ ] 陷阱描述
  - [ ] 触发场景
  - [ ] 错误示例
  - [ ] 正确做法
  - [ ] 相关任务和发生时间
  - [ ] 避免方法
- [ ] 包含修正循环失败案例（如有）
- [ ] 包含重构破坏历史功能案例（如有）

### 10.3 memory/skills-candidates.md 检查

- [ ] 可复用方法已写入 `memory/skills-candidates.md`
- [ ] 每个候选包含：
  - [ ] 用途（解决什么问题）
  - [ ] 适用场景
  - [ ] 输入和输出
  - [ ] 当前状态（候选 / 待验证 / 可优先实现）
- [ ] 只记录多 Agent 协作相关的方法
- [ ] 没有记录普通代码技巧或优化方法

### 10.4 经验沉淀时机检查

- [ ] 每次修正循环结束后判断是否需要沉淀
- [ ] 每次发现有效方法时建议沉淀
- [ ] 每次发现容易犯错的地方时建议沉淀
- [ ] 不要过度记录，只记录真正有价值的内容

---

## 11. 阶段 10：阶段总结检查

### 11.1 所有任务完成后检查

- [ ] 所有任务状态为 `completed`
- [ ] `docs/tasks.md` 中所有任务已完成
- [ ] `reports/dev/` 中有所有任务的开发报告
- [ ] `reports/test/` 中有所有任务的测试报告

### 11.2 生成项目总结

- [ ] 生成 `reports/project-summary.md`
- [ ] 总结已完成任务
- [ ] 总结关键经验
- [ ] 总结已知风险
- [ ] 总结后续计划

### 11.3 统计数据收集

- [ ] 统计总任务数
- [ ] 统计任务完成率
- [ ] 统计修正循环次数
- [ ] 统计修正成功率
- [ ] 统计开发报告数量
- [ ] 统计测试报告数量

### 11.4 模板反馈收集

- [ ] 记录模板使用中的问题
- [ ] 记录模板需要调整的地方
- [ ] 记录 Agent 模板的适应性
- [ ] 记录经验库的完整性
- [ ] （可选）反馈给模板维护者

---

## 12. 常见禁止事项

### 12.1 Git 相关禁止事项

- [ ] ❌ 不要提交 `.claude/settings.local.json`
- [ ] ❌ 不要提交个人配置文件
- [ ] ❌ 不要提交临时文件

### 12.2 Agent 职责相关禁止事项

- [ ] ❌ 不要让 Developer 修改 `docs/tasks.md` 的任务状态
- [ ] ❌ 不要让 Developer 修改 `docs/acceptance.md` 的验收标准
- [ ] ❌ 不要让 Tester 修改业务代码
- [ ] ❌ 不要让 Planner 修改业务代码

### 12.3 主 Agent 相关禁止事项

- [ ] ❌ 不要让主 Agent 直接编码
- [ ] ❌ 不要让主 Agent 直接测试
- [ ] ❌ 不要让主 Agent 跳过开发报告
- [ ] ❌ 不要让主 Agent 跳过测试报告

### 12.4 流程相关禁止事项

- [ ] ❌ 不要跳过独立验收
- [ ] ❌ 不要无限修正循环（最多 3 轮）
- [ ] ❌ 不要让 Developer 一次性完成整个项目
- [ ] ❌ 不要让 Developer 擅自扩展功能

### 12.5 经验记录相关禁止事项

- [ ] ❌ 不要把普通代码技巧误记为 Skill 候选
- [ ] ❌ 不要在 `memory/lessons.md` 中记录踩坑案例
- [ ] ❌ 不要在 `memory/pitfalls.md` 中记录正向经验
- [ ] ❌ 不要在 `memory/skills-candidates.md` 中记录与多 Agent 协作无关的内容

---

## 13. 启动前最终确认

在开始多 Agent 协作开发前，最后确认以下事项：

### 13.1 文档完整性确认

- [ ] `docs/requirements.md` 已编写
- [ ] `docs/plan.md` 已生成
- [ ] `docs/tasks.md` 已生成
- [ ] `docs/acceptance.md` 已生成
- [ ] `docs/workflow.md` 已阅读
- [ ] `template-usage.md` 已阅读

### 13.2 Agent 模板确认

- [ ] `.claude/agents/planner.md` 已检查
- [ ] `.claude/agents/developer.md` 已检查
- [ ] `.claude/agents/tester.md` 已检查
- [ ] 确认三个 Agent 模板适用于当前项目

### 13.3 经验库确认

- [ ] `memory/lessons.md` 已阅读
- [ ] `memory/pitfalls.md` 已阅读
- [ ] 熟悉 Task 012 的 trim() 案例（重构任务经典踩坑案例）
- [ ] `memory/skills-candidates.md` 已了解

### 13.4 环境准备确认

- [ ] Git 仓库已初始化
- [ ] `.gitignore` 已配置
- [ ] `.claude/settings.local.json` 不会提交
- [ ] PowerShell 中文文件显示正常（如适用）

### 13.5 Windows PowerShell UTF-8 设置（如适用）

如果使用 PowerShell 查看中文文件时出现乱码：

```powershell
chcp 65001
[Console]::OutputEncoding = [System.Text.Encoding]::UTF8
Get-Content -Encoding UTF8 docs\workflow.md -TotalCount 40
```

或优先使用 VS Code 等支持 UTF-8 的工具查看文件。

### 13.6 准备就绪确认

- [ ] 所有前置检查项已完成
- [ ] 没有阻塞问题
- [ ] 可以开始多 Agent 协作开发

---

**检查清单版本**: v1.0

**创建日期**: 2026-04-30

**基于项目**: multi-agent-project-template（来自 todo-agent-workflow-demo）

**适用场景**: Claude Code 多 Agent 协作开发项目初始化
