<div align="center">

# 🛠️ Tools & Frameworks for Context Engineering

*Comprehensive comparison of tools for building context-aware LLM systems*

[Back to Main Guide](../README.md)

</div>

---

## Table of Contents

- [Orchestration Frameworks](#orchestration-frameworks)
- [Vector Databases](#vector-databases)
- [Embedding Models](#embedding-models)
- [Context Management & Memory](#context-management--memory)
- [Evaluation Tools](#evaluation-tools)
- [Prompt Optimization](#prompt-optimization)
- [Deployment & Serving](#deployment--serving)
- [Selection Guide](#selection-guide)

---

## Orchestration Frameworks

These frameworks provide the scaffolding for building LLM applications with retrieval, memory, and tool use.

### LangChain

- **Link:** [github.com/langchain-ai/langchain](https://github.com/langchain-ai/langchain)
- **Language:** Python, JavaScript/TypeScript
- **Stars:** 98k+
- **License:** MIT
- **Level:** 🟡

| Aspect | Details |
|:-------|:--------|
| **Best For** | Full-featured LLM application development |
| **RAG Support** | Comprehensive: document loaders, text splitters, vector stores, retrievers |
| **Memory** | Multiple memory types: buffer, summary, entity, conversation |
| **Agent Support** | ReAct, OpenAI functions, structured chat, plan-and-execute |
| **Integrations** | 750+ integrations with LLMs, vector stores, tools |
| **Production** | LangSmith for monitoring, LangServe for deployment |

**When to Use:** You need a batteries-included framework with the widest ecosystem. Good default choice for most projects.

**When to Avoid:** You need maximum control over the pipeline or are building something highly custom. The abstraction overhead may be unnecessary for simple use cases.

---

### LlamaIndex

- **Link:** [github.com/run-llama/llama_index](https://github.com/run-llama/llama_index)
- **Language:** Python
- **Stars:** 37k+
- **License:** MIT
- **Level:** 🟡

| Aspect | Details |
|:-------|:--------|
| **Best For** | Data-centric LLM applications, complex RAG |
| **RAG Support** | Advanced: multi-index, recursive, tree-structured, knowledge graphs |
| **Memory** | Chat memory with configurable strategies |
| **Agent Support** | ReAct agents, structured planning, multi-agent |
| **Integrations** | 300+ data source connectors via LlamaHub |
| **Production** | LlamaCloud for managed RAG, LlamaTrace for observability |

**When to Use:** Your primary challenge is connecting to and reasoning over complex data. Best for advanced RAG architectures.

**When to Avoid:** You need a general-purpose agent framework beyond data Q&A.

---

### DSPy

- **Link:** [github.com/stanfordnlp/dspy](https://github.com/stanfordnlp/dspy)
- **Language:** Python
- **Stars:** 19k+
- **License:** MIT
- **Level:** 🔴

| Aspect | Details |
|:-------|:--------|
| **Best For** | Programmatic prompt optimization, research |
| **RAG Support** | Built-in retrieval modules with automatic optimization |
| **Memory** | Managed through module composition |
| **Agent Support** | Through program composition and assertions |
| **Key Feature** | Compiles declarative programs into optimized prompts |
| **Philosophy** | Programming, not prompting |

**When to Use:** You want to systematically optimize your entire LLM pipeline rather than hand-tuning prompts. Best for researchers and advanced practitioners.

**When to Avoid:** You need quick prototyping or are new to LLM development.

---

### Haystack

- **Link:** [github.com/deepset-ai/haystack](https://github.com/deepset-ai/haystack)
- **Language:** Python
- **Stars:** 17k+
- **License:** Apache 2.0
- **Level:** 🟡

| Aspect | Details |
|:-------|:--------|
| **Best For** | Production NLP/RAG pipelines |
| **RAG Support** | Pipeline-based: composable components for retrieval and generation |
| **Memory** | Conversation memory with customizable stores |
| **Agent Support** | Tool-using agents with pipeline integration |
| **Key Feature** | Clean pipeline abstraction, strongly typed |
| **Production** | deepset Cloud for managed deployment |

**When to Use:** You want clean, well-tested pipeline abstractions with strong typing. Good for teams that value software engineering practices.

**When to Avoid:** You need the widest ecosystem of integrations (LangChain wins here).

---

### Semantic Kernel

- **Link:** [github.com/microsoft/semantic-kernel](https://github.com/microsoft/semantic-kernel)
- **Language:** C#, Python, Java
- **Stars:** 22k+
- **License:** MIT
- **Level:** 🟡

| Aspect | Details |
|:-------|:--------|
| **Best For** | Enterprise .NET/Java applications with LLM features |
| **RAG Support** | Memory connectors with vector search |
| **Memory** | Built-in semantic memory with multiple backends |
| **Agent Support** | Planner-based agents with automatic function calling |
| **Key Feature** | First-class C#/Java support, Azure integration |
| **Production** | Deep Azure OpenAI integration |

**When to Use:** Your stack is .NET or Java, or you are deeply invested in the Microsoft/Azure ecosystem.

**When to Avoid:** You are Python-first or need the broadest community support.

---

### CrewAI

- **Link:** [github.com/joaomdmoura/crewAI](https://github.com/joaomdmoura/crewAI)
- **Language:** Python
- **Stars:** 24k+
- **License:** MIT
- **Level:** 🟡

| Aspect | Details |
|:-------|:--------|
| **Best For** | Multi-agent systems with role-based design |
| **RAG Support** | Through tool integration |
| **Memory** | Shared and agent-specific memory |
| **Agent Support** | Role-based agents with delegation and collaboration |
| **Key Feature** | Intuitive role/goal/backstory agent definition |
| **Production** | CrewAI+ for enterprise features |

**When to Use:** You are building multi-agent systems where agents have distinct roles and need to collaborate.

**When to Avoid:** You need fine-grained control over the agent loop, or your use case is single-agent.

---

### AutoGen

- **Link:** [github.com/microsoft/autogen](https://github.com/microsoft/autogen)
- **Language:** Python
- **Stars:** 35k+
- **License:** MIT
- **Level:** 🔴

| Aspect | Details |
|:-------|:--------|
| **Best For** | Multi-agent conversation and complex workflows |
| **RAG Support** | Through retrieval-augmented agents |
| **Memory** | Conversation-based, configurable |
| **Agent Support** | Flexible multi-agent conversation patterns |
| **Key Feature** | Human-in-the-loop, code execution, group chat |
| **Production** | AutoGen Studio for visual agent building |

**When to Use:** You need complex multi-agent conversations with human oversight and code execution capabilities.

**When to Avoid:** Simple single-agent tasks or straightforward RAG.

---

## Framework Comparison Matrix

| Feature | LangChain | LlamaIndex | DSPy | Haystack | Semantic Kernel | CrewAI | AutoGen |
|:--------|:---------:|:----------:|:----:|:--------:|:--------------:|:------:|:-------:|
| RAG Quality | A | A+ | A | A | B+ | B | B |
| Agent Support | A | B+ | B | B+ | A | A+ | A+ |
| Ease of Use | B+ | B+ | C+ | A | B | A | B |
| Production Ready | A | A | B | A | A | B+ | B+ |
| Ecosystem Size | A+ | A | B | B+ | B+ | B | B+ |
| Multi-Agent | B | B | C | B | B | A+ | A+ |
| Context Optimization | B | A | A+ | B | B | B | B |
| Learning Curve | Medium | Medium | Steep | Low | Medium | Low | High |

---

## Vector Databases

### Comparison Table

| Database | Type | Hosted | OSS | Max Vectors | Key Feature | Best For |
|:---------|:----:|:------:|:---:|:-----------:|:-----------|:---------|
| **Pinecone** | Cloud | Yes | No | Billions | Fully managed, enterprise SLA | Production, zero-ops |
| **Weaviate** | Hybrid | Yes | Yes | Billions | GraphQL, hybrid search, modules | Multimodal search |
| **Chroma** | Embedded | Yes | Yes | Millions | Lightweight, developer-friendly | Prototyping, small-scale |
| **Milvus** | Distributed | Yes | Yes | Trillions | GPU acceleration, partitioning | Large-scale production |
| **Qdrant** | Hybrid | Yes | Yes | Billions | Rust, filtering, payload search | Filtered similarity search |
| **pgvector** | Extension | No | Yes | Millions | PostgreSQL integration | Existing Postgres users |
| **FAISS** | Library | No | Yes | Billions | Speed, GPU support | Research, batch processing |
| **Vespa** | Hybrid | Yes | Yes | Billions | Hybrid search, ML ranking | Enterprise search |
| **LanceDB** | Embedded | No | Yes | Millions | Columnar, multimodal | Embedded applications |

### Detailed Profiles

#### Pinecone

- **Link:** [pinecone.io](https://www.pinecone.io/)
- **Pricing:** Free tier (1 index), paid from $70/month
- **Best For:** Teams that want zero operational overhead

**Strengths:** Fully managed, excellent documentation, fast setup, enterprise features (SSO, audit logs).

**Limitations:** Vendor lock-in, no self-hosted option, can be expensive at scale.

---

#### Weaviate

- **Link:** [weaviate.io](https://weaviate.io/)
- **Pricing:** Open source self-hosted, cloud from $25/month
- **Best For:** Projects needing hybrid search (vector + keyword) with rich querying

**Strengths:** GraphQL API, built-in vectorization modules, multi-tenancy, hybrid search.

**Limitations:** Higher resource requirements, steeper learning curve than Chroma.

---

#### Chroma

- **Link:** [trychroma.com](https://www.trychroma.com/)
- **Pricing:** Open source (free), cloud in development
- **Best For:** Rapid prototyping, local development, small to medium scale

**Strengths:** Simplest API, runs in-process or client-server, Python/JS native.

**Limitations:** Not designed for billion-scale, limited filtering compared to alternatives.

---

#### Qdrant

- **Link:** [qdrant.tech](https://qdrant.tech/)
- **Pricing:** Open source self-hosted, cloud from $25/month
- **Best For:** Applications requiring complex filtering alongside similarity search

**Strengths:** Rust performance, payload-based filtering, quantization support, rich query API.

**Limitations:** Smaller community than Pinecone/Weaviate.

---

## Embedding Models

### Comparison Table

| Model | Provider | Dims | Max Tokens | MTEB Score | Open Source | Cost |
|:------|:--------:|:----:|:----------:|:----------:|:-----------:|:----:|
| text-embedding-3-large | OpenAI | 3072 | 8191 | 64.6 | No | $0.13/1M |
| text-embedding-3-small | OpenAI | 1536 | 8191 | 62.3 | No | $0.02/1M |
| embed-v4 | Cohere | 1024 | 512 | 66.3 | No | $0.10/1M |
| voyage-3 | Voyage AI | 1024 | 32000 | 67.3 | No | $0.06/1M |
| BGE-M3 | BAAI | 1024 | 8192 | 66.1 | Yes | Free |
| GTE-Qwen2-7B | Alibaba | 1536 | 32000 | 70.2 | Yes | Free |
| NomicEmbed-v1.5 | Nomic | 768 | 8192 | 62.8 | Yes | Free |
| E5-Mistral-7B | Microsoft | 4096 | 32000 | 66.6 | Yes | Free |
| Jina-embeddings-v3 | Jina AI | 1024 | 8192 | 65.5 | Yes | Free |

### Selection Guide

```
Do you need multilingual support?
├── Yes ──> BGE-M3 (open) or Cohere embed-v4 (API)
└── No
    ├── Budget constrained?
    │   ├── Yes ──> NomicEmbed (open, free)
    │   └── No
    │       ├── Need long-context embeddings (>8K)?
    │       │   ├── Yes ──> voyage-3 or GTE-Qwen2 (32K context)
    │       │   └── No ──> text-embedding-3-large (OpenAI)
    │       └── Maximum quality?
    │           └── GTE-Qwen2-7B (open) or voyage-3 (API)
    └── Self-hosted required?
        └── Yes ──> BGE-M3 or GTE-Qwen2
```

---

## Context Management & Memory

| Tool | Purpose | Key Feature | Link |
|:-----|:--------|:-----------|:-----|
| **MemGPT / Letta** | Virtual context management | Self-editing memory, OS-inspired hierarchy | [github.com/cpacker/MemGPT](https://github.com/cpacker/MemGPT) |
| **Mem0** | Personalized AI memory | User-specific persistent memory layer | [github.com/mem0ai/mem0](https://github.com/mem0ai/mem0) |
| **LangMem** | Long-term memory for LangChain | Persistent conversational memory | [github.com/langchain-ai/langmem](https://github.com/langchain-ai/langmem) |
| **Instructor** | Structured output extraction | Pydantic-based, retry logic | [github.com/jxnl/instructor](https://github.com/jxnl/instructor) |
| **Guardrails AI** | Output validation | Structure, type, quality checks | [github.com/guardrails-ai/guardrails](https://github.com/guardrails-ai/guardrails) |
| **Outlines** | Structured generation | Grammar-constrained decoding | [github.com/outlines-dev/outlines](https://github.com/outlines-dev/outlines) |
| **Guidance** | Constrained generation | Template-based control flow | [github.com/guidance-ai/guidance](https://github.com/guidance-ai/guidance) |

---

## Evaluation Tools

| Tool | Focus | Key Feature | Link |
|:-----|:------|:-----------|:-----|
| **RAGAS** | RAG evaluation | Faithfulness, relevance, context metrics | [github.com/explodinggradients/ragas](https://github.com/explodinggradients/ragas) |
| **DeepEval** | LLM evaluation | 14+ metrics, CI/CD integration | [github.com/confident-ai/deepeval](https://github.com/confident-ai/deepeval) |
| **LangSmith** | LLM observability | Tracing, evaluation, monitoring | [smith.langchain.com](https://smith.langchain.com/) |
| **Phoenix (Arize)** | LLM observability | Traces, evals, embeddings viz | [github.com/Arize-ai/phoenix](https://github.com/Arize-ai/phoenix) |
| **Promptfoo** | Prompt testing | CLI-based, CI/CD, red teaming | [github.com/promptfoo/promptfoo](https://github.com/promptfoo/promptfoo) |
| **Braintrust** | LLM evaluation | Logging, scoring, experiments | [braintrust.dev](https://www.braintrust.dev/) |
| **TruLens** | RAG evaluation | Feedback functions, groundedness | [github.com/truera/trulens](https://github.com/truera/trulens) |

---

## Prompt Optimization

| Tool | Approach | Key Feature | Link |
|:-----|:---------|:-----------|:-----|
| **DSPy** | Compilation | Automatic prompt optimization | [github.com/stanfordnlp/dspy](https://github.com/stanfordnlp/dspy) |
| **TextGrad** | Gradient descent | Natural language gradients | [github.com/zou-group/textgrad](https://github.com/zou-group/textgrad) |
| **OPRO** | LLM optimization | Uses LLMs to optimize prompts | [arxiv.org/abs/2309.03409](https://arxiv.org/abs/2309.03409) |
| **PromptBench** | Benchmarking | Robustness evaluation for prompts | [github.com/microsoft/promptbench](https://github.com/microsoft/promptbench) |

---

## Deployment & Serving

| Tool | Purpose | Key Feature | Link |
|:-----|:--------|:-----------|:-----|
| **vLLM** | LLM serving | PagedAttention, high throughput | [github.com/vllm-project/vllm](https://github.com/vllm-project/vllm) |
| **TGI** | LLM serving | Hugging Face optimized serving | [github.com/huggingface/text-generation-inference](https://github.com/huggingface/text-generation-inference) |
| **Ollama** | Local LLM running | Simple CLI, model management | [github.com/ollama/ollama](https://github.com/ollama/ollama) |
| **LiteLLM** | LLM proxy | Unified API across 100+ providers | [github.com/BerriAI/litellm](https://github.com/BerriAI/litellm) |
| **LangServe** | LLM app serving | REST API from LangChain chains | [github.com/langchain-ai/langserve](https://github.com/langchain-ai/langserve) |

---

## Selection Guide

### "I'm building a simple RAG chatbot"

**Recommended Stack:**
- Framework: LangChain or LlamaIndex
- Vector DB: Chroma (development), Pinecone or Qdrant (production)
- Embeddings: text-embedding-3-small (OpenAI)
- Evaluation: RAGAS

### "I'm building a multi-agent system"

**Recommended Stack:**
- Framework: CrewAI or AutoGen
- Memory: Mem0 or MemGPT
- Vector DB: Qdrant or Weaviate
- Evaluation: LangSmith

### "I want maximum RAG quality"

**Recommended Stack:**
- Framework: LlamaIndex (advanced RAG patterns)
- Vector DB: Weaviate (hybrid search) or Qdrant
- Embeddings: voyage-3 or GTE-Qwen2
- Reranking: Cohere Rerank or ColBERT
- Evaluation: RAGAS + DeepEval

### "I need to optimize prompts systematically"

**Recommended Stack:**
- Framework: DSPy
- Evaluation: Promptfoo + custom metrics
- Monitoring: LangSmith or Phoenix

### "I'm on a tight budget / want open source only"

**Recommended Stack:**
- Framework: LlamaIndex or Haystack
- Vector DB: Chroma or pgvector
- Embeddings: BGE-M3 or NomicEmbed
- LLM Serving: Ollama + vLLM
- Evaluation: RAGAS (open source)

---

<div align="center">

**[Back to Main Guide](../README.md)**

</div>
