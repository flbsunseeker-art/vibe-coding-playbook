# Vibe Coding 项目开发 SOP

> 核心原则：**人负责方向、判断、边界和验收；AI / Codex 负责执行、补全和提效。**

Vibe Coding 不是把一句想法丢给 AI 写代码，而是通过清晰的 SOP，把项目从「产品想法」推进到「可展示的 MVP」。

---

## 0. 总体流程

```txt
1. 产品定位，形成 PRD 草稿
2. 视觉设计，形成 UI 原型
3. 开发准备，固化项目文档
4. 正式开发，小步迭代
5. 测试部署，闭环交付
```

---

# 1. 产品定位：形成 PRD 草稿

这一阶段的目标不是写代码，而是先把产品想清楚。

你可以先和 AI 脑暴讨论，逐步明确：

- 这个产品解决什么问题？
- 目标用户是谁？
- 用户现在怎么解决这个问题？
- 现有方案有什么不足？
- 竞品是谁？有什么可以借鉴？
- 我们的差异化价值是什么？
- MVP 最小可交付范围是什么？
- 哪些功能这版坚决不做？
- 发布形态是什么：网页、小程序、插件、App，还是内部工具？
- 成本是否可控：API 成本、服务器成本、时间成本？
- 技术上大致能不能实现？有没有明显风险？

注意：这里的技术判断只做**可行性初判**，不展开详细架构。

最终产出：

```txt
docs/PRD.md
```

建议 PRD 包含：

```md
# PRD

## 1. 产品一句话

这个产品是什么？为谁解决什么问题？

## 2. 目标用户

核心用户是谁？在什么场景下使用？

## 3. 用户痛点

用户现在遇到的主要问题是什么？

## 4. 现有方案与不足

用户现在如何解决？为什么还不够好？

## 5. 产品价值主张

我们的产品相比现有方案强在哪里？

## 6. MVP 功能范围

### 必做功能

- 功能 1
- 功能 2
- 功能 3

### 暂不做功能

- 功能 4
- 功能 5

## 7. 核心用户流程

用户从进入产品到完成目标的完整路径。

## 8. 技术可行性初判

- 大致实现方式：
- 可能依赖的能力：
- 明显技术风险：
- API / 部署 / 时间成本是否可控：

## 9. 验收标准

什么情况下，这个 MVP 算完成。
```

这一阶段结束后，你应该拿到的是一个**产品方案初版**，而不是一堆零散想法。

---

# 2. 视觉设计：形成 UI 原型

这一阶段的目标是让产品从“想法”变成“可感知的界面”。

不要直接让 AI 说“帮我做个好看的页面”。更好的方式是先找参考，再让 AI 提炼风格。

可以参考：

- Dribbble
- Linear
- Vercel
- Raycast
- v0
- Mobbin
- Pinterest
- 同类产品截图

你可以让 AI 总结：

- 整体气质
- 色彩风格
- 页面布局
- 卡片样式
- 组件风格
- 关键交互
- Loading / Empty / Error 状态

如果有条件，可以用 Figma Make、Figma AI、v0 先生成并打磨 UI 原型。

最终产出：

```txt
docs/DESIGN.md
```

建议内容：

```md
# Design Guide

## 1. 视觉关键词

例如：简洁、专业、轻量、AI 感、适合 Demo 展示。

## 2. 页面结构

- 首页：
- 输入区：
- 结果区：
- 操作区：

## 3. 组件规范

- Button：
- Input：
- Card：
- Modal：
- Toast：
- Loading：
- Empty：
- Error：

## 4. 交互原则

- 主流程要短
- 操作反馈要明确
- AI 生成过程必须有 Loading
- 失败时要给用户可理解的提示

## 5. UI 原型参考

放截图、链接或设计说明。
```

---

# 3. 开发准备：固化项目边界

这一阶段的目标是让 Codex Agent 在清晰边界下开发，避免项目后期混乱。

打开项目目录，建立：

```txt
docs/
  PRD.md
  DESIGN.md
  ARCHITECTURE.md
  TODO.md

AGENTS.md
README.md
```

