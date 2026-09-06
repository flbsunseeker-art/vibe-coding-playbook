# Vibe Coding 项目开发 SOP

> 核心原则：**人负责方向、判断、边界和最终验收；AI / Codex 负责执行、验证、补全和提效。**

Vibe Coding 不是把一句想法丢给 AI 写代码，而是让 AI 在明确的产品目标、项目规则和验证标准下，把「想法 → MVP → 可交付产品」稳定推进。

---

## 0. 总体流程

```txt
0. 项目初始化：Git + 基础 AGENTS.md
1. 产品定位：形成 PRD 草稿
2. 视觉设计：形成 UI 原型与 DESIGN.md
3. 开发准备：形成 ARCHITECTURE.md + TODO.md，并补全 AGENTS.md
4. 正式开发：小步实现 → AI 自测 → Review → Local Commit → 人工验收
5. 变更控制：先更新方案，再做大改
6. 发布验证：完整验证 → 部署 / 远端同步
7. 交付沉淀：README + Demo + 复盘
```

---

# 0. 项目初始化：先建立可回滚环境

每个新项目开始时，先让 AI 完成基础工程初始化。

```txt
git init（如果当前还不是 Git 仓库）
→ 创建 .gitignore
→ 创建基础 AGENTS.md
→ 建立 docs/ 等基础目录
→ 检查 Git 状态
```

建议在基础项目骨架建立后创建第一个本地 Commit：

```bash
git add .
git commit -m "chore: initialize project"
```

### Git 基本原则

- Git 是 AI Coding 的**可恢复 checkpoint**，不只是代码托管工具。
- 不要求每次细小修改都 Commit。
- **每完成一个独立、可验证的任务单元，并通过相关验证后，创建一次本地 Commit。**
- Commit message 简洁说明本次核心改动，方便后续追踪和回滚。
- 本地 Commit 可由 AI 自动完成，不需要每次确认。
- `push / force-push / merge / publish` 等远端操作必须先获得用户明确确认。
- 不提交 `.env`、API Key、Token、密码等敏感信息。
- 不执行 `git reset --hard`、`push --force` 等破坏性操作，除非明确授权。

推荐 Commit：

```txt
feat: add portfolio import flow
fix: handle invalid stock symbols
test: add calculation regression coverage
refactor: simplify quote service
docs: update product scope
```

> 项目刚开始时的 `AGENTS.md` 可以先保持基础版本；PRD 和技术方案明确后，再由 AI 自动补全项目规则。

---

# 1. 产品定位：形成 PRD 草稿

这一阶段的目标不是写代码，而是先把产品想清楚。

先和 AI 脑暴讨论，逐步明确：

- 这个产品解决什么问题？
- 目标用户是谁？
- 用户现在怎么解决？现有方案有什么不足？
- 有哪些竞品或参考方案？
- 产品的差异化价值是什么？
- MVP 最小可交付边界是什么？哪些功能暂时不做？
- 最终发布形态是什么？
- 技术上大致能不能实现？主要依赖和风险是什么？
- API、部署、时间等成本是否可控？

这里的技术讨论只做**可行性初判**，不展开详细架构。

最终产出：

```txt
docs/PRD.md
```

建议包含：

```md
# PRD

## 1. 产品一句话
这个产品是什么？为谁解决什么问题？

## 2. 目标用户与场景
谁会用？在什么场景下使用？

## 3. 用户痛点
当前最值得解决的问题是什么？

## 4. 现有方案与不足
用户现在如何解决？为什么还不够好？

## 5. 产品价值主张
相比现有方案，我们强在哪里？

## 6. MVP 范围
### 必做
- 功能 1
- 功能 2

### 暂不做
- 功能 3
- 功能 4

## 7. 核心用户流程
用户从进入产品到完成目标的完整路径。

## 8. 技术可行性初判
- 大致实现方式：
- 主要依赖：
- 明显风险：
- 成本是否可控：

## 9. 验收标准
什么情况下，这个 MVP 算完成。
```

这一阶段结束后，应该得到的是一个**可以指导后续设计与开发的产品方案初稿**。

---

# 2. 视觉设计：形成 UI 原型

目标是把产品方案变成可感知的界面和交互。

