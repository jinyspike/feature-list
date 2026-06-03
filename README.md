# Feature List Workflow

一个基于 `feature-list.jsonc` 的功能驱动开发工作流，贯穿需求、开发、修复、测试全流程。

## 灵感来源

本项目深受 Anthropic 工程团队的博客文章启发：

> **[Effective harnesses for long-running agents](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents)** — *Anthropic Engineering, Nov 26, 2025*

文章指出，长期运行的 agent 面临两个核心问题：

1. **急于求成** — agent 试图一次性完成所有功能，导致上下文窗口耗尽，功能半成品堆积
2. **过早收工** — agent 看到部分进展就以为任务已完成

解决方案的核心之一就是 **Feature List**：initializer agent 会先编写一份全面的 feature 需求文件（比如 Claude.ai 克隆项目定义了 200+ 个 feature），**全部标记为 "未通过"**。后续的 coding agent 逐条推进，直到所有 feature 变绿。

> *"These features were all initially marked as 'failing' so that later coding agents would have a clear outline of what full functionality looked like."*

## 本项目的实现

我将其思路提炼为三个可复用 skill，分别对应开发流程的三个场景：

| Skill | 场景 | 职责 |
|---|---|---|
| `feature-list-new` | 开发新需求 | 定义 feature + TDD 开发，保持 `passes: false` |
| `feature-list-fix` | 修复/需求变更 | 先更新 feature list，再改代码，重置受影响条目 |
| `feature-list-verify` | 端到端验证 | 设计 e2e 测试，通过后标记 `passes: true` |

### 工作流程

```
新需求 → /feature-list-new → 单元测试通过 → /feature-list-verify → 完成
                                ↑
修复/变更 → /feature-list-fix → 单元测试通过 → /feature-list-verify → 完成
```

### 硬性规则

- **渐进式**：新功能/修改功能必须先有 `feature-list.jsonc` 条目，再写代码
- **单一信息源**：需求定义、测试追踪、覆盖状态全在一个 `feature-list.jsonc` 文件中
- **修复先改 list**：修改代码前必须先用 feature-list-fix 更新 feature list

## 快速开始

将 `.claude/skills/` 目录复制到目标项目中，在 `CLAUDE.md` 中声明本文的工作流即可。

## 结构

```
feature-list/
├── README.md
├── CLAUDE.md                           ← 工作流规则
└── skills/
    ├── feature-list-new/SKILL.md       ← 新需求：定义 + TDD 开发
    ├── feature-list-fix/SKILL.md       ← 修复/需求变更：先改 list，再改代码
    └── feature-list-verify/SKILL.md    ← 端到端验证：e2e 测试 + passes=true
```