其中：

```txt
PRD.md          产品定位、用户痛点、MVP 边界、验收标准
DESIGN.md       视觉风格、组件规范、交互状态
ARCHITECTURE.md 技术栈、目录结构、模块边界、开发约束
TODO.md         分阶段任务清单
AGENTS.md       给 Codex Agent 的项目规则
README.md       对外展示说明
```

## 3.1 生成 ARCHITECTURE.md

这一步才正式进入技术方案。

建议包含：

```md
# Architecture

## 1. 技术栈

- Frontend:
- Backend:
- Database:
- AI API:
- Deployment:

## 2. 目录结构

src/
  app/
  components/
  lib/
  services/
  hooks/
  types/

## 3. 核心模块

- 用户输入模块
- AI 生成模块
- 结果展示模块
- 保存 / 导出模块

## 4. 数据模型

定义核心对象和字段。

## 5. API 设计

列出核心接口。

## 6. 开发约束

- 不做复杂登录
- 不做多租户
- 不做过度抽象
- 不引入无关依赖
- 不破坏 PRD 和 DESIGN 中定义的主流程
```

## 3.2 生成 AGENTS.md

这是给 Codex Agent 的项目说明书。

```md
# AGENTS.md

## Project Goal

Build a small but polished MVP with clear product value, clean structure, and demoable core flow.

## Must Read Before Coding

Before coding, read:

- docs/PRD.md
- docs/DESIGN.md
- docs/ARCHITECTURE.md
- docs/TODO.md

## Development Rules

- Work on one task at a time.
- Do not rewrite unrelated files.
- Do not introduce large dependencies without confirmation.
- Do not change architecture without updating docs/ARCHITECTURE.md.
- Do not change product scope without updating docs/PRD.md.
- Keep components small and readable.
- Prefer simple implementation over over-engineering.

## Commands

npm install
npm run dev
npm run lint
npm run build

## Definition of Done

A task is done only when:

- The feature works in browser.
- Loading / empty / error states are handled.
- No obvious console errors.
- Lint and build pass.
- Code is committed.
```

---

# 4. 正式开发：小步迭代

这一阶段的核心原则是：

```txt
一次只做一个任务。
一次只改一个明确范围。
每轮都要测试。
每轮都要 commit。
```

先让 Codex 基于文档生成：

```txt
docs/TODO.md
```

建议结构：

```md
# TODO

## Phase 1：项目初始化

- [ ] 初始化项目
- [ ] 配置基础样式
- [ ] 建立目录结构
- [ ] 搭建首页框架

## Phase 2：核心功能

- [ ] 实现用户输入
- [ ] 实现 AI 生成接口
- [ ] 实现结果展示
- [ ] 实现复制 / 保存

## Phase 3：体验完善

- [ ] Loading 状态
- [ ] Empty 状态
- [ ] Error 状态
- [ ] 移动端适配

## Phase 4：测试与部署

- [ ] 跑通主流程
- [ ] 修复明显 bug
- [ ] npm run lint
- [ ] npm run build
- [ ] 部署上线
- [ ] 补充 README
```

## 4.1 每轮开发 Prompt

```txt
请先阅读：

- docs/PRD.md
- docs/DESIGN.md
- docs/ARCHITECTURE.md
- docs/TODO.md

现在只执行 TODO 中的这一项：

[具体任务]

要求：

1. 只修改和该任务相关的文件。
2. 不要重构无关代码。
3. 不要引入不必要依赖。
4. 不要突破 PRD 和 ARCHITECTURE 的边界。
5. 完成后说明修改了哪些文件。
6. 完成后说明如何验证。
7. 如发现架构问题，先说明，不要直接大改。
```

## 4.2 每轮开发节奏

```txt
选一个任务
→ Codex 实现
→ 本地验证
→ Review Diff
→ 修复问题
→ Git Commit
→ 下一个任务
```

每完成一个模块，至少验证：

```txt
1. 主流程能否跑通
2. Loading 状态是否正常
3. Empty 状态是否正常
4. Error 状态是否正常
5. 控制台是否有明显报错
```

然后执行：

