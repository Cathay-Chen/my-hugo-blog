# AI 技术博文系列设计文档

## 项目概述

为面试准备,创建一个从 RAG 技术到 AI Agent 生态,再到 AI IDE 开发工具的完整技术博文系列。时间线覆盖 2022-2025,共 21 篇文章,展示对 AI 应用技术栈的深度理解和实践经验。

## 目标受众

- **主要**: 技术面试官 - 展示技术深度和实践经验
- **次要**: 同行开发者 - 分享技术演进和实战经验

## 内容策略

- **理论实践混合**: 前期(RAG/Agent)偏理论和架构思考,后期(AI IDE)偏实战经验
- **代码比例**: 理论为主(20-30%代码),关键点用代码验证
- **技术时间线**: 2022-2025 完整周期

## 实践经验背景

- **工具深度用户**: Cursor/Claude Code 重度使用者,有工作流优化经验
- **理论研究**: RAG/Agent 框架的学习和研究
- **写作策略**:
  - 前期 RAG/Agent: 技术演进分析和架构思考
  - 后期 AI IDE: 深度实战经验和最佳实践

## 文章分布结构

**金字塔结构 (3 + 6 + 12 = 21篇)**:
- RAG 基础篇: 3→4 篇(打基础)
- Agent 进阶篇: 5→6 篇(讲演进,加入 MCP/A2A/A2UI)
- AI IDE 深度篇: 12→11 篇(深度实战,重点 Claude Code)

调整后最终: **4 + 6 + 11 = 21 篇**

---

## 第一部分: RAG 基础篇 (4篇, 2022-2023)

### 1. 《向量嵌入的数学本质: 从 Word2Vec 到 Transformer Embedding》

**时间定位**: 2022.11-2023.01
**核心内容**:
- 为什么要把文本变成向量? 语义相似性的几何表达
- Word2Vec 的直觉: CBOW vs Skip-gram,词向量的代数性质(king - man + woman = queen)
- Sentence-BERT 的突破: 如何表达句子级语义
- OpenAI text-embedding-ada-002 vs 开源模型(all-MiniLM, BGE, E5)
- 距离度量对比: cosine similarity, euclidean distance, dot product 的选择逻辑

**技术深度**: 20% 代码,展示向量计算和相似度对比,重点是数学直觉和几何理解

---

### 2. 《知识图谱与向量数据库: 两种知识表达范式的碰撞》

**时间定位**: 2023.01-2023.04
**核心内容**:
- 向量数据库的兴起(Pinecone, Weaviate, Milvus, Chroma)
- 图数据库的知识表达(Neo4j, 实体关系的显式建模)
- 两种范式的本质差异: 模糊相似 vs 精确关系
- 混合方案: GraphRAG 的思想萌芽,向量检索 + 图遍历
- 为什么大部分 RAG 选择了向量而不是图?

**技术深度**: 理论为主,架构对比,少量伪代码展示检索逻辑差异

---

### 3. 《从文本切块到语义检索: RAG 的工程化实践》

**时间定位**: 2023.04-2023.07
**核心内容**:
- Chunking 策略对比(固定长度 vs 递归字符分割 vs 语义分割)
- Overlap 的必要性: 避免语义断裂
- 检索策略演进: naive vector search → hybrid search(BM25 + vector) → reranking
- 元数据过滤的实战价值(时间、来源、标签)
- LangChain/LlamaIndex 的 Document Loader 和 Retriever 设计

**技术深度**: 30% 代码,展示不同 chunking 对检索效果的影响,代码示例用 Python + LangChain

---

### 4. 《RAG 的记忆系统: 从无状态到有状态的演进》

**时间定位**: 2023.07-2023.10
**核心内容**:
- 早期 RAG 的问题: 每次对话都是新的,无法记住上下文
- Short-term Memory: 对话历史的滑动窗口管理
- Long-term Memory: 将对话摘要存入向量库,形成"经验积累"
- Memory 的分层设计: Working Memory + Episodic Memory + Semantic Memory
- 引出 Agent 思想: 记忆系统是 Agent 的基础能力

**技术深度**: 理论为主,架构图和伪代码,为 Agent 篇做铺垫

---

## 第二部分: Agent 进阶篇 (6篇, 2023-2024)

### 5. 《从 AutoGPT 到 Agent 范式: AI 为什么需要"自主性"?》