不要只告诉 AI“做得好看”，更好的方式是：

```txt
找参考
→ AI 提炼视觉语言
→ 形成页面结构与关键交互
→ 生成 / 打磨 UI 原型
→ 沉淀 DESIGN.md
```

可以参考 Dribbble、Mobbin、Linear、Vercel、Raycast、v0、Pinterest 或同类产品截图。

最终产出：

```txt
docs/DESIGN.md
```

建议记录：

- 视觉关键词与色彩风格
- 页面结构
- 核心组件
- 关键交互
- Loading / Empty / Error 状态
- UI 原型、截图或参考链接

---

# 3. 开发准备：固化项目边界

这一步才正式进入技术方案，并让 Codex 在清晰边界下开发。

推荐项目结构：

```txt
docs/
  PRD.md
  DESIGN.md
  ARCHITECTURE.md
  TODO.md

AGENTS.md
README.md
```

## 3.1 生成 ARCHITECTURE.md

建议明确：

```md
# Architecture

## 技术栈
- Frontend:
- Backend:
- Database:
- AI API:
- Deployment:

## 目录结构
定义主要目录及职责。

## 核心模块
定义模块边界和依赖关系。

## 数据模型
定义核心对象和字段。

## API 设计
定义核心接口。

## 开发约束
明确哪些东西不做，以及哪些边界不能随意突破。
```

短周期 MVP 优先：

- 简单方案优于过度设计
- 少依赖、少状态、少复杂权限
- 先保证核心用户流程完整

## 3.2 补全项目级 AGENTS.md

`AGENTS.md` 是 Codex 的项目级工作说明书，应在 PRD 和 Architecture 确定后补全。

至少包含：

```txt
Project Goal
Must Read Before Coding
Development Rules
Git Rules
Verification Rules
Commands
Definition of Done
```

其中最关键的规则：

```txt
Local Commit：验证通过后可自动执行
Remote Push：必须用户确认

每个任务交付前必须完成与风险匹配的验证
验证失败时不得宣称任务完成
```

## 3.3 生成 TODO.md

让 Codex 基于 `PRD.md + DESIGN.md + ARCHITECTURE.md` 拆成可以逐项完成和验证的任务。

```md
# TODO

## Phase 1：项目骨架
- [ ] 初始化核心工程
- [ ] 建立基础页面和目录

## Phase 2：核心功能
- [ ] 功能 A
- [ ] 功能 B

## Phase 3：体验完善
- [ ] Loading / Empty / Error
- [ ] UI Polish

## Phase 4：发布准备
- [ ] 核心流程验证
- [ ] Build
- [ ] 部署
- [ ] README
```

TODO 的粒度应满足：**一个任务可以独立实现、验证和 Commit。**

---

# 4. 正式开发：实现与验证属于同一个 Task

不要采用：

```txt
AI 写完代码 → 交给人测试
```

更推荐：

```txt
选择一个 TODO Task
→ Codex 实现
→ 判断是否需要新增 / 更新测试
→ 执行与风险匹配的 AI 自测
→ 修复发现的问题
→ Review Diff
→ Local Git Commit
→ 人工验收
→ 下一个 Task
```

## 4.1 测试原则：每次都要验证，但不要求每次都新增测试

测试强度应该和改动风险匹配，而不是为了测试而测试。

例如：

| 改动类型 | 推荐验证方式 |
| --- | --- |
| 文案 / Markdown | 内容检查 |
| 简单 UI / CSS | 页面运行 + 视觉检查 |
| 纯逻辑函数 | Unit Test |
| Bug 修复 | 复现验证 + 必要时补 Regression Test |
| API / 数据链路 | Integration / API Test |
| 核心用户流程 | 实际跑通核心 Flow / E2E |
| 大范围 Refactor | 原有测试 + Relevant Test Suite |

可使用的验证手段包括：

```txt
lint / typecheck / build
unit / integration / regression tests
运行时检查
真实用户流程验证
Browser / Computer Use / Simulator 等可用工具
```

**具体使用什么工具由项目和改动决定，不强制使用 Computer Use 或任何特定插件。**

## 4.2 独立 QA Agent：按复杂度启用

独立 QA Agent 有价值，但不作为所有任务的默认流程。

