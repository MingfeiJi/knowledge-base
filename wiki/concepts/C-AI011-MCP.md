---
aliases: [MCP, Model Context Protocol, 模型上下文协议]
created: 2026-04-05
updated: 2026-04-05
---

# MCP (Model Context Protocol)

## 定义

Anthropic 开发的开放协议，让 AI Agent 能够与外部工具（数据库、搜索引擎、API 等）进行标准化通信。被称为"AI 的 USB-C"。

## 详细解释

MCP 解决了 AI Agent 实际应用中的核心问题：如何连接到工作实际发生的系统。

发展历程：
- **2025 年初**：Anthropic 发布 MCP
- **2025 年 4 月**：GitHub 为 VS Code 用户推出 MCP 支持的 Agent Mode
- **2025 年 9 月**：GitHub MCP Registry 上线
- **2026 年 3 月**：达到 9700 万安装里程碑
- **开放治理**：Linux Foundation 接管

MCP 的设计理念是让每个 MCP Server 像 AI 技术栈中的一个组件，可以灵活组合。与 Google 的 Agent2Agent 协议（解决 Agent 间通信）互补。

## 关键特征

- 标准化的工具连接协议
- 开放源代码
- Linux Foundation 开放治理
- 与 Agent2Agent 协议协同工作

## 典型例子

- 连接数据库进行查询
- 调用搜索引擎获取信息
- 集成第三方 API
- GitHub Copilot Agent Mode

## 相关概念

- [[C-AI012-Agent2Agent]]
- [[C-AI007-Claude-Code]]
- [[C-AI013-Agentic-Coding]]

## 来源引用

- [[wiki/summaries/S-AI004-AI-Agent-Progress]]