**时间定位**: 2023.03-2023.06
**核心内容**:
- AutoGPT 的震撼: 第一次看到 AI "自己规划、自己执行"
- Agent 的本质: Goal-driven vs Prompt-driven 的范式转变
- Agent 的核心能力三要素: Planning(规划), Memory(记忆), Tool Use(工具使用)
- 为什么 RAG 不够? 从被动检索到主动决策
- 早期 Agent 的失败案例: 无限循环、目标偏移、成本爆炸

**技术深度**: 理论为主,架构对比,展示 Agent 的思维链路 vs 传统 Prompt 的差异

---

### 6. 《Function Calling 与 MCP: Agent 工具接口的标准化之路》

**时间定位**: 2023.06-2024.11
**核心内容**:
- OpenAI Function Calling 的标准化(2023.06.13): Tool Schema 设计
- 从硬编码到动态注册: LangChain Tools, LlamaIndex Tools
- Anthropic MCP 协议的登场(2024.11): 为什么需要新标准?
- MCP 的核心设计: Server-Client 架构, Resources/Tools/Prompts 三大原语
- Function Calling vs MCP 的本质差异: API 调用 vs 上下文协议
- 实战案例: 用 MCP 构建文件系统、数据库、API 访问工具

**技术深度**: 40% 代码,对比 Function Calling 和 MCP 的实现,Python + TypeScript 示例

---

### 7. 《ReAct 与 Chain-of-Thought: Agent 的推理模式演进》

**时间定位**: 2023.09-2023.12
**核心内容**:
- Chain-of-Thought (CoT): 让 LLM "说出思考过程"
- ReAct 框架: Reasoning + Acting 的交替循环
- 对比其他推理模式: ReWOO, Plan-and-Execute, Reflection
- Few-shot prompting 在 Agent 中的关键作用
- 为什么 o1/o3 模型让 ReAct 变得不那么必要?

**技术深度**: 理论为主,Prompt 示例对比,展示不同推理模式的思维链差异

---

### 8. 《Plan-and-Execute 与 Self-Reflection: 复杂 Agent 架构》

**时间定位**: 2023.12-2024.03
**核心内容**:
- 简单 ReAct Agent 的局限: 短视、易偏离目标
- Plan-and-Execute 模式: LangGraph 的设计哲学
- Self-Reflection 机制: Agent 如何"反思"和纠错
- BabyAGI 和 GPT-Engineer 的架构分析
- Agentic Workflow vs Chatbot Workflow 的本质差异

**技术深度**: 30% 代码,架构图 + LangGraph 示例,展示状态机和控制流

---

### 9. 《Multi-Agent 系统: A2A 协议与协作涌现》

**时间定位**: 2024.03-2024.08
**核心内容**:
- 为什么需要 Multi-Agent? 单个 Agent 的能力上限
- 协作模式: 辩论(Debate), 层级(Hierarchical), 并行(Parallel)
- AutoGen 框架: Conversable Agents 的设计
- CrewAI: Role-based Agent 协作
- **A2A (Agent-to-Agent) 通信协议**: 消息格式、状态同步、错误处理
- Multi-Agent 的挑战: 通信成本、一致性、死锁问题

**技术深度**: 30% 代码,架构对比,展示 A2A 消息协议和 AutoGen 示例

---

### 10. 《Agent UI 框架: 从 Google Assistant 到 Vercel assistant-ui》

**时间定位**: 2024.06-2024.12
**核心内容**:

**Part 1: 对话式 UI 的设计范式**
- Google Assistant UI 的设计哲学: 对话即界面
- 对话式交互的核心组件: Intent, Entity, Context, Fulfillment
- 从语音到多模态: Actions on Google 的演进
- 对话流的状态管理: Session state vs User state

**Part 2: Vercel AI SDK 生态**
- RSC (React Server Components) + AI 的化学反应
- `ai` 包核心 API: useChat, useCompletion, streamText, streamUI
- `assistant-ui`: 开箱即用的 Agent 对话组件
- Generative UI 的突破: 从文本到动态组件生成
- 实战案例: 用 assistant-ui 构建一个支持工具调用的 Agent 界面

**Part 3: 为什么 AI IDE 是下一站?**
- 对话式 UI 的局限: 缺乏持久状态、无法处理复杂工作流
- IDE 的天然优势: 文件系统、终端、Git、LSP 都是现成的"工具"
- 引出 Cursor 和 Claude Code: 把 Agent 嵌入开发环境

**技术深度**: 40% 代码,Google Assistant 的 intent schema + Vercel AI SDK 完整示例(Next.js + assistant-ui)

