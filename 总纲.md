# AI Agent 工程知识体系 · 总纲

> 面向 AI Agent 工程师的系统化知识框架，覆盖从底层原理到生产落地的完整链路。每章标注了子章节数、核心内容、面试权重和撰写优先级。

---

## 阅读路径图

| 读者背景 | 推荐阅读顺序 | 说明 |
|----------|-------------|------|
| **Agent 新手** | Part 1 → Part 2 → Part 3 → Part 5 → Part 6 → Part 8 | 先建立核心概念，再深入上下文工程和工具，最后学部署 |
| **有经验的 LLM 工程师** | Part 2 → Part 4 → Part 7 → Part 9 → Part 10 | 重点在上下文工程、多 Agent 和可观测性等进阶主题 |
| **面试备考** | Part 2 → Part 1(Ch4) → Part 3 → Part 5 → Part 6(Ch17,18) → Part 7(Ch20) → Part 8(Ch21) | 按面试权重从高到低，集中突破高频考点 |
| **架构师/TL** | Part 4 → Part 6 → Part 7 → Part 8(Ch21) → Part 9 → Part 10 | 聚焦架构设计、安全容错、生产踩坑和前沿方向 |
| **查阅式阅读** | 善用附录 D「面试高频 50 题索引」反向定位章节 | 遇到具体问题或面试题时快速定位 |

> **优先级说明**：P0 = 核心必写（面试高频 + 生产必需），P1 = 重要选写，P2 = 可暂缓（前沿/参考级别）。优先完成 P0 章节，再逐步补充 P1、P2。

---

## 第一部分：Agent 核心原理（4 章）

### 01 — LLM 推理基础（5 节）[P1]
> 理解模型如何"思考"，是所有 Agent 设计的起点。本章建立对 Transformer 架构、推理模式和主流模型能力的统一认知。

- 1.1 Transformer 自注意力与 KV Cache —— 为什么长上下文成本是 O(n²)
- 1.2 Tokenization 的工程影响 —— BPE vs SentencePiece、中文分词的 token 膨胀问题
- 1.3 上下文窗口 —— 从 4K 到 2M 的演进、注意力衰减曲线、"Lost in the Middle" 现象
- 1.4 推理模式 —— Next-Token / CoT / ToT / Thinking Tokens / 推理时扩展（Test-time Compute）
- 1.5 主流模型能力矩阵 —— GPT-4o / Claude 4.5 / Gemini 2.5 / DeepSeek-V3 / Qwen3 / MiniMax 的横向对比

### 02 — Agent 核心循环（5 节）[P0]
> Agent 和 Chatbot 的本质区别是什么？本章拆解 Agent 的"大脑回路"——Think→Act→Observe 循环及其变体。

- 2.1 ReAct —— Thought → Action → Observation 交替执行，适合路径不确定的任务
- 2.2 Plan-and-Execute —— 先规划再执行，何时比 ReAct 更优
- 2.3 Plan-then-ReAct 混合模式 —— 工业界最常用的折中：大步骤规划 + 子步骤灵活执行
- 2.4 Reflexion —— 引入反思记忆解决长周期任务状态遗忘，自我纠错循环
- 2.5 Agent 四组件 —— LLM（大脑）+ Planning（规划）+ Memory（记忆）+ Tools（工具）

### 03 — Embedding 与向量检索（5 节）[P1]
> Agent 如何"理解"文本语义？Embedding 是 RAG、记忆检索、语义搜索的基石。本章覆盖从原理到选型。

- 3.1 文本 Embedding 原理 —— 对比学习、Matryoshka 表示、多语言模型（BGE / text-embedding-3）
- 3.2 向量数据库选型 —— ChromaDB vs Milvus vs Qdrant vs Pinecone 的架构差异与适用场景
- 3.3 ANN 索引算法 —— HNSW / IVF / DiskANN 的精度-速度-内存三角权衡
- 3.4 分块策略基础 —— 各分块方法对 Embedding 质量的影响概述（深入见 8.2）
- 3.5 检索-重排序流水线 —— Cross-Encoder Reranker 如何将 Hit Rate 从 70% 提到 95%

