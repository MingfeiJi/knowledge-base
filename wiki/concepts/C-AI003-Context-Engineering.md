---
aliases: [Context Engineering, 上下文工程]
created: 2026-04-05
updated: 2026-04-05
---

# Context Engineering (上下文工程)

## 定义

为 LLM 精心设计和管理输入上下文的技术，包括选择性信息加载、上下文压缩、以及会话状态管理。

## 详细解释

上下文工程是 LLM 应用开发中的核心技能。由于 LLM 的上下文窗口是有限且宝贵的资源，如何有效利用成为关键问题。

主要技术包括：
1. **选择性加载**：只加载与当前任务相关的信息
2. **上下文压缩**：总结或精简已有上下文
3. **分层管理**：CLAUDE.md 等配置文件、会话历史、即时输入
4. **子代理隔离**：使用子代理处理调查任务，避免污染主上下文

在 Cursor、Claude Code 等 LLM 应用中，上下文工程是核心能力：
- 精心编排复杂的 LLM 调用 DAG
- 提供应用特定的 GUI
- 管理"自主程度滑块"

## 关键特征

- 上下文窗口是最重要的约束
- 性能随上下文填满而下降
- 需要主动管理而非被动使用
- 支持增量和全量两种模式

## 典型例子

- `/clear` 命令重置上下文
- 子代理进行独立调查
- CLAUDE.md 持久化配置
- 自动压缩历史对话

## 相关概念

- [[C-AI007-Claude-Code]]
- [[C-AI009-Subagent]]
- [[C-AI010-CLAUDE-MD]]

## 来源引用

- [[wiki/summaries/S-AI003-Claude-Code-Best-Practices]]
- [[wiki/summaries/S-AI002-Karpathy-2025-LLM-Year-Review]]
