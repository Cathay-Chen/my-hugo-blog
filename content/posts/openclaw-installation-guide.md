---
title: "OpenClaw 安装与配置完全指南: 从坑到成功的完整记录"
date: 2026-02-08T23:50:00+08:00
lastmod: 2026-02-08T23:50:00+08:00
draft: false
tags: ["OpenClaw", "AI", "飞书", "安装教程", "Gateway", "Token"]
categories: ["技术教程"]
author: "cathay"
description: "详细记录 OpenClaw 安装过程，包括 Auth Token 问题解决、飞书第三方 Skill 配置等踩坑经验"
---

## 前言

**OpenClaw** 是一个开源的 AI 助手框架，可以将 Claude 等大模型接入到各种聊天平台（如飞书、微信、Telegram、Discord 等）。本文记录了我从安装到配置的完整过程，包括遇到的坑和解决方案，希望能帮到你。

---

## 一、正常安装步骤

### 1. 一键安装

OpenClaw 提供了官方的一键安装脚本：

```bash
curl -fsSL https://openclaw.ai/install.sh | bash
```

安装完成后，OpenClaw 会被安装到 `~/.openclaw` 目录。

### 2. 验证安装

```bash
openclaw --version
openclaw status
```

### 3. 启动 Gateway

```bash
# 启动 Gateway 服务
openclaw gateway start

# 查看状态
openclaw gateway status
```

---

## 二、踩坑实录: Auth Token 问题解决

### ❌ 问题现象

启动 Gateway 后发现无法正常使用，日志提示认证相关的错误。排查后发现是缺少 Gateway Token。

### 🔧 解决过程

我首先尝试了交互式配置：

```bash
# 查看当前配置
openclaw config

# 交互式配置（手动设置 token）
openclaw configure
```

在 `configure` 过程中，可以重新设置相关的 token 配置项。

### ✅ 最终解决方案

后来发现官方提供了更便捷的命令，可以直接生成 Gateway Token：

```bash
# 一键生成并配置 Gateway Token
openclaw doctor --generate-gateway-token
```

这个命令会自动生成新的 token 并写入配置，比手动配置更方便可靠。

---

## 三、飞书配置: 官方报错，转用第三方 Skill

### ❌ 问题现象

安装官方飞书插件时遇到报错，无法正常使用飞书集成。

### 🔧 解决过程

```bash
# 删除官方飞书插件（如果已安装）
rm -rf /Users/cathay/.openclaw/extensions/feishu

# 安装第三方飞书 Skill（亲测可用）
openclaw plugins install @m1heng-clawd/feishu
```

### ⚙️ 配置飞书

安装完成后，需要进行飞书配置：

```bash
openclaw configure
```

主要配置项：

| 配置项 | 说明 | 获取位置 |
|--------|------|----------|
| `app_id` | 飞书应用 ID | 飞书开发者后台 |
| `app_secret` | 飞书应用密钥 | 飞书开发者后台 |
| `encrypt_key` | 加密密钥（可选） | 飞书事件订阅配置 |
| `verification_token` | 验证令牌 | 飞书事件订阅配置 |

### 📚 参考教程