### 04 — 主流 Agent 框架深度对比（6 节）[P0]
> 2025 年 Agent 框架百花齐放。本章深入对比四大主流框架的架构哲学、性能差异和选型逻辑。

- 4.1 LangGraph —— 图状态机架构、自动检查点（checkpointing）、时间旅行调试，适合复杂多步骤工作流
- 4.2 CrewAI —— 角色化团队抽象、YAML 配置驱动、低代码上手，适合内容生产流水线
- 4.3 AutoGen（Microsoft）—— Actor Model 异步消息驱动、三层架构（Core/AgentChat/Extensions）、GAIA 基准 #1
- 4.4 Agno（原 Phidata）—— 轻量高性能（实例化比 LangGraph 快 529 倍）、内置 Session Memory、关注点分离
- 4.5 其他框架技术定位 —— PydanticAI / DSPy / LangChain / LlamaIndex 的技术架构与核心场景对比（社区生态与趋势见 26.7）
- 4.6 选型决策指南 —— 按复杂度 × 性能 × 合规 × 团队能力的四维评估矩阵

---

## 第二部分：上下文工程与记忆（4 章）

> **面试最高频考点**。核心矛盾：上下文窗口有限，但任务需要无限记忆。本章覆盖从 Token Budget 到长期记忆的完整方案。

### 05 — Context Engineering（6 节）[P0]
> "Prompt Engineering 已死，Context Engineering 当立"——Karpathy。本章涵盖上下文管理的全套策略。

- 5.1 上下文五层竞争模型 —— System Instructions / Tool Definitions / Memory / Retrieval / User Input 共享同一个 token 池
- 5.2 Token Budget 策略 —— 缓存稳定层、摘要压缩历史、工具懒加载、输出 capping、递减收益检测
- 5.3 渐进式信息披露 L0-L3 —— Task → Evidence Index → Evidence Fragments → Full Evidence，按需加载
- 5.4 上下文压缩体系 —— Micro（清旧工具结果）/ Auto（LLM 摘要）/ Reactive（API 报错触发）/ SessionMemory（零成本）
- 5.5 Prompt Cache —— Static/Dynamic 分离、工具 Schema 排序保证缓存键稳定、全局缓存作用域（跨用户共享）
- 5.6 长上下文的工程现实 —— "1M token 窗口"广告 vs 100K 即退化 50% 的现实（2025 年论文验证），对上下文预算和压缩策略的影响（底层 Attention 机制分析见 27.6）

### 06 — Prompt 工程（5 节）[P0]
> 系统提示词是 Agent 的"宪法"。本章涵盖提示词的架构设计、模板化、版本管理和 AB 测试。

- 6.1 System Prompt 架构 —— Base + Rules + Context + Tools + Skills 的分层设计
- 6.2 Static/Dynamic 分离 —— 哪些缓存、哪些每轮重建、缓存破裂检测
- 6.3 提示词压缩 —— 从"教科书"风格（3,500 字符）到"执行手册"风格（1,500 字符），节省 60% token
- 6.4 Jinja2 模板引擎 + 版本管理 —— 可回滚、可对比、可审计的提示词迭代
- 6.5 环境感知注入 —— 根据 OS / Shell 类型 / 模型能力 / 可用工具动态调整提示词

### 07 — 记忆系统设计（7 节）[P0]
> Agent 的"海马体"——如何让 Agent 记住昨天和用户说过的话？本章从认知科学到工程实现。

- 7.1 三层记忆架构 —— Working Memory（上下文窗口）/ Short-Term（Redis 会话）/ Long-Term（向量 DB）
- 7.2 MemGPT 的 OS 启发模型 —— 主内存 + 虚拟内存分页 + 内存压力告警（>70% 触发 eviction）
- 7.3 记忆类型 —— Episodic（情景）/ Semantic（语义）/ Procedural（程序），各自的存储和检索策略
- 7.4 记忆提取 —— LLM 驱动 vs 关键词 vs 混合，提取时机、频率和去重
- 7.5 Ebbinghaus 遗忘曲线 —— 时效性 + 频率 + 重要性三维评分，记忆的自动衰减与强化
- 7.6 记忆整合（Consolidation）—— Sleep Consolidation、语义聚类、短期→长期晋升流水线
- 7.7 记忆污染与冷启动 —— Upsert 而非 Append、初始画像推断、垃圾记忆清理