---

## 第三部分: AI IDE 深度篇 (11篇, 2024-2025)

### 11. 《AI IDE 的三个世代: Copilot、Cursor、Claude Code》

**时间定位**: 2024.01-2024.09
**核心内容**:
- **第一代: GitHub Copilot (2021-2023)**
  - 自动补全范式,基于上下文的代码建议
  - 局限: 单文件视角,无法理解全局架构
- **第二代: Cursor, Augment Code (2023-2024)**
  - Codebase-aware,全局代码理解
  - Chat + Composer 模式,多文件编辑
  - 局限: 仍然是辅助工具,需要人驱动
- **第三代: Claude Code (2024-)**
  - Agent-first 设计,从对话到自主执行
  - 工具生态: MCP、Skills、可扩展性
  - 范式转变: 从"辅助编程"到"协作开发"
- 三代对比表: 能力矩阵、使用场景、技术架构

**技术深度**: 理论为主,功能对比表,架构图

---

### 12. 《Cursor 与 Augment Code: GUI 驱动的 AI IDE》

**时间定位**: 2024.06-2024.12
**核心内容**:
- **Cursor 的核心能力**:
  - Tab 补全 + Chat 对话 + Composer 多文件编辑
  - @-mentions 上下文管理
  - .cursorrules 项目定制
  - 优势: GUI 友好,上手快,IDE 集成度高
  - 局限: Agent 自主性有限,复杂任务需要多次交互

- **Augment Code 的设计哲学**:
  - 类似 Cursor 但更激进的自动化
  - 后台持续分析代码,主动提出改进建议
  - 优势: 更智能的主动提示
  - 局限: (如果你用过可以补充,没用过可以简单带过)

- **为什么 Claude Code 是下一步?**
  - GUI 的天花板: 复杂工作流的交互成本
  - CLI + Agent 的优势: 完整的工具链访问、更强的自主性

**技术深度**: 30% 实战截图,展示 Cursor 的使用场景,引出 Claude Code

---

### 13. 《Claude Code 架构解析: Agent、Tools、MCP》

**时间定位**: 2024.11-2024.12
**核心内容**:
- **Claude Code 的核心架构**:
  - Agent 循环: Thinking → Tool Use → Observation → Reflection
  - 工具系统: Read, Edit, Write, Bash, Glob, Grep, Task, AskUserQuestion
  - Context 管理: 如何在有限窗口内保持全局理解

- **与 Cursor 的本质差异**:
  - Cursor: 等待用户指令,执行单步操作
  - Claude Code: Goal-driven,自主规划多步骤任务

- **MCP 集成的意义**:
  - 为什么 Claude Code 原生支持 MCP?
  - 工具扩展的标准化路径

- **技术架构图**: Agent loop + Tool execution flow + MCP protocol

**技术深度**: 理论为主,架构图,伪代码展示 Agent 决策流程

---

### 14. 《Claude Code 工具系统深度解析》

**时间定位**: 2024.12-2025.01
**核心内容**:
- **文件操作工具**:
  - Read: 智能分页,避免上下文溢出
  - Edit: 精确字符串替换,preserving context
  - Write: 新建文件,何时用 Write vs Edit
  - Glob: 文件查找,pattern matching
  - Grep: 代码搜索,正则表达式

- **执行工具**:
  - Bash: 命令执行,git、npm、测试运行
  - Task: 子 Agent 调度,并行任务处理

- **交互工具**:
  - AskUserQuestion: 决策点的人类介入

- **工具组合的艺术**:
  - 如何用 Grep + Read 理解代码
  - 如何用 Edit + Bash 实现测试驱动开发
  - 如何用 Task 并行处理多个独立任务

- **实战案例**: 用工具组合完成一个完整功能开发

**技术深度**: 40% 代码,展示工具调用序列,实际执行日志

---

### 15. 《MCP Server 开发: 为 Claude Code 扩展能力》

**时间定位**: 2024.12-2025.02
**核心内容**:
- **MCP 协议回顾**:
  - Server-Client 架构
  - Resources, Tools, Prompts 三大原语

- **开发 MCP Server 的完整流程**:
  - 环境搭建: TypeScript + @modelcontextprotocol/sdk
  - Server 结构: stdio transport, tool registration
  - Tool schema 设计: 参数定义、错误处理

- **实战案例 1: 文件系统 MCP Server**:
  - 提供高级文件操作(批量重命名、目录对比)

