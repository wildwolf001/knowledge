# 附录 B — 技术栈速查表

> 2026 年 Agent 工程常用技术栈与版本兼容性矩阵。

---

## 一、Python 工具链

| 类别 | 推荐库 | 版本 | 用途 |
|------|--------|------|------|
| **Agent 框架** | LangGraph | 1.1.x | 有状态图编排 |
| | CrewAI | 1.14.x | 角色驱动多 Agent |
| | Microsoft Agent Framework | latest | AutoGen 继任者 |
| | Agno | latest | 轻量高性能 Agent |
| **LLM 客户端** | openai | 2.x | OpenAI/兼容 API |
| | anthropic | 0.50+ | Anthropic Claude API |
| | google-genai | 1.x | Google Gemini API |
| **HTTP 框架** | FastAPI | 0.115+ | 异步 Web API |
| | httpx | 0.28+ | 异步 HTTP 客户端 |
| | uvicorn | 0.34+ | ASGI 服务器 |
| **数据验证** | Pydantic | 2.10+ | 数据模型与验证 |
| **向量数据库** | chromadb | 0.6.x | 轻量级向量存储 |
| | qdrant-client | 1.13+ | 高性能向量检索 |
| | pymilvus | 2.5+ | 分布式向量数据库 |
| **嵌入模型** | sentence-transformers | 3.x | 开源 Embedding |
| | openai (text-embedding-3) | — | OpenAI Embedding API |
| **检索** | rank-bm25 | 0.2 | BM25 稀疏检索 |
| | FlagEmbedding | 1.3+ | BGE Reranker |
| **MCP** | mcp | 1.x | MCP SDK (Python) |
| **可观测性** | opentelemetry-api | 1.29+ | 分布式追踪 |
| | langfuse | 2.x | LLM 可观测性 |
| **缓存** | redis | 5.x | Redis 客户端 |
| **数据库** | sqlalchemy | 2.x | ORM |
| | asyncpg | 0.30+ | PostgreSQL 异步驱动 |
| | aiosqlite | 0.20+ | SQLite 异步驱动 |
| **容器化** | Docker | 27+ | 容器运行时 |
| **测试** | pytest | 8.x | 测试框架 |
| | pytest-asyncio | 0.25+ | 异步测试 |

---

## 二、TypeScript / Node.js 工具链

| 类别 | 推荐库 | 版本 | 用途 |
|------|--------|------|------|
| **Agent 框架** | Mastra | latest | TypeScript 原生 Agent |
| | LangGraph.js | 0.3.x | 图编排 (JS) |
| **MCP** | @modelcontextprotocol/sdk | 1.x | MCP SDK (TypeScript) |
| **LLM 客户端** | @anthropic-ai/sdk | 0.50+ | Anthropic Claude |
| | openai | 5.x | OpenAI SDK |
| | ai (Vercel) | 4.x | 统一 LLM 接口 |
| **运行环境** | Node.js | 22 LTS | JavaScript 运行时 |
| | Bun | 1.2+ | 高性能 JS 运行时 |
| **Web 框架** | Hono | 4.x | 轻量 Web 框架 |
| **验证** | Zod | 3.24+ | Schema 验证 |

---

## 三、基础设施

| 类别 | 推荐工具 | 说明 |
|------|----------|------|
| **容器编排** | Kubernetes 1.32+ | 生产集群管理 |
| **CI/CD** | GitHub Actions | 自动化流水线 |
| **监控** | Grafana 11.x + Prometheus | 指标可视化 |
| **日志** | OpenTelemetry Collector | 统一日志/Trace |
| **LLM 网关** | LiteLLM / Portkey | 多 Provider 统一代理 |
| **沙箱** | Docker + gVisor | Agent 代码执行隔离 |

---

## 四、pip 常用命令

```bash
# Agent 核心
pip install langgraph langchain-core crewai
pip install openai anthropic google-genai
pip install fastapi uvicorn httpx

# 数据 & 检索
pip install chromadb qdrant-client sentence-transformers
pip install rank-bm25 redis sqlalchemy

# MCP & 可观测性
pip install mcp opentelemetry-api langfuse

# 开发工具
pip install pytest pytest-asyncio ruff mypy
```

## 五、npm 常用命令

```bash
# Agent
npm install @anthropic-ai/sdk openai ai
npm install @modelcontextprotocol/sdk

# Web
npm install hono zod

# Mastra
npm install @mastra/core @mastra/mcp
```
