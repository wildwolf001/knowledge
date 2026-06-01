# 附录 A — 核心资源索引

> 2026 年最新版。按章节索引的论文、博客、框架文档和评估基准资源。

---

## 面试备考资料

- [Datawhale hello-agents 面试总结](https://github.com/datawhalechina/hello-agents) — 真实秋招面经 + 参考答案
- [DolbyUUU 面试题合集](https://github.com/DolbyUUU/Awesome-LLM-Interview-Questions-and-Answers) — 2025-2026 年大厂面试真题
- [guoguo-tju agent_java_offer](https://github.com/guoguo-tju/agent_java_offer) — 后端转 AI Agent 的结构化复习资料库
- [AI System Design Guide](https://github.com/ombharatiya/ai-system-design-guide) — 110+ 面试题 + 答题框架

---

## 核心论文（2022-2026）

| 论文 | 年份 | 核心贡献 | 对应章节 |
|------|------|----------|----------|
| ReAct (Yao et al.) | 2022 | Reasoning + Acting 交替循环 | 02-Agent核心循环 |
| Reflexion (Shinn et al.) | 2023 | 情景自我反思跨试验 | 02/14-自验证循环 |
| MemGPT (Packer et al.) | 2023 | OS 启发式记忆分层与分页 | 07-记忆系统设计 |
| Toolformer (Schick et al.) | 2023 | 预训练阶段学习 Token 级工具调用 | 09-Tool-Function-Calling |
| Lost in the Middle (Liu et al.) | 2023 | 长上下文中间信息被系统性忽略 | 05-Context-Engineering |
| **EvoGraph-R1 (CVPR)** | **2026** | 自进化多模态知识超图 Agentic 检索 | 08-RAG/GraphRAG |
| **HyperGraphPro (arXiv)** | **2026** | 超图检索+强化学习，进度驱动策略优化 | 08-RAG/GraphRAG |
| **Youtu-GraphRAG (ICLR)** | **2026** | 垂直统一 Agentic GraphRAG，33.6%成本节省 | 08-RAG/GraphRAG |
| **RAGSearch Benchmark** | **2026** | Agentic Search vs GraphRAG 系统性对比 | 08-RAG评估 |
| **Anthropic Agentic Coding Report** | **2026** | 60%工作使用AI，27%是新附加任务 | 26-AI-Agent前沿 |
| MemFlow (Chen et al.) | 2026 | 意图驱动的记忆编排 | 07-记忆系统设计 |
| GUARDIAN (Zhou et al.) | 2025 | 多 Agent 幻觉传播的时序图检测 | 12-Multi-Agent |
| JSONSchemaBench (Geng et al.) | 2025 | 受控解码的标准化基准 | 15-结构化输出 |
| PARSE (EMNLP) | 2025 | LLM 驱动的 Schema 优化，+64.7%准确率 | 15-结构化输出 |
| The Hidden Cost of Structure (Schall) | 2025 | 受控解码对指令微调模型的退化 | 14/15-约束生成代价 |
| When Refusals Fail (Hadeliya) | 2025 | 长上下文 Agent 的安全机制退化 | 05-Context-Engineering |
| **MCP STDIO RCE (OX Security)** | **2026** | 跨所有 MCP SDK 的远程代码执行漏洞 | 17-安全防护 |

---

## 关键文章与博客（2025-2026）

- [**Anthropic: MCP + Skills — 手与脑的关系**](https://www.anthropic.com) — 2026年4月正式定义 MCP/Skills 分工
- [**Anthropic: Advanced Tool Use Suite**](https://www.anthropic.com) — Tool Search + PTC + Examples 三项功能详解
- [**Google Cloud Next 2026: Agent Chaos to Engineered Intelligence**](https://thecuberesearch.com/agent-chaos-to-engineered-intelligence/) — 78%企业AI失败源于上下文管理
- [**NVIDIA GTC 2026: Claws Strategy & Agent AI Infrastructure**](https://counterpointresearch.com/) — NemoClaw + OpenShell + DGX
- [**12-Factor Agents**](https://github.com/allarddewinter/my-blog) — 受 12-Factor App 启发的 Agent 方法论
- [**11 Problems Building Agents (Composio)**](https://composio.dev/) — 生产实践踩坑合集
- [**Design Patterns for Agentic Workflows (HuggingFace)**](https://huggingface.co/blog/) — 六种基础 Agent 设计模式
- [**Building Reliable AI Workflows (GitHub Blog)**](https://github.blog/ai-and-ml/) — Markdown → Agentic Primitives → Context Engineering
- [**Tool Descriptions Eating Tokens (CNCF)**](https://www.cncf.io/blog/) — 工具描述 Token 消耗真实分析
- [**Agent Patterns v0.2.0**](https://agent-patterns.readthedocs.io) — 9 种生产就绪 Agent 模式
- [**Bilibili Data AI 探索和实践**](https://mp.weixin.qq.com) — B站 Multi-Agent + MCP 生产演进
- [**MCP Dev Summit 2026 (Linux Foundation)**](https://modelcontextprotocol.io) — MCP 生态年度大会
- [**MCP vs A2A in 2026**](https://futureagi.com/blog/mcp-vs-a2a-2025/) — 两大协议定位与选型

---

## 框架文档

| 框架 | 2026 状态 | 文档链接 |
|------|----------|---------|
| LangGraph | ✅ 活跃 (SDK 0.3.14) | [docs](https://langchain-ai.github.io/langgraph/) |
| CrewAI | ✅ 活跃 (v1.14.4) | [docs](https://docs.crewai.com/) |
| AutoGen | ⛔ 维护模式 | [docs](https://microsoft.github.io/autogen/) |
| **Microsoft Agent Framework** | ✅ AutoGen 官方继任者 | [docs](https://learn.microsoft.com/ai/agent-framework) |
| AG2 | ✅ 社区分支 (v0.12.3) | [github](https://github.com/ag2ai/ag2) |
| Agno (原 Phidata) | ✅ 活跃 | [docs](https://docs.agno.com/) |
| Google ADK | ✅ 活跃 | [docs](https://google.github.io/adk-docs/) |
| OpenAI Agents SDK | ✅ 活跃 | [docs](https://platform.openai.com/docs/guides/agents) |
| Mastra | ✅ TypeScript 原生 | [docs](https://mastra.ai/) |
| **MCP 协议** | ✅ Linux Foundation 治理 | [spec](https://modelcontextprotocol.io/) |
| **A2A 协议** | ✅ Linux Foundation 治理 | [spec](https://a2a-protocol.org/) |
| OpenClaw | ✅ 开源 Computer Use 框架 | [github](https://github.com/OpenClaw/OpenClaw) |

---

## Agent 评估基准

| 基准 | 维度 | 2026 领先模型/分数 | 对应章节 |
|------|------|-------------------|----------|
| **SWE-bench Verified** | 软件工程 | Claude Opus 4.5 80.9% | 20-评估体系 |
| **SWE-bench Pro (SEAL)** | 多语言软件工程 | Claude Opus 4.5 45.9% | 20-评估体系 |
| **OSWorld-Verified** | Computer Use/GUI | Claude Opus 4.6 72.7% | 26-Computer Use |
| **Terminal-Bench 2.0** | 终端/CLI 技能 | GPT-5.3-Codex 77.3% | 20-评估体系 |
| **ARC-AGI-2** | 抽象推理 | Claude Opus 4.6 68.8% | 27-模型前沿 |
| **GPQA Diamond** | 研究生级科学 | Claude Opus 4.6 91.3% | 27-模型前沿 |
| **Humanity's Last Exam** | 极限推理(带工具) | Claude Opus 4.6 53.1% | 27-模型前沿 |
| **FrontierMath** | 数学推理 | Claude Opus 4.6 40.7% | 27-模型前沿 |
| **GAIA** | 通用 AI 助手 | — | 20-评估体系 |
| **WebArena** | 真实网站交互 | — | 20-评估体系 |
| **MCP Atlas** | 工具使用 | Claude Sonnet 4.6 61.3% | 09-Tool-Calling |
| **Finance Agent** | 金融 Agent | Claude Sonnet 4.6 63.3% | 20-评估体系 |
| **RAGSearch** | Agentic RAG 搜索 | 2026 新基准 | 08-RAG评估 |

---

*另见：[附录 B — 技术栈速查表](./B-技术栈速查表.md) | [附录 C — 术语表中英对照](./C-术语表中英对照.md) | [附录 D — 面试高频 50 题索引](./D-面试高频50题索引.md)*
