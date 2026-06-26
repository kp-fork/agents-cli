# Agent Templates

`agents-cli` creates projects from agent templates. Each template provides a working agent with the right dependencies, tools, and project structure for its use case.

---

## Available Templates

| Template | Description | Use Case |
|----------|-------------|----------|
| `adk` | ReAct agent using ADK | General-purpose conversational agent with tool use |
| `agentic_rag` | ADK agent with RAG pipeline | Document Q&A with automated data ingestion |

### adk

The default template. Creates a ReAct agent using the [Agent Development Kit](https://google.github.io/adk-docs/) with a sample tool. Start here if you are new to ADK or building a general-purpose agent.

```bash
agents-cli create my-agent --agent adk
```

Every Python ADK agent serves the [Agent-to-Agent (A2A) protocol](https://a2a-protocol.org) out of the box — the A2A routes (agent card + JSON-RPC) are mounted automatically. Use this when your agent needs to interoperate with agents built on other frameworks (LangGraph, CrewAI, etc.) or when building a distributed multi-agent system; no separate template or hand-written A2A code is required.

### agentic_rag

A document Q&A agent with a built-in RAG (Retrieval-Augmented Generation) pipeline. Includes data ingestion infrastructure for indexing documents into a vector store and retrieving them at query time.

```bash
agents-cli create my-agent --agent agentic_rag --datastore agent_platform_search
```

During project creation, choose a datastore backend:

| Datastore | Description |
|-----------|-------------|
| `agent_platform_search` | GCS Data Connector with built-in scheduling and ranking |
| `agent_platform_vector_search` | Kubeflow pipeline with auto-embedding |

After creation, provision the datastore and ingest data:

```bash
agents-cli infra datastore
agents-cli data-ingestion
```