### 08 — RAG 检索增强生成（7 节）[P0]
> 如何让 Agent 准确引用外部知识？本章覆盖从经典 RAG 到 Agentic RAG 的完整演进。

- 8.1 经典 RAG 四阶段 —— Index → Retrieve → Augment → Generate，每个阶段的工程挑战
- 8.2 分块策略深度 —— 固定大小 vs 语义分割 vs 递归分块 vs Agentic Chunking 的 recall 曲线与工程取舍（从 3.4 基础概念延伸）
- 8.3 混合检索 —— Dense（向量）+ Sparse（BM25）+ Cross-Encoder Reranker，三合一流水线
- 8.4 Agentic RAG —— 多步推理检索、自我纠错（Error Book）、查询重写、工具调用增强检索
- 8.5 GraphRAG —— 知识图谱 + 向量检索融合，实体关系增强回答的事实一致性
- 8.6 RAG 评估 —— Hit Rate / MRR / NDCG / Faithfulness / 引用溯源准确率
- 8.7 RAG 生产陷阱 —— 检索噪声→反馈循环→相关性漂移，元数据质量衰减导致 Agent 效果崩坏

---

## 第三部分：工具与技能（3 章）

### 09 — Tool / Function Calling（7 节）[P0]
> Agent 的"双手"——如何让模型准确选择、调用和编排工具？本章覆盖从协议到生产的全套方案。

- 9.1 OpenAI Function Call 协议 —— JSON Schema 设计规范、参数 description 对模型行为的影响
- 9.2 工具注册中心 —— 发现、版本管理、权限标注、Schema 兼容性检测
- 9.3 工具执行编排 —— 并发安全判定（isConcurrencySafe）、读工具并行 vs 写工具串行、依赖 DAG 分析
- 9.4 流式工具执行 vs 批量执行 —— 延迟差异（流式可提前启动）、顺序保证、进度消息
- 9.5 海量工具管理 —— 层级工具菜单（Root 5 类 → 按需展开展开子工具），60+ 工具时的选型准确率
- 9.6 工具描述膨胀 —— "114 个工具说 hello 耗 46,000 token"的真实案例分析
- 9.7 工具调用失败三层处理 —— 可重试（指数退避）/ 参数修正（LLM 重新生成）/ 不可恢复降级

### 10 — MCP 协议（4 节）[P0]
> Anthropic 提出的"AI Agent 的 USB-C"——标准化工具接口。2025 年最热的 Agent 面试考点。

- 10.1 设计目标 —— 统一 AI 应用与外部工具/数据源的通信协议，解决"M×N 集成问题"
- 10.2 MCP vs Function Calling —— 通信管道 vs 工具选择的互补关系，什么时候用哪个
- 10.3 Client/Server 模型 —— 工具发现（list_tools）、资源读取（read_resource）、安全沙箱
- 10.4 工程实践 —— 动态发现、缓存策略、多 MCP Server 协作、A2A 协议的竞合关系

### 11 — Skill / 插件系统（4 节）[P1]
> 如何让 Agent 具备可扩展的"专业技能"？本章覆盖 Skill 的定义、加载、注入和发现。

- 11.1 Skill 定义格式 —— SKILL.md 标准（Frontmatter + Body）、when_to_use 触发器
- 11.2 三级加载架构 —— Bundled（内置）→ User（用户）→ Project（项目），优先级与覆盖规则
- 11.3 Skill 注入策略 —— Inline 展开 vs Fork 子 Agent vs Remote 加载，各自的 token 成本
- 11.4 技能发现 —— 关键词匹配 vs AI 分类 vs 用户显式调用，何时自动激活何时等待指令

---

## 第四部分：Multi-Agent 系统（2 章）

### 12 — Multi-Agent 架构与协作（6 节）[P0]
> 一个 Agent 搞不定的时候怎么办？本章覆盖多 Agent 协作的架构模式、通信机制和分歧解决。

