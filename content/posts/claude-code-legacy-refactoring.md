---
title: "Claude Code 实战: 遗留代码重构"
date: 2025-07-15T10:00:00+08:00
lastmod: 2025-07-15T10:00:00+08:00
draft: false
tags: ["AI", "IDE", "Claude Code", "Refactoring", "Legacy Code", "实战"]
categories: ["AI技术"]
author: "cathay"
---

## 前言

遗留代码重构是每个开发者的噩梦: 无文档、无测试、逻辑混乱。Claude Code 如何应对这种复杂场景?本文将通过一个真实的重构案例展示完整过程。

## 场景设定

### 项目背景

TODO: 一个混乱的 Node.js 项目

### 问题清单

- 无 TypeScript 类型约束
- 逻辑混乱,职责不清
- 零测试覆盖
- 代码风格不一致

### 重构目标

TODO: 迁移到 TypeScript + 分层架构 + 测试覆盖

## 重构策略: 五个阶段

### 第一阶段: 理解现有代码

TODO: 用 Glob + Grep + Read 建立全局认知

```
Claude 的分析过程:
1. Glob "**/*.js" → 发现 50+ 文件
2. Grep "app.listen" → 找到入口文件
3. Read server.js → 理解服务器启动逻辑
4. Grep "router" → 找到路由定义
5. Read routes/*.js → 理解路由结构
6. 生成项目架构分析报告
```

### 第二阶段: 补充测试

TODO: 保证不破坏现有功能

```typescript
// TODO: 为现有功能添加集成测试
```

### 第三阶段: 类型定义

TODO: 逐步迁移 TypeScript

```typescript
// TODO: 类型定义文件
```

### 第四阶段: 架构重构

TODO: 提取 service layer,分离关注点

```
重构前:
routes/users.js → 直接操作数据库,混杂业务逻辑

重构后:
routes/users.ts → 只处理 HTTP 请求
services/UserService.ts → 业务逻辑
repositories/UserRepository.ts → 数据访问
```

### 第五阶段: 验证和清理

TODO: 运行测试,删除冗余代码

## Claude Code 的工作流

### 如何让 Claude 理解全局架构?

TODO: 上下文管理策略

### 如何规划多步骤重构?

TODO: 分阶段执行,避免一次性大改

### 如何处理 Git 历史?

TODO: 保持 clean commits 的策略

```bash
# TODO: Git commit 策略
git commit -m "refactor: add types for User model"
git commit -m "refactor: extract UserService"
git commit -m "refactor: add tests for UserService"
```

## 踩坑记录

### Claude 理解错误的情况

TODO: 真实案例

### 如何引导 Claude 纠正?

TODO: 人机协作的技巧

### 何时需要人工介入?

TODO: AI 的边界

## Before/After 对比

### 代码质量对比

TODO: 代码示例对比

### 测试覆盖率

```
Before: 0%
After: 85%
```

### 可维护性

TODO: 架构清晰度、文档完整性

## 完整的重构日志

TODO: 展示 Claude 的完整工具调用序列和 Git 提交历史

## 小结

TODO: 总结遗留代码重构的经验,预告下一篇 Git 工作流

---

**系列文章**:
- 上一篇: Claude Code 实战: TDD 工作流
- 下一篇: Claude Code 与 Git 工作流: Commit、PR、Review
