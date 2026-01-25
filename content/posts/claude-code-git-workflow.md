---
title: "Claude Code 与 Git 工作流: Commit、PR、Review"
date: 2025-08-15T10:00:00+08:00
lastmod: 2025-08-15T10:00:00+08:00
draft: false
tags: ["AI", "IDE", "Claude Code", "Git", "GitHub", "Workflow"]
categories: ["AI技术"]
author: "cathay"
---

## 前言

代码写完只是第一步,如何优雅地提交、创建 PR、响应 Code Review?Claude Code 的 Git 集成让这些流程变得丝滑。本文将展示完整的 Git 工作流。

## Claude Code 的 Git 集成

### 自动分析变更

TODO: git status、git diff 的自动执行

```bash
# TODO: Claude 自动运行的 git 命令
```

### 智能 commit message 生成

TODO: 如何生成专业的 commit message?

### Co-Authored-By 署名

TODO: 人机协作的署名规范

## Commit 工作流

### 如何让 Claude 写出专业的 commit message?

TODO: Conventional Commits 规范

```
feat: add user authentication endpoints
fix: resolve memory leak in file upload
refactor: extract UserService from controller
docs: update API documentation
test: add integration tests for auth flow
```

### 分析变更生成 message

TODO: Claude 如何理解代码变更的意图?

```
Claude 的分析过程:
1. git diff → 查看所有变更
2. 分析: 新增了 auth 相关文件,修改了路由配置
3. 理解意图: 这是添加新功能
4. 生成: "feat: add user authentication with JWT"
```

### 拆分大 commit 的策略

TODO: 如何将大改动拆分为逻辑清晰的小 commits?

## PR 工作流

### gh CLI 集成

TODO: 用 gh 命令创建 PR

```bash
# TODO: gh pr create 命令示例
```

### 自动生成 PR description

TODO: Claude 如何总结变更?

```markdown
# TODO: PR description 示例
## Summary
Added user authentication system with JWT tokens

## Changes
- Implemented `/auth/register` endpoint
- Implemented `/auth/login` endpoint
- Added JWT middleware for protected routes
- Added comprehensive tests (85% coverage)

## Test Plan
- [ ] Manual test registration flow
- [ ] Manual test login flow
- [ ] Verify token expiration handling
- [ ] Run full test suite
```

### Test plan 的生成

TODO: 自动生成测试清单

## Code Review with Claude

### 审查 PR 的工作流

TODO: 用 Claude 进行 pre-review

```bash
# TODO: gh pr view + Claude 分析
```

### 响应 review 评论

TODO: 如何让 Claude 理解 review 评论并修正?

### 自动修复简单问题

TODO: linting、formatting 等简单问题的自动修复

## 实战案例: 从需求到 PR merge

TODO: 完整的流程演示

```
完整流程:
1. 需求: "添加用户认证功能"
2. Claude 开发实现 (TDD 流程)
3. git add + commit (自动生成 message)
4. git push
5. gh pr create (自动生成 description)
6. 等待 Code Review
7. 响应 review 评论,修正代码
8. git commit --amend / 新 commit
9. git push
10. PR merged
```

## Git 命令序列

TODO: 展示完整的 git 命令历史

## 最佳实践

TODO: Git 工作流的经验总结

## 小结

TODO: 总结 Git 工作流的价值,预告下一篇 Claude Code 的边界

---

**系列文章**:
- 上一篇: Claude Code 实战: 遗留代码重构
- 下一篇: Claude Code 的边界: 能做什么,不能做什么
