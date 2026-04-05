---
source_url: https://code.claude.com/docs/en/best-practices
author: Anthropic
published: 2026-04-01
fetched: 2026-04-05
tags: [claude-code, agentic-coding, best-practices, anthropic, 开发工具]
---

# Claude Code 最佳实践完全指南 (2026)

## TL;DR

Claude Code 是 Anthropic 推出的 agentic 编码工具。本指南总结了官方文档和社区实践中的核心技巧：管理上下文窗口、提供验证机制、先探索再编码、配置环境、以及高效沟通和并行扩展。

## 核心约束：上下文窗口

> "Most best practices are based on one constraint: Claude's context window fills up fast, and performance degrades as it fills."

Claude 的上下文窗口包含整个对话、每个读取的文件和每个命令输出。一次调试会话可能消耗数万 token。

**关键影响**：
- 上下文填满时，Claude 会开始"遗忘"早期指令
- 更容易犯错
- 是需要管理的最重要资源

## 六大核心实践

### 1. 提供验证机制

**最高杠杆的单一操作**：让 Claude 能够自我验证工作。

| 策略 | 之前 | 之后 |
|---|---|---|
| 提供验证标准 | "实现邮箱验证函数" | "写 validateEmail 函数，测试用例：user@example.com 为 true，invalid 为 false，user@.com 为 false。实现后运行测试" |
| 视觉验证 UI | "让仪表盘更好看" | "[粘贴截图] 实现这个设计，截图结果并与原图对比，列出差异并修复" |
| 解决根本原因 | "构建失败了" | "构建失败错误：[粘贴错误]。修复并验证构建成功，解决根因而非压制错误" |

### 2. 探索、计划、编码

**四阶段工作流**：

1. **探索** (Plan Mode)：读取文件，理解代码
2. **计划** (Plan Mode)：创建详细实现方案，`Ctrl+G` 可在编辑器中编辑
3. **实现** (Normal Mode)：编码并验证
4. **提交**：描述性 commit 并创建 PR

> "Plan Mode is most useful when you're uncertain about the approach, when the change modifies multiple files, or when you're unfamiliar with the code being modified."

### 3. 提供具体上下文

| 策略 | 之前 | 之后 |
|---|---|---|
| 限定任务范围 | "给 foo.py 加测试" | "为 foo.py 写测试，覆盖用户登出的边界情况，避免使用 mock" |
| 指向来源 | "ExecutionFactory API 为什么这么奇怪？" | "查看 ExecutionFactory 的 git 历史，总结其 API 的演变过程" |
| 引用现有模式 | "添加日历组件" | "查看首页现有组件的实现模式，HotDogWidget.php 是好例子，按照模式实现新的日历组件" |

**丰富内容输入方式**：
- `@` 引用文件
- 直接粘贴图片
- 提供 URL
- 管道输入数据：`cat error.log | claude`

### 4. 配置环境

#### CLAUDE.md 文件

运行 `/init` 生成基础配置，然后逐步优化。

**应包含**：
- Claude 无法猜测的 Bash 命令
- 与默认不同的代码风格规则
- 测试指令和首选测试运行器
- 仓库礼仪（分支命名、PR 约定）
- 项目特定的架构决策
- 开发环境怪癖

**不应包含**：
- Claude 能通过读代码推断的内容
- 标准语言约定
- 详细 API 文档（改用链接）
- 经常变化的信息
- 不言自明的实践如"写干净的代码"

> "If Claude keeps doing something you don't want despite having a rule against it, the file is probably too long and the rule is getting lost."

#### 权限配置

三种减少中断的方式：
- **Auto Mode**：分类器模型审核命令，只阻止高风险操作
- **Permission Allowlists**：允许已知安全的工具
- **Sandboxing**：启用操作系统级隔离

#### 子代理 (Subagents)

在 `.claude/agents/` 定义专业助手：

```markdown
---
name: security-reviewer
description: Reviews code for security vulnerabilities
tools: Read, Grep, Glob, Bash
model: opus
---
You are a senior security engineer. Review code for:
- Injection vulnerabilities
- Authentication flaws
- Secrets in code
- Insecure data handling
```