- 12.1 Single vs Multi 的决策边界 —— 何时值得付出协调开销？什么时候一个 Agent 就够了？
- 12.2 通信模式 —— 广播 / Hub-Spoke / 点对点 / 层级，各自的延迟和可靠性特征
- 12.3 Orchestrator-Worker 模式 —— 中心协调者分发任务给专业 Agent，结果聚合
- 12.4 Architect-Coder 模式 —— 规划与执行分离：一个 Agent 设计、另一个 Agent 实现
- 12.5 Agent 间上下文传递 —— 共享记忆 vs 消息传递 vs 结构化摘要交接
- 12.6 分歧解决 —— 规则优先→多数投票→Manager 仲裁→人工升级，四层递进

### 13 — 子 Agent 与任务分解（5 节）[P1]
> Fork、串行还是并行？本章覆盖子任务的粒度判定、隔离策略和容错机制。

- 13.1 任务粒度判定 —— 何时 Fork 子 Agent、何时串行、何时并行
- 13.2 子 Agent 的上下文隔离 —— 独立上下文窗口 + 受限工具集 + 权限收窄
- 13.3 Coordinator 模式 —— 任务分发、结果聚合、超时处理、部分失败恢复
- 13.4 进程内 vs 远程 Agent —— 通信开销、安全隔离、故障域的工程取舍
- 13.5 多模型协同路由 —— B 站生产实践：SQL→Claude / 多模态→Gemini / 中文→DeepSeek

---

## 第五部分：输出质量与可靠性（3 章）

### 14 — 降低幻觉（6 节）[P0]
> Agent 最致命的问题：自信地说谎。本章覆盖从护栏到自验证的幻觉防御体系。

- 14.1 幻觉根因 —— 训练数据噪声、概率采样、上下文误导、知识截止
- 14.2 多层护栏（Guardrails）—— 输入过滤→行动计划验证→输出事实核查，三道防线
- 14.3 自验证循环 —— Librarian Check：生成的每步都经验证节点二次确认
- 14.4 引用溯源 —— 强制标注来源段落，Cross-Encoder 验证引用与断言的语义一致性
- 14.5 置信度评分 —— 让模型有能力说"我不知道"——比编造好 100 倍
- 14.6 约束生成降低幻觉的代价 —— 受控解码有时反而降低指令遵循能力（2025 年论文发现）

### 15 — 结构化输出与受控解码（6 节）[P1]
> 如何保证 Agent 输出合法 JSON？为什么 Few-shot 对受控解码有放大效应？

- 15.1 两条路径 —— Prompt-Based（非确定性）vs Constrained Decoding（确定性语法保证）
- 15.2 受控解码框架对比 —— Outlines（FSM 平衡）/ XGrammar（下推自动机 100x 加速）/ LMFE（零样本最低幻觉 8.9%）
- 15.3 指令微调模型的结构化输出退化 —— 受约束后性能反而下降（RANLP 2025 论文）
- 15.4 Few-shot 的放大效应 —— 1-2 个示例对受控解码的提升远大于对非受控的提升
- 15.5 Schema 优化 —— PARSE：让 LLM 自己优化 JSON Schema，提取准确率 +64.7%、错误率 -92%
- 15.6 生产推荐 —— OpenAI Structured Outputs / Amazon Nova / Outlines / XGrammar

### 16 — Agent 设计模式（4 节）[P0]
> 可复用的 Agent 架构积木。本章覆盖业界验证的 15+ 种设计模式。

- 16.1 HuggingFace 六种基础模式 —— Evaluator-Optimizer / Context-Augmentation / Prompt-Chaining / Parallelization / Routing / Orchestrator-Workers
- 16.2 Agent Patterns 九种进阶模式 —— ReAct / Reflection / Plan&Solve / Reflexion / LLM Compiler / REWOO / LATS / Self-Discovery / STORM
- 16.3 12-Factor Agents 方法论 —— 受 12-Factor App 启发：工具即结构化输出、小而专注、拥有你的上下文窗口
- 16.4 Route-then-Compile —— 意图分类后执行确定性路径，避免开放式工具选择的幻觉

