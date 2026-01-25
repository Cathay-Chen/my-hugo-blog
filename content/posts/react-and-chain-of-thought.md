---
title: "ReAct 与 Chain-of-Thought: Agent 的推理模式演进"
date: 2024-05-10T10:00:00+08:00
lastmod: 2024-05-10T10:00:00+08:00
draft: false
tags: ["AI", "Agent", "ReAct", "Chain-of-Thought", "Reasoning"]
categories: ["AI技术"]
author: "cathay"
---

## 前言

Agent 不仅需要执行工具,更需要"思考"。Chain-of-Thought 和 ReAct 代表了两种不同的推理模式。本文将深入探讨 Agent 如何"思考",以及不同推理模式的权衡。

## Chain-of-Thought: 让 LLM 说出思考过程

### CoT 的核心思想

TODO: 为什么"说出来"能提升推理能力?

### Few-shot CoT vs Zero-shot CoT

TODO: 对比两种 CoT 方式

```
# TODO: CoT Prompt 示例
```

## ReAct: Reasoning + Acting 的交替循环

### ReAct 框架的工作流程

TODO: Thought → Action → Observation 循环

### ReAct 的 Prompt 设计

```
# TODO: ReAct Prompt 模板
```

### 实战案例: ReAct Agent 执行过程

TODO: 展示完整的推理链路

## 其他推理模式对比

### ReWOO: Reasoning WithOut Observation

TODO: 先规划后执行的思路

### Plan-and-Execute

TODO: 分离规划和执行

### Reflection

TODO: 自我反思和纠错

## Few-shot Prompting 的关键作用

TODO: 如何用示例引导 Agent 推理

## o1/o3 模型: 推理模式的未来?

### 为什么 o1 让 ReAct 变得不那么必要?

TODO: 内置推理能力的模型

### 推理模式的演进方向

TODO: 从显式到隐式

## 小结

TODO: 总结推理模式的演进,预告下一篇复杂 Agent 架构

---

**系列文章**:
- 上一篇: Function Calling 与 MCP: Agent 工具接口的标准化之路
- 下一篇: Plan-and-Execute 与 Self-Reflection: 复杂 Agent 架构
