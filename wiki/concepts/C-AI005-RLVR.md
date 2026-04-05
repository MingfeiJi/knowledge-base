---
aliases: [RLVR, 强化学习从可验证奖励, Reinforcement Learning from Verifiable Rewards]
created: 2026-04-05
updated: 2026-04-05
---

# RLVR (强化学习从可验证奖励)

## 定义

针对自动可验证的奖励进行强化学习训练的方法，使 LLM 自发展现"推理"能力。

## 详细解释

RLVR 是 LLM 训练的第四阶段，扩展了传统的三阶段流程：

**传统三阶段**：预训练 → SFT (监督微调) → RLHF (人类反馈强化学习)

**扩展四阶段**：预训练 → SFT → RLHF → **RLVR**

RLVR 的核心思想是利用可自动验证的任务（如数学问题、代码测试）作为奖励信号，让模型学习推理能力。与 RLHF 依赖人工标注不同，RLVR 可以大规模自动化执行。

关键影响：
- 模型学会将问题分解为中间步骤
- 发展多种问题解决策略
- 计算资源从预训练转向 RL 运行时

## 关键特征

- 使用可自动验证的任务作为奖励
- 无需人工标注
- 培养模型的推理能力
- 支持大规模自动化训练

## 典型例子

- OpenAI o1：首次演示 RLVR 能力
- OpenAI o3：RLVR 的转折点
- 数学推理任务
- 代码生成与验证

## 相关概念

- [[C-AI015-RLHF]]
- [[C-AI016-Chain-of-Thought]]
- [[C-AI017-Test-Time-Compute]]

## 来源引用

- [[wiki/summaries/S-AI002-Karpathy-2025-LLM-Year-Review]]