---

## 第六部分：安全与容错（2 章）

### 17 — 安全防护（6 节）[P1]
> Agent 拥有了执行代码的能力——如何防止它被注入恶意指令？本章覆盖从输入到输出的纵深防线。

- 17.1 Prompt Injection 四层纵深防御 —— 输入过滤→Prompt 层隔离（边界标记）→工具权限层→输出过滤
- 17.2 工具权限分级 —— Read / Write / Shell / Network / Agent，每级的信任边界
- 17.3 沙箱执行 —— Docker 容器 vs Host 进程 vs 虚拟机，CAP_SYS_ADMIN 与网络隔离
- 17.4 Kill Switch 设计 —— 不能只停执行，要过渡到安全模式 + 补偿未完成的有状态操作
- 17.5 数据脱敏与本地化 —— PII 检测时机、审计日志、企业文化数据不外泄
- 17.6 法规合规 —— EU AI Act 对 Agent 部署的影响、数据本地化要求、模型输出审计追溯、企业级合规清单

### 18 — 可靠性与容错（6 节）[P0]
> "Agent 是概率系统，你怎么在不确定性中做出可靠的工程设计？"——面试必问题。

- 18.1 Agent 的概率本质 —— 每步 5% 失败率 → 20 步累积失败率 64%，概率爆炸的数学
- 18.2 重试策略 —— 指数退避 + 最大重试 + 断路器（Circuit Breaker: CLOSED→OPEN→HALF_OPEN）
- 18.3 多 Provider Fallback —— 链路切换 + 模型降级 + 529 Overloaded 专项处理
- 18.4 静默失败的检测 —— 行为信号监控：重复重规划、工具调用暴增、状态漂移、无显性 error
- 18.5 幂等性设计 —— 可重放的步骤、进度跟踪、从崩溃点恢复而非从头开始
- 18.6 降级策略 —— 置信度低于阈值时：Human-in-the-loop 转人工、回退到规则引擎

---

## 第七部分：可观测性与评估（2 章）

### 19 — 可观测性（5 节）[P0]
> 当 Agent 在后台跑了 50 步后给出一个错误答案——你怎么知道是哪一步出的问题？

- 19.1 完整链路追踪 —— Thought → Action → Observation 每一步的输入/输出/耗时/Token
- 19.2 三维度指标体系 —— Token 消耗（每步/每工作流）/ 延迟 P50 P95 P99 / 成本（按模型/按工作流）
- 19.3 上下文窗口监控 —— 当前用量百分比、压缩触发预警、性能退化检测
- 19.4 工具集成 —— LangFuse / LangSmith / Phoenix / OpenTelemetry 的接入方式和差异
- 19.5 错误回放与根因分析 —— 完整上下文快照、可复现的调试环境

### 20 — Agent 评估体系（6 节）[P0]
> "你的 Agent 好不好？"——用数据回答。本章覆盖四层评估模型、主流基准和实验方法。

- 20.1 四层评估模型 —— 输出质量（准确性/忠实度）→ 行为质量（任务完成率/工具准确率）→ 用户体验（首Token延迟/放弃率）→ 业务指标（转人工率/处理时长）
- 20.2 评估框架 —— WebArena（网站交互）/ OSWorld（OS 操作）/ SWE-Bench（软件工程）/ GAIA（通用助手）
- 20.3 LLM-as-Judge —— 用强模型评估弱模型、评分一致性校准、位置偏差（首尾偏好）
- 20.4 评估→训练闭环 —— 失败案例自动归类→根因诊断→Skill 改进→回归测试→部署
- 20.5 Agent A/B 测试与实验设计 —— 受控实验设计、统计显著性检验、混淆变量控制、渐进式发布策略
- 20.6 评测数据集构建 —— 自建 eval set 的方法论、数据标注质量控制、训练/评估数据隔离防泄露

---

## 第八部分：工程架构与部署（3 章）

### 21 — Agent 框架从零设计（6 节）[P0]
> "从零设计一个 Agent 框架"——系统设计面试最可能出的大题。