```bash
git status
git add .
git commit -m "feat: xxx"
```

---

# 5. 变更控制：防止 MVP 失控

开发过程中一定会冒出新想法，但不能让新需求随便插入。

处理方式：

```txt
小需求：当场判断，必要时加入 TODO
大需求：先更新 PRD.md 和 ARCHITECTURE.md，再重新拆 TODO
```

判断标准：

```txt
如果新需求会影响产品定位、核心流程、数据模型、技术架构，就不是小改，必须先更新文档。
```

否则项目很容易变成：

```txt
需求越来越多
结构越来越乱
主流程越来越不稳定
最后 Demo 反而讲不清楚
```

---

# 6. Review / Refactor 单独处理

不要让 Codex 边写功能边大规模重构。

Review Prompt：

```txt
请 review 当前 diff，重点看：

1. 是否符合 PRD
2. 是否违反 ARCHITECTURE
3. 是否有重复代码
4. 是否有过度复杂逻辑
5. 是否缺少 loading / empty / error 状态
6. 是否有明显安全问题

先输出 review 结论，不要直接修改。
```

Refactor Prompt：

```txt
请基于刚才的 review 结果做最小范围 refactor。

要求：

1. 不改变功能表现。
2. 不重写无关模块。
3. 不引入新依赖。
4. 修改后说明验证方式。
```

---

# 7. 测试上线：闭环交付

上线前至少完成：

```md
# Testing Checklist

## 主流程

- [ ] 用户可以进入首页
- [ ] 用户可以完成输入
- [ ] 用户可以触发 AI 生成
- [ ] 系统可以返回结果
- [ ] 用户可以复制 / 保存结果

## 状态

- [ ] Loading 正常
- [ ] Empty 正常
- [ ] Error 正常
- [ ] API 报错有提示

## 技术

- [ ] 没有明显 console error
- [ ] npm run lint 通过
- [ ] npm run build 通过
- [ ] 环境变量正确
- [ ] 部署环境可访问
```

部署可以选择：

```txt
Vercel / Netlify / Cloudflare
```

---

# 8. 交付文档：让项目拿得出手

项目完成后，补齐：

```txt
README.md
docs/DEMO_SCRIPT.md
```

README 建议包含：

```md
# Project Name

## 一句话介绍

这个项目是什么，解决什么问题。

## Demo

- Online Demo:
- Screenshots:

## 核心功能

- 功能 1
- 功能 2
- 功能 3

## 产品亮点

- 亮点 1
- 亮点 2
- 亮点 3

## 技术栈

- Next.js
- Tailwind CSS
- AI API
- Vercel

## 本地运行

npm install
npm run dev

## 环境变量

OPENAI_API_KEY=

## 我的思考

- 为什么做这个产品
- 为什么这样设计 MVP
- 技术上做了哪些取舍
- 后续如何扩展
```

---

# 9. 最终推荐 SOP

```txt
1. 和 AI 脑暴产品方向
2. 明确产品定位、目标用户、痛点和 MVP 边界
3. 做技术可行性初判，不展开详细技术方案
4. 输出 docs/PRD.md
5. 收集 UI 参考，生成 UI 原型
6. 输出 docs/DESIGN.md
7. 让 Codex 生成 docs/ARCHITECTURE.md
8. 创建 AGENTS.md，固化 Agent 开发规则
9. 生成 docs/TODO.md
10. 按 TODO 小步开发
11. 每完成一项就测试、review、commit
12. 新需求先判断大小，大需求先更新 PRD / ARCHITECTURE
13. 主流程跑通后做 UI polish
14. 部署到 Vercel / Netlify / Cloudflare
15. 补 README 和 Demo Script
16. 复盘并更新文档
```

---

# 10. 一句话总结

> 最好的 Vibe Coding，不是让 AI 替你思考，而是你先把产品方向、MVP 边界和验收标准想清楚，再让 Codex 在清晰文档和开发规则下高速执行。
>
> 真正体现 Builder 能力的，不是代码量，而是你能否定义问题、控制范围、快速交付，并把项目讲成一个完整的产品故事。
