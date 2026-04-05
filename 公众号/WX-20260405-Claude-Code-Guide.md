---
title: Claude Code 完全指南：像高级工程师一样使用 AI 编程
created: 2026-04-05
source: [[wiki/summaries/S-AI003-Claude-Code-Best-Practices]]
status: draft
word_count: 2500
---

# Claude Code 完全指南：像高级工程师一样使用 AI 编程

> 91% 的工程师已经在使用 agentic AI 编码工具，你准备好了吗？

## 导语

Claude Code 是 Anthropic 推出的 agentic 编码工具。与传统 AI 助手不同，它能够自主读取文件、运行命令、做出修改，并在你观察、引导或离开时自主解决问题。

但这种自主性也带来了学习曲线。本文总结官方文档和社区实践中的核心技巧，帮你快速上手。

## 核心约束：上下文窗口

**这是最重要的一点**：Claude 的上下文窗口填满得很快，性能会随之下降。

上下文包含：
- 整个对话历史
- 读取的每个文件
- 每个命令输出

一次调试会话可能消耗数万 token。上下文填满时，Claude 会开始"遗忘"早期指令。

**解决方案**：
- 使用 `/clear` 在不相关任务间重置上下文
- 用子代理进行调查，避免污染主对话
- 纠正两次后如果还是错，直接 `/clear` 重来

## 六大核心实践

### 1. 提供验证机制

**最高杠杆的单一操作**：让 Claude 能够自我验证。

❌ 之前："实现邮箱验证函数"

✅ 之后："写 validateEmail 函数，测试用例：user@example.com 为 true，invalid 为 false。实现后运行测试"

没有验证，Claude 可能产出看起来对但实际不工作的代码。

### 2. 探索 → 计划 → 编码

别让 Claude 直接写代码。用 Plan Mode 分离探索和执行：

1. **探索**（Plan Mode）：读取文件，理解代码
2. **计划**（Plan Mode）：创建实现方案，`Ctrl+G` 可编辑
3. **实现**（Normal Mode）：编码并验证
4. **提交**：创建 PR

什么时候跳过计划？任务简单、范围明确、能一句话描述的时候。

### 3. 提供具体上下文

Claude 不能读心。引用具体文件、说明约束、指向模式。

❌ "给 foo.py 加测试"
✅ "为 foo.py 写测试，覆盖用户登出的边界情况，避免使用 mock"

丰富输入的方式：
- `@` 引用文件
- 直接粘贴图片
- 管道输入：`cat error.log | claude`

### 4. 配置 CLAUDE.md

运行 `/init` 生成基础配置。

**应包含**：
- Claude 无法猜测的 Bash 命令
- 与默认不同的代码风格
- 测试指令
- 项目特定的架构决策

**不应包含**：
- Claude 能从代码推断的内容
- 标准语言约定
- "写干净的代码"这种废话

> 如果 Claude 一直违反某条规则，文件可能太长了，规则被淹没了。

### 5. 使用 "Think" 触发词

这是一个隐藏技巧。用特定词汇触发更深度的思考：

| 触发词 | 效果 |
|---|---|
| think | 基础思考 |
| think hard | 更多思考 |
| think harder | 深度思考 |
| ultrathink | 最大思考预算 (31,999 tokens) |

复杂任务时，加上 "ultrathink" 会得到更好的结果。

### 6. 用子代理调查

子代理在独立上下文中运行，不会污染主对话：

```
Use subagents to investigate how our authentication system
handles token refresh
```

子代理会探索、读取文件，然后返回摘要。你的主对话保持干净。

## 模型选择策略

- **Opus**：复杂推理
- **Sonnet**：通用工作
- **Haiku**：快速探索

用 Haiku 做探索 + Sonnet 做实现，成本降低 40-50%。

## 常见失败模式

1. **厨房水槽会话**：在一个任务中混入不相关问题
   → `/clear` 在不相关任务间

2. **反复纠正**：Claude 错了，纠正它，还是错
   → 两次失败后 `/clear`，用更好的提示重来

3. **CLAUDE.md 太长**：重要规则被淹没
   → 无情修剪

4. **信任-验证差距**：看似合理但不处理边界情况
   → 始终提供验证机制

## 结语

Claude Code 的核心理念是：把它当成一个"超高速初级工程师"。

你给出清晰的约束、要求计划、强制测试、把控变更。

掌握这些实践，你会发现 AI 编程的生产力提升是真实的。

---

**推荐阅读**：
- [官方文档](https://code.claude.com/docs/en/best-practices)
- [DeepLearning.AI 课程](https://learn.deeplearning.ai/courses/claude-code-a-highly-agentic-coding-assistant)

---

## 发布说明

- 封面图：Claude Code 界面截图 + 标题
- 预计阅读时间：8 分钟
- 标签：AI编程 Claude Code 开发工具 效率提升