- 21.1 架构蓝图 —— 主循环 + 工具编排层 + 记忆层 + 安全层 + 可观测层的模块划分
- 21.2 主循环设计 —— Async Generator 模式、Turn 管理、Stop Hooks（循环检测、最大轮次）
- 21.3 多 Provider 适配层 —— 统一接口抽象、Provider 间差异屏蔽、运行时热切换
- 21.4 会话管理 —— SQLite/Redis/PostgreSQL 的持久化选型、Resume（恢复）机制
- 21.5 流式通信 —— SSE vs WebSocket vs Webhook 的延迟、可靠性、复杂性对比
- 21.6 连接池管理 —— httpx.AsyncClient 跨 Turn 复用、避免每请求新建 TCP 连接

### 22 — 推理优化与成本控制（5 节）[P1]
> Agent 是昂贵的——如何在保持质量的同时控制成本？

- 22.1 推理加速 —— 量化（FP32→INT8→INT4）、Continuous Batching、KV Cache 复用、Speculative Decoding
- 22.2 本地模型部署 —— Ollama / vLLM / llama.cpp / SGLang 的适用场景与性能特征
- 22.3 成本控制策略 —— 模型蒸馏（大模型→小模型）、缓存命中率优化、多模型路由（简单任务用小模型）
- 22.4 延迟优化 —— 首 Token 时间（TTFT）vs 总吞吐、流式响应的感知延迟、预填充缓存
- 22.5 微调 vs 提示词决策框架 —— 何时 Fine-tune 而非优化 Prompt？信号判断（任务确定性/数据量/成本权衡）、LoRA 微调的 ROI 计算

### 23 — 部署与运维（5 节）[P1]
> 从笔记本到生产——Agent 上线需要什么？

- 23.1 Web 框架选型 —— FastAPI + Uvicorn 的异步部署模式
- 23.2 容器化 —— Docker 多阶段构建、健康检查、优雅关闭
- 23.3 数据持久化 —— SQLite（单机）vs PostgreSQL（分布式）、迁移策略
- 23.4 缓存层 —— Redis 用于 Session Cache / Embedding Cache / Rate Limiter
- 23.5 实时通信 —— WebSocket 长连接管理 + SSE 单向流 + 断线重连

---

## 第九部分：生产踩坑与反模式（2 章）

> 来自 Composio、Google ADK、B 站数据 AI 团队、CNCF 等的一线生产经验。

### 24 — 10 个真实生产问题（10 节）[P1]
- 24.1 测试通过、48h 后死循环 —— 可观测性黑洞：日志显示正常，trace 无用，无法复现
- 24.2 Token 爆炸 —— 50 步工作流吃掉 100 万+ token，不是因为任务复杂而是工具元数据膨胀
- 24.3 工具选择错误 —— 100+ 工具全部暴露、名称相似的函数互相干扰、模型选错概率飙升
- 24.4 上下文静默退化与增量污染 —— 不报错但输出完全错误：100K token 处模型性能暴跌 50%+（2025 年论文）；旧上下文被截断后后续决策基于不完整信息
- 24.5 元数据质量衰减 —— RAG 索引随时间腐化、Agent 效果缓慢下降、没有告警机制
- 24.6 概率爆炸 —— 多节点 Agent 工作流中每步的错误累积，6 步后可靠性从 99% 降到 94%
- 24.7 非确定性输出 —— 相同输入不同结果：检索顺序、模型温度、工具输出格式波动
- 24.8 工具调用幻觉 —— 1B-3B 参数小模型产生虚假函数名或错误参数类型
- 24.9 缺少"我已尝试过什么"跟踪 —— Agent 原地打转，重复调用同样的工具期望不同结果
- 24.10 多模型协同路由平衡难 —— 任务-模型匹配策略不当导致成本翻倍或质量下降

### 25 — 五大反模式（5 节）[P0]
- 25.1 "把一切扔进上下文" —— 完整历史 + 全量工具 + 原始检索结果 → Token 灾难
- 25.2 "没有上下文预算" —— 不追踪 Token 消耗就无法优化，无法优化就无法规模化
- 25.3 "隐式状态管理" —— 松散变量替代检查点，步骤 3 失败需要从零重跑
- 25.4 "所有工具始终可见" —— 替代方案：层级工具菜单，Root 5 类 → 按需展开
- 25.5 "不区分压缩和摘要" —— 可逆压缩（内容可恢复）vs 不可逆摘要（永久信息丢失）