### 5. 高效沟通

#### "Think" 触发词层级

Simon Willison 发现的 token 预算系统：

| 触发词 | Token 预算 |
|---|---|
| "think" | 4,000 |
| "think hard" | 更多 |
| "think harder" | 更多 |
| "megathink" | 10,000 |
| "ultrathink" | 31,999 |

> "These specific phrases are mapped directly to increasing levels of thinking budget."

#### 让 Claude 采访你

对于大型功能，先让 Claude 采访你：

```
I want to build [brief description]. Interview me in detail using the AskUserQuestion tool.

Ask about technical implementation, UI/UX, edge cases, concerns, and tradeoffs.
Keep interviewing until we've covered everything, then write a complete spec to SPEC.md.
```

### 6. 管理会话

#### 及早纠正

- `Esc`：中途停止 Claude
- `Esc + Esc` 或 `/rewind`：恢复之前的对话和代码状态
- `/clear`：在不相关任务间重置上下文

> "If you've corrected Claude more than twice on the same issue in one session, the context is cluttered with failed approaches. Run /clear and start fresh."

#### 使用子代理进行调查

```
Use subagents to investigate how our authentication system handles token
refresh, and whether we have any existing OAuth utilities I should reuse.
```

子代理在独立上下文中探索，返回摘要，不会污染主对话。

## 自动化与扩展

### 非交互模式

```bash
# 一次性查询
claude -p "Explain what this project does"

# 结构化输出
claude -p "List all API endpoints" --output-format json

# 流式处理
claude -p "Analyze this log file" --output-format stream-json
```

### 并行会话

三种并行方式：
1. **Claude Code 桌面应用**：可视化管理多个本地会话
2. **Claude Code on Web**：在 Anthropic 安全云基础设施中运行
3. **Agent Teams**：多会话自动协调

### Writer/Reviewer 模式

| Session A (Writer) | Session B (Reviewer) |
|---|---|
| `Implement a rate limiter for our API endpoints` | |
| | `Review the rate limiter implementation. Look for edge cases, race conditions.` |
| `Here's the review feedback. Address these issues.` | |

## 常见失败模式

1. **厨房水槽会话**：在一个任务中混入不相关的问题
   - **修复**：`/clear` 在不相关任务间

2. **反复纠正**：Claude 错了，纠正它，还是错
   - **修复**：两次失败后 `/clear`，用更好的初始提示重新开始

3. **过度指定的 CLAUDE.md**：太长导致 Claude 忽略一半
   - **修复**：无情地修剪，或转换为 hook

4. **信任-验证差距**：Claude 产出看似合理但不处理边界情况的实现
   - **修复**：始终提供验证机制

5. **无限探索**：让 Claude "调查"却不限定范围
   - **修复**：限定调查范围或使用子代理

## 模型选择策略

- **Opus**：复杂推理任务
- **Sonnet**：通用工作
- **Haiku**：快速探索

> "Using Haiku for exploration subagents and Sonnet for implementation typically reduces costs 40-50% compared to using Sonnet for everything."

## 关键资源

- [官方文档](https://code.claude.com/docs/en/best-practices)
- [DeepLearning.AI 课程](https://learn.deeplearning.ai/courses/claude-code-a-highly-agentic-coding-assistant)
- [Anthropic 团队使用方式 PDF](https://www-cdn.anthropic.com/58284b19e702b49db9302d5b6f135ad8871e7658.pdf)
- [awesome-claude-code GitHub](https://github.com/hesreallyhim/awesome-claude-code)

---

## 金句摘录

> "Claude Code is an agentic coding environment. Unlike a chatbot that answers questions and waits, Claude Code can read your files, run commands, make changes, and autonomously work through problems."

> "Treat Claude like a junior engineer with super speed: you give clear constraints, you demand a plan, you enforce tests, and you gate changes."

> "The best results come from tight feedback loops."
