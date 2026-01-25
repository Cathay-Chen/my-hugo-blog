---
title: "RAG 的记忆系统: 从无状态到有状态的演进"
date: 2023-10-20T10:00:00+08:00
lastmod: 2023-10-20T10:00:00+08:00
draft: false
tags: ["AI", "RAG", "Memory", "Agent"]
categories: ["AI技术"]
author: "cathay"
---

## 前言

早期的 RAG 系统有一个致命缺陷: 每次对话都是独立的,无法记住之前的上下文。本文将探讨 RAG 如何从无状态走向有状态,以及记忆系统如何成为 Agent 的基础能力。

## 早期 RAG 的问题: 健忘症

### 每次对话都是新的

TODO: 展示无状态 RAG 的局限性

### 上下文丢失的后果

TODO: 用户体验的断裂

## Short-term Memory: 对话历史管理

### 滑动窗口策略

TODO: 如何管理有限的上下文窗口

### Token 预算分配

TODO: System Prompt + History + Retrieved Docs 的权衡

## Long-term Memory: 经验积累

### 对话摘要存入向量库

TODO: 如何将历史对话转化为长期记忆

### 记忆的检索和召回

TODO: 何时需要召回历史经验?

## 记忆的分层设计

### Working Memory

TODO: 当前对话的短期缓存

### Episodic Memory

TODO: 事件性记忆,具体对话的完整记录

### Semantic Memory

TODO: 语义记忆,提取的知识和规律

## 记忆系统的架构设计

TODO: 架构图和伪代码

## 记忆系统是 Agent 的基础

### 为什么 Agent 需要记忆?

TODO: 引出下一个系列 Agent 的核心能力

### 从 RAG 到 Agent 的演进

TODO: 记忆是自主性的前提

## 小结

TODO: 总结 RAG 系列,预告 Agent 系列

---

**系列文章**:
- 上一篇: 从文本切块到语义检索: RAG 的工程化实践
- 下一篇: 从 AutoGPT 到 Agent 范式: AI 为什么需要"自主性"?