```txt
简单任务：Main Agent 实现 + 自测

中高复杂度 / 高风险任务：
Main Agent 实现
→ QA Sub Agent 独立 Review / 测试
→ Main Agent 修复
→ Regression
→ Commit
```

推荐 QA Agent 默认只负责：

- 阅读 PRD / Architecture / Diff
- 跑测试
- 验证核心流程
- 找 Bug 和风险

默认不要和 Main Agent 同时修改同一个 working tree；由 Main Agent 根据 QA 结论完成修复。

## 4.3 Definition of Done

一个 Task 只有满足以下条件才算完成：

```txt
功能符合需求
+ 必要测试已新增 / 更新
+ 相关验证全部通过
+ 无已知阻塞问题
+ Diff 已 Review
+ 已创建可回滚的 Local Commit
```

AI 在相关验证失败时，不应向用户宣称“已完成”。

---

# 5. 变更控制：防止 MVP 失控

开发过程中出现新需求时，先判断改动级别。

```txt
小改动
→ 不影响产品定位 / 核心流程 / 数据模型 / 技术架构
→ 可以直接加入 TODO

大改动
→ 影响上述任一关键边界
→ 先更新 PRD / DESIGN / ARCHITECTURE
→ 再重新拆 TODO
→ 再开始实现
```

原则：**方案先变，代码后变。**

---

# 6. Review / Refactor

不要让 AI 在实现功能的同时顺手进行大范围重构。

Review 重点：

```txt
1. 是否符合 PRD
2. 是否违反 Architecture
3. 是否修改了无关代码
4. 是否有重复或过度复杂逻辑
5. 是否有遗漏的异常状态
6. 是否存在安全 / 隐私风险
7. 测试是否覆盖了本次核心风险
```

Refactor 应遵循：

```txt
最小范围
不改变功能表现
不引入无必要依赖
修改后重新执行相关验证
```

---

# 7. 发布验证：最后一次完整检查

因为测试已经进入日常开发循环，发布阶段不再承担“第一次测试”，而是做最终 Release Verification。

上线前至少确认：

```txt
✓ 核心用户流程完整跑通
✓ Relevant / Full Test Suite 通过
✓ lint / typecheck / build 通过（如项目适用）
✓ 没有明显 console / runtime error
✓ 环境变量和生产配置正确
✓ 敏感信息未进入 Git
✓ 部署环境实际可访问
```

如果需要同步 GitHub 或其他远端仓库：

> **Push Remote 前必须获得用户明确确认。**

---

# 8. 交付沉淀

项目完成后，至少补齐：

```txt
README.md
docs/DEMO_SCRIPT.md（需要展示时）
```

README 建议包含：

- 一句话介绍
- Demo / Screenshots
- 核心功能
- 产品亮点
- 技术栈
- 本地运行方式
- 环境变量说明
- 核心产品 / 技术取舍
- 后续规划

---

# 9. 最终推荐 SOP

```txt
0. 初始化项目：Git + .gitignore + 基础 AGENTS.md
1. 和 AI 脑暴产品方向
2. 明确定位、用户、痛点、MVP 和技术可行性
3. 输出 docs/PRD.md
4. 收集 UI 参考并形成原型
5. 输出 docs/DESIGN.md
6. 输出 docs/ARCHITECTURE.md
7. 补全项目级 AGENTS.md
8. 生成 docs/TODO.md
9. 按 TODO 小步开发
10. 每个 Task：实现 → 必要测试 → AI 自测 → 修复 → Review → Local Commit
11. 是否使用 Computer Use / QA Sub Agent 等，根据任务风险和复杂度决定
12. 大需求先更新方案文档，再改代码
13. 人工验收最终产品效果
14. 发布前完成 Release Verification
15. Push Remote 前由用户确认
16. 补 README / Demo Script，并复盘更新文档
```

---

# 10. 一句话总结

> 最好的 Vibe Coding，不是让 AI 替你思考，而是让人负责方向与最终判断，让 AI 在清晰边界下自主完成「实现 → 验证 → 修复 → 留痕」。
>
> Git 让 AI Coding **可回退**，AI Self-Test 让它 **更可信**，而人的最终验收确保我们做出来的是**真正想要的产品**。
