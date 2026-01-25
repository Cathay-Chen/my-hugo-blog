---
title: "Function Calling 与 MCP: Agent 工具接口的标准化之路"
date: 2024-03-15T10:00:00+08:00
lastmod: 2024-03-15T10:00:00+08:00
draft: false
tags: ["AI", "Agent", "Function Calling", "MCP", "Tool Use"]
categories: ["AI技术"]
author: "cathay"
---

## 前言

Agent 需要使用工具才能与外部世界交互。OpenAI 的 Function Calling 和 Anthropic 的 MCP 协议代表了两种不同的工具接口标准化思路。本文将深入对比这两种方案,探讨工具接口的演进方向。

## OpenAI Function Calling: API 调用范式

### 2023.06.13 的标准化时刻

TODO: Function Calling 的发布背景

### Tool Schema 设计

TODO: 如何定义工具的能力边界

```json
// TODO: Function Calling schema 示例
```

### 从硬编码到动态注册

TODO: LangChain Tools, LlamaIndex Tools 的设计

## Anthropic MCP 协议: 上下文协议范式

### 2024.11 登场: 为什么需要新标准?

TODO: MCP 解决了什么问题?

### MCP 的核心设计

#### Server-Client 架构

TODO: 架构图和工作流程

#### 三大原语: Resources, Tools, Prompts

TODO: 详细解释每个原语的用途

## Function Calling vs MCP: 本质差异

### API 调用 vs 上下文协议

TODO: 深度对比两种范式

### 适用场景对比

TODO: 什么时候用 Function Calling,什么时候用 MCP?

## 实战: 用 MCP 构建工具

### 案例 1: 文件系统访问

```typescript
// TODO: MCP Server 代码示例
```

### 案例 2: 数据库查询

```typescript
// TODO: 数据库 MCP Server
```

### 案例 3: API 集成

```python
# TODO: Python MCP Server 示例
```

## 小结

TODO: 总结工具接口标准化的价值,预告下一篇推理模式

---

**系列文章**:
- 上一篇: 从 AutoGPT 到 Agent 范式: AI 为什么需要"自主性"?
- 下一篇: ReAct 与 Chain-of-Thought: Agent 的推理模式演进
