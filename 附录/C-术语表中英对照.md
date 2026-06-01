# 附录 C — 术语表中英对照

> Agent 工程常用术语、缩写、协议名称速查。

---

## 核心概念

| 英文 | 中文 | 解释 |
|------|------|------|
| Agent / AI Agent | 智能体 / AI 智能体 | 能感知环境、进行推理并采取行动的 AI 系统 |
| LLM (Large Language Model) | 大语言模型 | 基于 Transformer 的大规模语言预训练模型 |
| RAG (Retrieval-Augmented Generation) | 检索增强生成 | 结合外部知识检索的文本生成技术 |
| Hallucination | 幻觉 | LLM 生成流畅但事实错误的内容 |
| Prompt | 提示词 | 输入给 LLM 的指令文本 |
| System Prompt | 系统提示词 | 定义 Agent 行为边界的顶层指令 |
| Context Window | 上下文窗口 | LLM 单次推理能处理的最大 token 数 |
| Token | 令牌/词元 | LLM 文本处理的最小语义单元 |
| Tokenization | 分词/词元化 | 将文本转换为 token 序列的过程 |
| Embedding | 嵌入/向量表示 | 文本的稠密向量表示，捕捉语义信息 |

---

## Agent 架构与模式

| 英文 | 中文 | 解释 |
|------|------|------|
| ReAct | 推理-行动循环 | Reasoning + Acting 交替执行的 Agent 模式 |
| CoT (Chain-of-Thought) | 思维链 | 逐步推理的 Prompt 技术 |
| ToT (Tree-of-Thoughts) | 思维树 | 多路径探索的推理模式 |
| Plan-and-Execute | 规划-执行 | 先制定完整计划再逐步执行的模式 |
| Reflexion | 反思模式 | 通过自我反思改进后续行为的 Agent 模式 |
| Orchestrator-Worker | 编排-工作者 | 中心协调者分配任务给专业 Agent 的架构 |
| Multi-Agent System (MAS) | 多智能体系统 | 多个 Agent 协作完成任务的系统 |
| HITL (Human-in-the-Loop) | 人机协作 | 在关键决策点引入人工审核的机制 |
| Guardrails | 护栏 | 对 Agent 行为施加约束和验证的机制 |
| Kill Switch | 紧急停止开关 | 安全终止 Agent 执行并做补偿操作的机制 |

---

## 协议与标准

| 英文 | 中文 | 解释 |
|------|------|------|
| MCP (Model Context Protocol) | 模型上下文协议 | Anthropic 提出、Linux Foundation 治理的 AI-工具通信标准 |
| A2A (Agent-to-Agent) | 智能体间协议 | Google 提出、Linux Foundation 治理的跨 Agent 通信标准 |
| Function Calling / Tool Use | 函数调用 / 工具使用 | LLM 选择和调用外部工具的能力 |
| JSON Schema | JSON 模式 | 描述 JSON 数据结构的规范 |
| Structured Outputs | 结构化输出 | 强制 LLM 输出符合特定格式的技术 |
| SSE (Server-Sent Events) | 服务器推送事件 | 服务端向客户端单向推送数据的协议 |
| OpenTelemetry | 开放遥测 | 分布式系统的可观测性标准 |

---

## 模型技术

| 英文 | 中文 | 解释 |
|------|------|------|
| Transformer | 变换器 | 基于自注意力机制的神经网络架构 |
| Attention | 注意力机制 | 让模型关注输入中不同部分权重的机制 |
| KV Cache | 键值缓存 | 缓存已计算的 Key/Value 以加速自回归生成 |
| MoE (Mixture of Experts) | 混合专家 | 每次推理仅激活部分参数的模型架构 |
| Fine-tuning | 微调 | 在预训练模型基础上用特定数据继续训练 |
| LoRA (Low-Rank Adaptation) | 低秩适配 | 高效的参数微调方法 |
| QLoRA | 量化低秩适配 | 结合量化的 LoRA，进一步降低显存需求 |
| RLHF (RL from Human Feedback) | 人类反馈强化学习 | 用人类偏好数据训练奖励模型的对齐方法 |
| DPO (Direct Preference Optimization) | 直接偏好优化 | 无需奖励模型的偏好对齐方法 |
| GRPO (Group Relative Policy Optimization) | 组相对策略优化 | DeepSeek-R1 使用的 RL 训练方法 |
| Speculative Decoding | 推测解码 | 用小模型快速生成候选，大模型验证的加速方法 |
| Continuous Batching | 连续批处理 | 动态组批提高推理吞吐的技术 |
| Quantization | 量化 | 降低模型参数精度以减少显存和加速推理 |
| RoPE (Rotary Position Embedding) | 旋转位置编码 | 通过旋转变换编码位置信息的方法 |

---

## RAG & 检索

| 英文 | 中文 | 解释 |
|------|------|------|
| ANN (Approximate Nearest Neighbor) | 近似最近邻 | 在高维向量空间中快速找到近似最近邻的算法 |
| HNSW (Hierarchical Navigable Small World) | 层级可导航小世界 | 一种高效的 ANN 索引算法 |
| BM25 | BM25 算法 | 基于词频的经典稀疏检索算法 |
| Cross-Encoder | 交叉编码器 | 联合编码两个文本后分类的模型，适合精排 |
| Bi-Encoder | 双编码器 | 分别编码后计算相似度的模型，适合粗排 |
| Reranker | 重排序器 | 对初步检索结果进行精细排序的模型 |
| GraphRAG | 图检索增强生成 | 融合知识图谱的 RAG 方法 |
| Agentic RAG | 智能体 RAG | 由 Agent 自主决策检索策略的 RAG 范式 |
| Chunking | 分块 | 将长文本切分为检索单元的策略 |
| Hit Rate | 命中率 | 检索结果中包含相关文档的比例 |
| MRR (Mean Reciprocal Rank) | 平均倒数排名 | 第一个相关文档排名的倒数平均值 |
| NDCG (Normalized Discounted Cumulative Gain) | 归一化折损累计增益 | 考虑排序位置权重的检索质量指标 |

---

## 安全

| 英文 | 中文 | 解释 |
|------|------|------|
| Prompt Injection | 提示词注入 | 通过恶意输入覆盖或绕过系统指令的攻击 |
| Jailbreak | 越狱 | 绕过模型安全限制的攻击技术 |
| PII (Personally Identifiable Information) | 个人身份信息 | 需要保护的隐私数据 |
| Sandbox | 沙箱 | 隔离执行环境，限制 Agent 的系统访问权限 |
| Circuit Breaker | 断路器 | 故障隔离模式，防止级联失败 |
| RCE (Remote Code Execution) | 远程代码执行 | 通过漏洞在目标系统执行任意代码 |

---

## 评估指标

| 英文 | 中文 | 解释 |
|------|------|------|
| SWE-Bench | 软件工程基准 | 评估 Agent 解决真实 GitHub Issue 的能力 |
| GAIA | 通用 AI 助手基准 | 评估 AI 助手的通用问题解决能力 |
| OSWorld | 操作系统基准 | 评估 Agent 操作真实 OS 环境的能力 |
| TTFT (Time To First Token) | 首 Token 延迟 | 从请求发送到第一个 token 返回的时间 |
| Faithfulness | 忠实度 | 生成内容与源材料的一致程度 |
| LLM-as-Judge | LLM 作评委 | 用强模型评估弱模型输出的方法 |

---

*另见：[附录 A — 核心资源索引](./A-核心资源索引.md) | [附录 B — 技术栈速查表](./B-技术栈速查表.md) | [附录 D — 面试高频 50 题索引](./D-面试高频50题索引.md)*