---

## 第十部分：前沿方向（2 章）

### 26 — AI Agent 前沿（7 节）[P2]
- 26.1 自我进化 Agent —— Skill 自动优化、Tool 描述自动改进（"描述→评估→改进"闭环）
- 26.2 A2A（Agent-to-Agent）协议 —— Google 提出的跨平台、跨厂商 Agent 通信标准
- 26.3 World Model 预测式执行 —— 先模拟可能结果再执行，减少不可逆操作的代价
- 26.4 Computer Use Agent —— 截图→视觉模型理解→元素定位→操作规划→鼠标键盘执行
- 26.5 形式化验证在 Agent 中的应用 —— 用数学方法验证关键决策路径的正确性
- 26.6 工业界实战 —— B 站 Multi-Agent + MCP 演进（RAG→Agent→Multi-Agent，Text-to-SQL 准确率 90%）
- 26.7 开源生态与社区全景 —— CrewAI / AutoGen / LangGraph / Agno / Dify / Coze / n8n 的社区活跃度、治理模式与商业化路径（技术架构对比见 4.5）

### 27 — 模型前沿（6 节）[P2]
- 27.1 MoE（Mixture of Experts）—— DeepSeek-V3 / Mixtral 的稀疏激活原理与推理成本优势
- 27.2 推理时扩展（Test-time Compute Scaling）—— OpenAI o1/o3 的"思考更久=答案更好"
- 27.3 多模态 Agent —— 视觉 + 代码 + 文档 + 语音的统一理解与行动
- 27.4 Fine-tuning 技术栈 —— LoRA / QLoRA / DPO / RLHF / GRPO，各自的适用场景和资源需求
- 27.5 小模型的 Agent 能力瓶颈 —— 1B-3B 参数模型的工具调用可靠性危机
- 27.6 长上下文的底层瓶颈 —— Attention 精度衰减机制、"Pre-rot threshold"概念、RoPE 位置编码的局限性（工程影响见 5.6）

---

## 附录（4 项）

| 附录 | 内容 | 用途 |
|------|------|------|
| **A — 核心资源索引** | 面试备考资料、必读论文（按章节索引）、关键博客、框架官方文档、评估基准（WebArena/SWE-Bench/GAIA） | 查阅原始资料 |
| **B — 技术栈速查表** | Python / TypeScript 工具链、关键库及版本兼容性矩阵、pip/npm 常用命令 | 快速技术选型 |
| **C — 术语表中英对照** | Agent 工程常用术语、缩写（MCP/A2A/RAG/CoT/RLHF/DPO...）、协议名称 | 阅读文档时查阅 |
| **D — 面试高频 50 题索引** | 每道题标注对应知识库章节、难度等级（★/★★/★★★）、出现频率（高频/中频/低频） | 面试前快速复习 |

---

## 章节统计

| 部分 | 章数 | 节数 | 面试权重 |
|------|------|------|----------|
| 第一部分：Agent 核心原理 | 4 章 | 21 节 | ★★★ |
| 第二部分：上下文工程与记忆 | 4 章 | 25 节 | ★★★★★ |
| 第三部分：工具与技能 | 3 章 | 15 节 | ★★★★ |
| 第四部分：Multi-Agent 系统 | 2 章 | 11 节 | ★★★ |
| 第五部分：输出质量与可靠性 | 3 章 | 16 节 | ★★★★ |
| 第六部分：安全与容错 | 2 章 | 12 节 | ★★★ |
| 第七部分：可观测性与评估 | 2 章 | 11 节 | ★★★ |
| 第八部分：工程架构与部署 | 3 章 | 16 节 | ★★★ |
| 第九部分：生产踩坑与反模式 | 2 章 | 15 节 | ★★ |
| 第十部分：前沿方向 | 2 章 | 13 节 | ★ |
| 附录 | 4 项 | — | — |
| **合计** | **27 章** | **155 节** | — |
