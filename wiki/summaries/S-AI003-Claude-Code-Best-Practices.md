---
source: "[[raw/articles/Claude-Code-Best-Practices-2026]]"
source_url: https://code.claude.com/docs/en/best-practices
author: Anthropic
created: 2026-04-05
tags: [claude-code, agentic-coding, best-practices, anthropic]
---

# Claude Code 最佳实践

## TL;DR

Claude Code 是 Anthropic 的 agentic 编码工具。核心实践：管理上下文窗口、提供验证机制、先探索再编码、配置 CLAUDE.md、使用子代理调查、并行会话扩展。

## 核心结论

- 上下文窗口是最重要的约束和资源
- 提供验证机制是最高杠杆的单一操作
- 四阶段工作流：探索 → 计划 → 实现 → 提交
- "think" 系列触发词控制 thinking 预算（think < think hard < ultrathink）
- 使用子代理进行调查，避免污染主对话上下文

## 关键证据

- Anthropic 内部团队和社区验证的模式
- 使用 Haiku 做探索、Sonnet 做实现，成本降低 40-50%
- 91% 工程师已使用 agentic AI 编码工具

## 相关概念

- [[C-AI007-Claude-Code]]
- [[C-AI003-Context-Engineering]]
- [[C-AI009-Subagent]]
- [[C-AI010-CLAUDE-MD]]

## 疑点/待验证

- 不同复杂度任务的最优工作流差异
- 长期项目中的上下文管理策略
- 团队协作中的 CLAUDE.md 最佳实践

## 原文引用

> "Treat Claude like a junior engineer with super speed: you give clear constraints, you demand a plan, you enforce tests, and you gate changes."
