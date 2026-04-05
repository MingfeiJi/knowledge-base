---
source_url: https://karpathy.bearblog.dev/year-in-review-2025/
author: Andrej Karpathy
published: 2025-12-31
fetched: 2026-04-05
tags: [llm, karpathy, 年度回顾, ai-trends, 2025]
---

# Karpathy 的 2025 LLM 年度回顾

## TL;DR

Karpathy 总结了 2025 年 LLM 领域的六大范式转变：RLVR 训练方法、"幽灵 vs 动物"认知框架、Cursor 应用层、Claude Code 本地 Agent、Vibe Coding 编程范式、以及 LLM GUI 的萌芽。

## 核心观点

> "2025 has been a strong and eventful year of progress in LLMs"

## 六大范式转变

### 1. RLVR (强化学习从可验证奖励)

**变化**: LLM 训练从三阶段（预训练→SFT→RLHF）扩展为四阶段，新增 RLVR。

**原理**: 针对自动可验证的奖励进行训练，使模型自发展现"推理"能力。

**影响**:
- 模型学会将问题分解为中间步骤
- 发展多种问题解决策略
- 计算资源从预训练转向 RL 运行

**里程碑**: OpenAI o1 首次演示，o3 发布成为转折点。

### 2. "幽灵 vs 动物" / 参差不齐的智能

**认知转变**: LLM 不是"进化中的动物"，而是"被召唤的幽灵"。

**关键差异**:
- 神经架构、训练数据、算法完全不同于生物
- 特定可验证领域表现突出
- 整体呈现"参差不齐"的性能

> "can be a genius polymath and a confused grade schooler, seconds away from being tricked"

**基准警告**: 基准测试容易被 RLVR 针对性优化，导致过度拟合。

### 3. Cursor / LLM 应用的新层级

**揭示**: LLM 应用架构的新层次。

**应用程序的关键功能**:
- 执行"上下文工程"
- 精心编排复杂的 LLM 调用 DAG
- 提供应用特定的 GUI
- 提供"自主程度滑块"

**预测**: LLM 实验室培养通用能力，LLM 应用通过私有数据和反馈循环将其组织成垂直专家。

### 4. Claude Code / 运行在你电脑上的 AI

**创新**: 首次展现 LLM Agent 的实际应用。

> "strings together tool use and reasoning for extended problem solving"

**关键特性**:
- 在本地计算机上运行（非云端）
- 可访问用户的环境、数据和上下文
- 低延迟交互

**新范式**:

> "a little spirit/ghost that 'lives' on your computer"

### 5. Vibe Coding (氛围编程)

**突破**: AI 跨越了仅用英语构建程序的能力阈值。

**含义**:
- 编程不再局限于训练有素的专业人士
- 代码变得 "free, ephemeral, malleable, discardable after single use"
- 专业人士能编写更多原本不会存在的软件

**赋权**: 符合 Karpathy 关于 LLM "赋予普通人权力"的理论。

### 6. Nano Banana / LLM GUI

**趋势**: 从文本界面向可视化转变的早期迹象。

**类比**:
- LLM 时代类似于 1970-80 年代的计算机革命
- 当前的"聊天"类似于 1980 年代的命令行界面
- 人类倾向于视觉/空间消费，而非文本阅读

**需求**: LLM GUI 层，整合文本生成、图像生成和世界知识。

## 关键预测

1. **能力悖论**: 迅速进展与"许多工作仍需完成"并存
2. **基准局限**: 2025 年基准容易被特定优化污染
3. **潜力低估**: LLM 已 "extremely useful" 但尚未充分发挥（不足 10%）

## 总结

2025 年标志着 LLM 发展的多个关键阶段转变：
- 训练方法论（RLVR）
- 部署架构（本地 Agent）
- 应用建设（垂直专家）

整个领域 "conceptually wide open"。

---

## 金句摘录

> "LLMs are not evolving animals, they are summoned ghosts."

> "I believe we are at maybe 10% of the way towards utilizing existing capabilities."

> "Code becomes free, ephemeral, malleable, discardable after single use."