- **实战案例 2: 数据库 MCP Server**:
  - 连接 PostgreSQL,提供查询和修改能力

- **实战案例 3: API 集成 MCP Server**:
  - 集成 Linear/Jira,从任务管理到代码实现的闭环

- **调试和测试**: 如何验证 MCP Server 工作正常

**技术深度**: 60% 代码,完整的 MCP Server 实现(TypeScript)

---

### 16. 《Claude Code Skills 系统: 可复用的 Agent 工作流》

**时间定位**: 2025.01-2025.03
**核心内容**:
- **Skills 的设计哲学**:
  - 为什么需要 Skills? Agent 的"肌肉记忆"
  - Skill 的本质: 结构化的 prompt + 工作流定义

- **Skill 的结构**:
  - Metadata: name, description, triggers
  - Instructions: 详细的执行步骤
  - Examples: few-shot learning

- **内置 Skills 解析**:
  - /commit: Git 提交的最佳实践流程
  - /test: 测试驱动开发工作流
  - /review: 代码审查工作流

- **自定义 Skills 开发**:
  - 场景 1: 创建 /deploy skill,自动化部署流程
  - 场景 2: 创建 /refactor skill,结构化重构策略
  - 场景 3: 创建 /doc skill,自动生成文档

- **Skills 的组合**: 如何让 Skills 相互调用

**技术深度**: 40% 代码,Skill 定义示例(Markdown + YAML)

---

### 17. 《Claude Code 实战: TDD 工作流》

**时间定位**: 2025.02-2025.03
**核心内容**:
- **TDD with Claude Code 的完整流程**:
  - 第一步: 描述需求
  - 第二步: Claude 生成测试用例
  - 第三步: 运行测试,验证失败
  - 第四步: Claude 实现功能
  - 第五步: 运行测试,验证通过
  - 第六步: 重构优化

- **实战案例: 开发一个 REST API**:
  - 需求: 用户认证系统(注册、登录、token 刷新)
  - 完整的 TDD 流程演示
  - Claude 的工具调用序列
  - 遇到的问题和修正

- **Claude Code 在 TDD 中的优势**:
  - 自动运行测试,根据错误信息修正代码
  - 并行生成多个测试用例
  - 边界情况的自动补充

- **效率对比**: AI 辅助 TDD vs 传统手工 TDD

**技术深度**: 60% 实战,完整的代码演示,测试输出日志

---

### 18. 《Claude Code 实战: 遗留代码重构》

**时间定位**: 2025.03-2025.04
**核心内容**:
- **场景设定**:
  - 一个混乱的 Node.js 项目
  - 问题: 无类型约束、逻辑混乱、无测试
  - 目标: 迁移到 TypeScript + 分层架构 + 测试覆盖

- **重构策略**:
  - 第一阶段: 理解现有代码(Glob + Grep + Read)
  - 第二阶段: 补充测试(保证不破坏功能)
  - 第三阶段: 类型定义(逐步迁移 TypeScript)
  - 第四阶段: 架构重构(提取 service layer)
  - 第五阶段: 验证和清理

- **Claude Code 的工作流**:
  - 如何让 Claude 理解全局架构
  - 如何规划多步骤重构
  - 如何处理 Git 历史(保持 clean commits)

- **踩坑记录**:
  - Claude 理解错误的情况
  - 如何引导 Claude 纠正
  - 何时需要人工介入

- **Before/After 对比**: 代码质量、测试覆盖率、可维护性

**技术深度**: 60% 实战,大量代码对比,Git commit 历史

---

### 19. 《Claude Code 与 Git 工作流: Commit、PR、Review》

**时间定位**: 2025.04-2025.05
**核心内容**:
- **Claude Code 的 Git 集成**:
  - 自动 git status、git diff 分析
  - 智能 commit message 生成
  - Co-Authored-By 署名

- **Commit 工作流**:
  - 如何让 Claude 写出专业的 commit message
  - Conventional Commits 规范
  - 拆分大 commit 的策略

- **PR 工作流**:
  - gh CLI 集成
  - 自动生成 PR description
  - Test plan 的生成

- **Code Review with Claude**:
  - 审查 PR 的工作流
  - 响应 review 评论
  - 自动修复简单问题

- **实战案例**: 从需求到 PR merge 的完整流程

**技术深度**: 50% 实战,Git 命令序列,PR 截图

---

### 20. 《Claude Code 的边界: 能做什么,不能做什么》