详细的飞书配置可以参考腾讯云的文章：
- [【保姆级教程】手把手教你安装OpenClaw并接入飞书，让AI在聊天软件里帮你干活-腾讯云开发者社区-腾讯云](https://cloud.tencent.com/developer/article/2626160)
- [OpenClaw 官方飞书文档](https://openclaw.ai/docs/channels/feishu)

---

## 四、OpenClaw 常用命令速查表

### 安装与升级

| 命令 | 说明 |
|------|------|
| `curl -fsSL https://openclaw.ai/install.sh \| bash` | 一键安装 OpenClaw |
| `openclaw --version` | 查看版本 |

### Gateway 管理

| 命令 | 说明 |
|------|------|
| `openclaw gateway start` | 启动 Gateway |
| `openclaw gateway stop` | 停止 Gateway |
| `openclaw gateway restart` | 重启 Gateway |
| `openclaw gateway status` | 查看 Gateway 状态 |
| `openclaw gateway install` | 安装 Gateway 为系统服务 |

### 配置管理

| 命令 | 说明 |
|------|------|
| `openclaw config` | 查看配置 |
| `openclaw configure` | 交互式配置 |

### 诊断与状态

| 命令 | 说明 |
|------|------|
| `openclaw status` | 查看整体状态 |
| `openclaw doctor` | 诊断问题 |
| `openclaw doctor --generate-gateway-token` | 生成 Gateway Token |
| `openclaw health` | 健康检查 |

### 插件管理

| 命令 | 说明 |
|------|------|
| `openclaw plugins install <plugin>` | 安装插件 |
| `openclaw plugins list` | 列出已安装插件 |
| `openclaw plugins remove <plugin>` | 卸载插件 |

### 其他

| 命令 | 说明 |
|------|------|
| `openclaw dashboard` | 打开 Web Dashboard |
| `openclaw help` | 查看帮助 |

---

## 五、我的完整操作流程

根据命令行历史，我的完整操作如下：

```bash
# 1. 安装 OpenClaw
curl -fsSL https://openclaw.ai/install.sh | bash

# 2. 处理飞书插件问题（先删除官方版）
rm -rf /Users/cathay/.openclaw/extensions/feishu

# 3. 安装第三方飞书 Skill
openclaw plugins install @m1heng-clawd/feishu

# 4. 配置（首次设置）
openclaw config
openclaw configure

# 5. 管理 Gateway
openclaw restart gateway
openclaw gateway stop
openclaw gateway start

# 6. 查看状态
openclaw gateway status
openclaw status

# 7. 🔑 关键：生成 Token
openclaw doctor --generate-gateway-token

# 8. 最终验证
openclaw status
```

---

## 六、关键教训与建议

1. **Gateway Token 是必须的**
   - 如果遇到认证问题，使用 `openclaw doctor --generate-gateway-token` 快速解决
   - 这是最容易踩的坑，但解决也很简单

2. **飞书推荐用第三方 Skill**
   - 官方飞书插件可能有兼容性问题
   - `@m1heng-clawd/feishu` 这个第三方 Skill 亲测可用

3. **善用诊断命令**
   - `status` 查看整体状态
   - `doctor` 诊断并修复常见问题
   - `health` 检查健康状态

4. **配置备份**
   - 核心配置文件：`~/.openclaw/openclaw.json`
   - 修改前建议备份

5. **Dashboard 很有用**
   - `openclaw dashboard` 可以打开 Web 管理界面
   - 可以查看会话、配置、状态等

---

## 七、目录结构说明

```
~/.openclaw/
├── openclaw.json          # 主配置文件
├── workspace/             # 工作区（Agent 代码、记忆等）
│   ├── AGENTS.md
│   ├── SOUL.md           # Agent 人格定义
│   ├── TOOLS.md          # 工具配置
│   ├── USER.md           # 用户信息
│   ├── MEMORY.md         # 长期记忆
│   └── memory/           # 记忆文件
├── extensions/            # 插件目录
│   └── feishu/           # 飞书插件
├── agents/               # Agent 配置
│   └── main/
└── logs/                 # 日志文件
```

---

## 八、相关链接

- [OpenClaw 官网](https://openclaw.ai)
- [OpenClaw GitHub](https://github.com/openclaw/openclaw)
- [OpenClaw 官方文档](https://docs.openclaw.ai)
- [OpenClaw 飞书配置文档](https://openclaw.ai/docs/channels/feishu)
- [飞书机器人开发指南 - 腾讯云](https://cloud.tencent.com/developer/article/2306353)

---

## 结语

OpenClaw 是一个功能强大的 AI 助手框架，虽然安装过程中可能会遇到一些小坑（主要是 Token 和飞书插件），但整体来说配置还是比较简单的。现在我已经可以通过飞书随时随地和 Claude 聊天了，非常方便！

如果你也在使用 OpenClaw，欢迎在评论区交流经验！

---

> 💡 **更新提示**: OpenClaw 更新很快，建议关注 [官方文档](https://docs.openclaw.ai) 获取最新信息。