**时间定位**: 2025.05-2025.08
**核心内容**:
- **Claude Code 的优势场景**:
  - 明确需求的功能开发
  - 代码重构和优化
  - 测试编写和 bug 修复
  - 文档生成和维护

- **Claude Code 的局限**:
  - 模糊需求的探索(需要更多人机交互)
  - 大规模架构重构(超出上下文窗口)
  - 性能调优(需要 profiling 和深度分析)
  - 创新性算法设计(需要人的创造力)

- **与其他工具的配合**:
  - Cursor: GUI 友好,快速原型,交互式开发
  - Claude Code: 复杂工作流,自动化任务,批量处理
  - 组合使用的最佳实践

- **我的工作流**:
  - 日常开发: Cursor(70%) + Claude Code(30%)
  - 大型重构: Claude Code(80%) + 人工验证(20%)
  - 学习新项目: Cursor 快速浏览 + Claude Code 深度分析

- **真实踩坑案例**: Claude Code 搞砸的场景和教训

**技术深度**: 理论为主,大量真实案例,使用建议

---

### 21. 《AI Agent 开发工作流的未来》

**时间定位**: 2025.08-2025.12
**核心内容**:
- **从 IDE 到 Agent 平台**:
  - Claude Code 的进化方向
  - Devin、GPT-Engineer、Smol Developer 的启示
  - 完全自主的软件工程 Agent 可能吗?

- **技术挑战**:
  - 上下文窗口的极限: 如何理解百万行代码?
  - 验证和测试: 如何保证 Agent 生成代码的质量?
  - 人机协作: 何时需要人介入,何时完全自主?

- **开发范式的转变**:
  - 从"写代码"到"描述需求"
  - 程序员的新角色: 架构师 + 产品经理 + Code Reviewer
  - "编程素养"的重新定义

- **MCP 生态的未来**:
  - 工具标准化带来的可能性
  - Agent 之间的协作(Multi-Agent Systems)
  - 从个人工具到团队协作平台

- **我的观点**:
  - AI 不会取代程序员
  - 但"不会用 AI 的程序员"会被淘汰
  - 未来的编程: 人的创造力 + AI 的执行力

**技术深度**: 理论为主,趋势分析,个人见解和预测

---

## 实施计划

### 第一阶段: 准备(1-2天)
- [ ] 创建 21 个 Hugo 博文 Markdown 文件框架
- [ ] 设置统一的 front matter(标题、日期、标签、分类)
- [ ] 准备图片/图表资源目录

### 第二阶段: 撰写(分批执行)
- [ ] **Batch 1**: RAG 基础篇 (1-4)
- [ ] **Batch 2**: Agent 进阶篇 (5-10)
- [ ] **Batch 3**: AI IDE 深度篇前半 (11-16)
- [ ] **Batch 4**: AI IDE 深度篇后半 (17-21)

### 第三阶段: 完善
- [ ] 添加代码示例和实战演示
- [ ] 补充架构图和对比表
- [ ] 交叉引用和内链优化
- [ ] SEO 优化(关键词、meta description)

### 第四阶段: 发布
- [ ] 按时间线顺序发布(模拟技术发展)
- [ ] 社交媒体同步(Twitter, LinkedIn)
- [ ] 收集反馈和优化

---

## 关键成功因素

1. **真实性**: 基于实际使用经验,避免纸上谈兵
2. **深度**: 不仅介绍是什么,更要讲为什么和怎么做
3. **系统性**: 21 篇形成完整的知识体系,相互引用
4. **时效性**: 符合技术发展的真实时间线
5. **实用性**: 提供可执行的代码和可复现的案例

---

## 标签体系

- **技术标签**: RAG, Vector Database, LLM, Agent, MCP, AI IDE, Cursor, Claude Code
- **主题标签**: Machine Learning, Software Engineering, Developer Tools, Workflow
- **系列标签**: AI-Tech-Series-2022-2025

---

## 参考资源

### RAG 相关
- LangChain Documentation
- LlamaIndex Documentation
- Pinecone Blog
- Weaviate Blog

### Agent 相关
- AutoGPT GitHub
- LangGraph Documentation
- AutoGen Documentation
- CrewAI Documentation
- Anthropic MCP Documentation

### AI IDE 相关
- Cursor Documentation
- Claude Code Documentation
- Vercel AI SDK Documentation
- GitHub Copilot Blog

---

**文档版本**: v1.0
**创建日期**: 2026-01-25
**最后更新**: 2026-01-25
