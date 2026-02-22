<div align="center">

# 🧠 Context Engineering — The Complete Guide

### Everything you need to know about Context Windows, Prompt Engineering, and Building Better AI Systems

[![GitHub stars](https://img.shields.io/github/stars/mlnjsh/context-engineering?style=for-the-badge&logo=github&color=yellow)](https://github.com/mlnjsh/context-engineering/stargazers)
[![GitHub forks](https://img.shields.io/github/forks/mlnjsh/context-engineering?style=for-the-badge&logo=github&color=blue)](https://github.com/mlnjsh/context-engineering/network)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg?style=for-the-badge)](https://opensource.org/licenses/MIT)
[![Last Updated](https://img.shields.io/badge/Last%20Updated-February%202026-purple?style=for-the-badge)]()
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=for-the-badge)](http://makeapullrequest.com)
[![Awesome](https://img.shields.io/badge/Awesome-Context%20Engineering-FC60A8?style=for-the-badge&logo=awesomelists&logoColor=white)]()

---

**Maintained by [Professor Milan Amrut Joshi](https://github.com/mlnjsh)**
*Professor of Data Science, Northwestern University*

*A curated, research-backed guide to the emerging discipline of Context Engineering for Large Language Models.*

[Papers](#-research-papers) · [Videos](#-youtube-videos--talks) · [Blog Posts](#-blog-posts--articles) · [Tools](#%EF%B8%8F-tools--frameworks) · [Techniques](#-techniques--patterns) · [Courses](#-courses--tutorials) · [Roadmap](#%EF%B8%8F-roadmap)

---

</div>

## Table of Contents

- [What is Context Engineering?](#what-is-context-engineering)
- [Context Engineering vs Prompt Engineering](#context-engineering-vs-prompt-engineering)
- [Why It Matters (2025-2026)](#why-it-matters-in-2025-2026)
- [Key Concepts](#key-concepts)
- [Context Window Sizes](#-context-window-sizes)
- [Research Papers](#-research-papers)
- [YouTube Videos & Talks](#-youtube-videos--talks)
- [Blog Posts & Articles](#-blog-posts--articles)
- [Tools & Frameworks](#%EF%B8%8F-tools--frameworks)
- [Courses & Tutorials](#-courses--tutorials)
- [Techniques & Patterns](#-techniques--patterns)
- [Roadmap](#%EF%B8%8F-roadmap)
- [Contributing](#contributing)
- [Citation](#citation)

---

## What is Context Engineering?

> **Context Engineering** is the art and science of designing, managing, and optimizing the information provided to Large Language Models (LLMs) within their context window to maximize the quality, accuracy, and relevance of their outputs.

While **prompt engineering** focuses on *how you ask*, **context engineering** focuses on *what information surrounds your ask* — the retrieval strategy, the memory architecture, the token budget allocation, the ordering of information, and the system-level design of context pipelines.

```
┌─────────────────────────────────────────────────────────────┐
│                      CONTEXT WINDOW                         │
│                                                             │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────────┐  │
│  │   SYSTEM     │  │  RETRIEVED   │  │   CONVERSATION   │  │
│  │   PROMPT     │  │  DOCUMENTS   │  │   HISTORY        │  │
│  │              │  │  (RAG)       │  │                  │  │
│  │  - Role      │  │  - Chunks    │  │  - Past turns    │  │
│  │  - Rules     │  │  - Metadata  │  │  - Summaries     │  │
│  │  - Examples  │  │  - Rankings  │  │  - Key facts     │  │
│  └──────────────┘  └──────────────┘  └──────────────────┘  │
│                                                             │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────────┐  │
│  │   TOOLS &    │  │  FEW-SHOT    │  │   USER           │  │
│  │   SCHEMAS    │  │  EXAMPLES    │  │   QUERY          │  │
│  │              │  │              │  │                  │  │
│  │  - Functions │  │  - Input/    │  │  - Current       │  │
│  │  - APIs      │  │    Output    │  │    request       │  │
│  │  - Formats   │  │    pairs     │  │  - Constraints   │  │
│  └──────────────┘  └──────────────┘  └──────────────────┘  │
│                                                             │
│           ▼ Token Budget Management ▼                       │
│           ▼ Information Ordering    ▼                       │
│           ▼ Relevance Filtering     ▼                       │
└─────────────────────────────────────────────────────────────┘
```

---

## Context Engineering vs Prompt Engineering

| Dimension | Prompt Engineering | Context Engineering |
|-----------|-------------------|-------------------|
| **Focus** | Crafting the query/instruction | Designing the entire information environment |
| **Scope** | Single prompt | Full context pipeline (retrieval, memory, tools) |
| **Abstraction** | Text-level | System-level architecture |
| **Key Question** | "How do I phrase this?" | "What information does the model need, and how should it be structured?" |
| **Includes** | Instructions, few-shot examples | RAG, memory, tool definitions, token budgets, ordering |
| **Skill Level** | 🟢 Beginner to Intermediate | 🟡 Intermediate to Advanced |
| **Optimization** | Wording, formatting, chain-of-thought | Retrieval quality, chunking, compression, caching |
| **Analogies** | Writing a good exam question | Designing the entire exam prep system |
| **Dynamic?** | Mostly static templates | Dynamic, adapts per query and session |
| **Measurable Impact** | Quality of single response | System-level accuracy, cost, latency |

---

## Why It Matters in 2025-2026

1. **Context windows are exploding** — From 4K tokens (GPT-3) to 2M+ tokens (Gemini). Managing this space effectively is a core engineering challenge.
2. **RAG is now standard** — Every production LLM application uses some form of retrieval. Context engineering defines how retrieved data is structured and ranked.
3. **Agentic AI demands it** — AI agents that use tools, maintain memory, and plan across steps require sophisticated context management.
4. **Cost optimization** — Tokens cost money. Smart context engineering reduces costs by 50-90% while maintaining quality.
5. **Accuracy at scale** — The "lost in the middle" problem and context dilution mean that *more* context is not always *better*. Engineering is required.

---

## Key Concepts

<details>
<summary><strong>🔑 Context Window</strong></summary>

The fixed-size buffer of tokens an LLM can process in a single forward pass. Everything the model "knows" at inference time must fit within this window: system prompt, retrieved documents, conversation history, tool schemas, and the user query.

</details>

<details>
<summary><strong>🔑 Token Limits & Budget Allocation</strong></summary>

Given a finite context window, context engineering involves deciding how many tokens to allocate to each component. A common allocation:
- System prompt: 5-10%
- Retrieved documents: 40-60%
- Conversation history: 15-25%
- Few-shot examples: 5-10%
- User query + response buffer: 10-20%

</details>

<details>
<summary><strong>🔑 Retrieval-Augmented Generation (RAG)</strong></summary>

The pattern of retrieving relevant documents from an external knowledge base and injecting them into the context window. RAG bridges the gap between parametric knowledge (model weights) and non-parametric knowledge (external data).

</details>

<details>
<summary><strong>🔑 Memory Management</strong></summary>

Strategies for maintaining information across sessions or long conversations: summarization, key-fact extraction, vector-based episodic memory, and hierarchical memory architectures (short-term, long-term, working memory).

</details>

<details>
<summary><strong>🔑 Context Compression</strong></summary>

Techniques to reduce token usage while preserving information: extractive summarization, LLMLingua-style token pruning, semantic deduplication, and information-theoretic compression.

</details>

<details>
<summary><strong>🔑 Information Ordering</strong></summary>

The position of information within the context window affects recall. Models exhibit primacy and recency biases. Context engineering accounts for this by placing critical information at the beginning and end of the context.

</details>

---

## 📋 Context Window Sizes

| Model | Context Window | Provider | Year | Notes |
|:------|:-------------:|:--------:|:----:|:------|
| GPT-4o | 128K tokens | OpenAI | 2024 | Multimodal, widely deployed |
| GPT-o3 | 200K tokens | OpenAI | 2025 | Reasoning model, extended context |
| Claude 3.5 Sonnet | 200K tokens | Anthropic | 2024 | Strong long-context performance |
| Claude Opus 4 | 200K tokens | Anthropic | 2025 | Frontier model |
| Claude Sonnet 4 | 200K tokens | Anthropic | 2025 | Balanced performance and speed |
| Gemini 2.0 Flash | 1M tokens | Google | 2025 | Fast, extended context |
| Gemini 2.0 Pro | 2M tokens | Google | 2025 | Largest production context window |
| Llama 3.1 405B | 128K tokens | Meta | 2024 | Open-weight |
| Llama 4 Maverick | 1M tokens | Meta | 2025 | Open-weight, MoE architecture |
| Mistral Large 2 | 128K tokens | Mistral | 2024 | European AI lab |
| DeepSeek V3 | 128K tokens | DeepSeek | 2025 | MoE, cost-efficient |
| DeepSeek R1 | 128K tokens | DeepSeek | 2025 | Reasoning-focused |
| Command R+ | 128K tokens | Cohere | 2024 | RAG-optimized |
| Grok-2 | 128K tokens | xAI | 2024 | Real-time data access |
| Qwen 2.5 72B | 128K tokens | Alibaba | 2024 | Multilingual |

> **Note:** Context window size alone does not determine quality. Effective utilization across the full window varies significantly between models. See the [RULER benchmark](https://arxiv.org/abs/2404.06654) and [Needle-in-a-Haystack](https://github.com/gkamradt/LLMTest_NeedleInAHaystack) for empirical evaluations.

---

## 📚 Research Papers

> Full details, abstracts, and annotations available in **[papers/README.md](papers/README.md)**

### Context Window & Long Context

| # | Paper | Authors | Year | Key Contribution |
|:-:|:------|:--------|:----:|:-----------------|
| 1 | [Lost in the Middle: How Language Models Use Long Contexts](https://arxiv.org/abs/2307.03172) | Liu et al. | 2023 | ![Badge](https://img.shields.io/badge/-Foundational-red) |
| 2 | [Extending Context Window of LLMs via Positional Interpolation](https://arxiv.org/abs/2306.15595) | Chen et al. | 2023 | ![Badge](https://img.shields.io/badge/-Method-blue) |
| 3 | [LongRoPE: Extending LLM Context Window Beyond 2 Million Tokens](https://arxiv.org/abs/2402.13753) | Ding et al. | 2024 | ![Badge](https://img.shields.io/badge/-Scaling-purple) |
| 4 | [Ring Attention with Blockwise Transformers](https://arxiv.org/abs/2310.01889) | Liu et al. | 2023 | ![Badge](https://img.shields.io/badge/-Infrastructure-orange) |
| 5 | [YaRN: Efficient Context Window Extension of LLMs](https://arxiv.org/abs/2309.00071) | Peng et al. | 2023 | ![Badge](https://img.shields.io/badge/-Method-blue) |
| 6 | [Effective Long-Context Scaling of Foundation Models](https://arxiv.org/abs/2309.16039) | Xiong et al. (Meta) | 2023 | ![Badge](https://img.shields.io/badge/-Scaling-purple) |
| 7 | [LongLoRA: Efficient Fine-tuning of Long-Context LLMs](https://arxiv.org/abs/2309.12307) | Chen et al. | 2023 | ![Badge](https://img.shields.io/badge/-Efficiency-green) |
| 8 | [RULER: What's the Real Context Size of Your LLM?](https://arxiv.org/abs/2404.06654) | Hsieh et al. | 2024 | ![Badge](https://img.shields.io/badge/-Benchmark-yellow) |
| 9 | [Leave No Context Behind: Efficient Infinite Context Transformers with Infini-attention](https://arxiv.org/abs/2404.07143) | Munkhdalai et al. (Google) | 2024 | ![Badge](https://img.shields.io/badge/-Architecture-teal) |
| 10 | [Data Engineering for Scaling Language Models to 128K Context](https://arxiv.org/abs/2402.10171) | Fu et al. | 2024 | ![Badge](https://img.shields.io/badge/-Data-brown) |

### Retrieval-Augmented Generation (RAG)

| # | Paper | Authors | Year | Key Contribution |
|:-:|:------|:--------|:----:|:-----------------|
| 11 | [Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks](https://arxiv.org/abs/2005.11401) | Lewis et al. | 2020 | ![Badge](https://img.shields.io/badge/-Foundational-red) |
| 12 | [Self-RAG: Learning to Retrieve, Generate, and Critique](https://arxiv.org/abs/2310.11511) | Asai et al. | 2023 | ![Badge](https://img.shields.io/badge/-Method-blue) |
| 13 | [RAPTOR: Recursive Abstractive Processing for Tree-Organized Retrieval](https://arxiv.org/abs/2401.18059) | Sarthi et al. | 2024 | ![Badge](https://img.shields.io/badge/-Architecture-teal) |
| 14 | [Corrective Retrieval-Augmented Generation (CRAG)](https://arxiv.org/abs/2401.15884) | Yan et al. | 2024 | ![Badge](https://img.shields.io/badge/-Method-blue) |
| 15 | [Active Retrieval Augmented Generation (FLARE)](https://arxiv.org/abs/2305.06983) | Jiang et al. | 2023 | ![Badge](https://img.shields.io/badge/-Method-blue) |
| 16 | [Dense Passage Retrieval for Open-Domain QA](https://arxiv.org/abs/2004.04906) | Karpukhin et al. | 2020 | ![Badge](https://img.shields.io/badge/-Foundational-red) |
| 17 | [ColBERT: Efficient and Effective Passage Search via Late Interaction](https://arxiv.org/abs/2004.12832) | Khattab & Zaharia | 2020 | ![Badge](https://img.shields.io/badge/-Efficiency-green) |
| 18 | [Adaptive-RAG: Learning to Adapt Retrieval-Augmented LLMs](https://arxiv.org/abs/2403.14403) | Jeong et al. | 2024 | ![Badge](https://img.shields.io/badge/-Method-blue) |
| 19 | [Seven Failure Points When Engineering a RAG System](https://arxiv.org/abs/2401.05856) | Barnett et al. | 2024 | ![Badge](https://img.shields.io/badge/-Survey-grey) |
| 20 | [A Survey on RAG Meets LLMs](https://arxiv.org/abs/2405.06211) | Fan et al. | 2024 | ![Badge](https://img.shields.io/badge/-Survey-grey) |

### Prompt Engineering & Optimization

| # | Paper | Authors | Year | Key Contribution |
|:-:|:------|:--------|:----:|:-----------------|
| 21 | [Chain-of-Thought Prompting Elicits Reasoning in LLMs](https://arxiv.org/abs/2201.11903) | Wei et al. | 2022 | ![Badge](https://img.shields.io/badge/-Foundational-red) |
| 22 | [Tree of Thoughts: Deliberate Problem Solving with LLMs](https://arxiv.org/abs/2305.10601) | Yao et al. | 2023 | ![Badge](https://img.shields.io/badge/-Method-blue) |
| 23 | [DSPy: Compiling Declarative Language Model Calls](https://arxiv.org/abs/2310.03714) | Khattab et al. | 2023 | ![Badge](https://img.shields.io/badge/-Framework-cyan) |
| 24 | [Automatic Prompt Optimization with Gradient Descent and Beam Search](https://arxiv.org/abs/2305.03495) | Pryzant et al. | 2023 | ![Badge](https://img.shields.io/badge/-Method-blue) |
| 25 | [Large Language Models Are Human-Level Prompt Engineers](https://arxiv.org/abs/2211.01910) | Zhou et al. | 2022 | ![Badge](https://img.shields.io/badge/-Method-blue) |
| 26 | [Principled Instructions Are All You Need](https://arxiv.org/abs/2312.16171) | Bsharat et al. | 2023 | ![Badge](https://img.shields.io/badge/-Guidelines-pink) |
| 27 | [Graph of Thoughts: Solving Elaborate Problems with LLMs](https://arxiv.org/abs/2308.09687) | Besta et al. | 2023 | ![Badge](https://img.shields.io/badge/-Method-blue) |

### Memory & Context Management

| # | Paper | Authors | Year | Key Contribution |
|:-:|:------|:--------|:----:|:-----------------|
| 28 | [MemGPT: Towards LLMs as Operating Systems](https://arxiv.org/abs/2310.08560) | Packer et al. | 2023 | ![Badge](https://img.shields.io/badge/-Architecture-teal) |
| 29 | [Reflexion: Language Agents with Verbal Reinforcement Learning](https://arxiv.org/abs/2303.11366) | Shinn et al. | 2023 | ![Badge](https://img.shields.io/badge/-Agents-violet) |
| 30 | [LLMLingua: Compressing Prompts for Accelerated Inference](https://arxiv.org/abs/2310.05736) | Jiang et al. | 2023 | ![Badge](https://img.shields.io/badge/-Compression-darkgreen) |
| 31 | [Voyager: An Open-Ended Embodied Agent with LLMs](https://arxiv.org/abs/2305.16291) | Wang et al. | 2023 | ![Badge](https://img.shields.io/badge/-Agents-violet) |
| 32 | [Cognitive Architectures for Language Agents](https://arxiv.org/abs/2309.02427) | Sumers et al. | 2023 | ![Badge](https://img.shields.io/badge/-Survey-grey) |
| 33 | [LongMem: Augmenting LLMs with Long-Term Memory](https://arxiv.org/abs/2306.07174) | Wang et al. | 2023 | ![Badge](https://img.shields.io/badge/-Architecture-teal) |
| 34 | [Walking Down the Memory Maze: Beyond Context Limit through Interactive Reading](https://arxiv.org/abs/2310.05029) | Chen et al. | 2023 | ![Badge](https://img.shields.io/badge/-Method-blue) |

---

## 📹 YouTube Videos & Talks

> Full playlist with timestamps and key takeaways in **[videos/README.md](videos/README.md)**

| # | Title | Channel | Year | Duration | Level |
|:-:|:------|:--------|:----:|:--------:|:-----:|
| 1 | [Let's Build GPT: From Scratch, In Code](https://www.youtube.com/watch?v=kCc8FmEb1nY) | Andrej Karpathy | 2023 | 2h | 🔴 |
| 2 | [Intro to Large Language Models](https://www.youtube.com/watch?v=zjkBMFhNj_g) | Andrej Karpathy | 2023 | 1h | 🟢 |
| 3 | [Attention Is All You Need (Illustrated)](https://www.youtube.com/watch?v=XowwKOAWYoQ) | Yannic Kilcher | 2021 | 45m | 🟡 |
| 4 | [But What Is a GPT? Visual Intro to Transformers](https://www.youtube.com/watch?v=wjZofJX0v4M) | 3Blue1Brown | 2024 | 27m | 🟢 |
| 5 | [Visualizing Attention in Transformers](https://www.youtube.com/watch?v=eMlx5fFNoYc) | 3Blue1Brown | 2024 | 26m | 🟢 |
| 6 | [RAG from Scratch (Full Course)](https://www.youtube.com/watch?v=sVcwVQRHIc8) | LangChain | 2024 | 2h | 🟡 |
| 7 | [Context Engineering for AI Agents](https://www.youtube.com/watch?v=dC8HZO_qtXo) | AI Jason | 2024 | 20m | 🟡 |
| 8 | [Building Production RAG Systems](https://www.youtube.com/watch?v=TRjq7t2Ms5I) | AI Engineer | 2024 | 35m | 🔴 |
| 9 | [How ChatGPT Works Technically](https://www.youtube.com/watch?v=bSvTVREwSNw) | ByteByteGo | 2023 | 15m | 🟢 |
| 10 | [The Illustrated Retrieval Transformer](https://www.youtube.com/watch?v=SZorAJ4I-sA) | Jay Alammar | 2023 | 18m | 🟡 |
| 11 | [Advanced RAG Techniques](https://www.youtube.com/watch?v=wd7TZ4w1mSw) | DeepLearning.AI | 2024 | 1h | 🟡 |
| 12 | [Prompt Engineering Full Course](https://www.youtube.com/watch?v=_ZvnD96BbJI) | freeCodeCamp | 2024 | 4h | 🟢 |
| 13 | [Building AI Agents with Long-Term Memory](https://www.youtube.com/watch?v=Eb8xBDy0Jss) | AI Jason | 2024 | 22m | 🟡 |
| 14 | [Stanford CS25 — Transformers United](https://www.youtube.com/watch?v=P127jhj-8-Y) | Stanford Online | 2024 | 1.5h | 🔴 |
| 15 | [DSPy Explained: The Framework for Programming LLMs](https://www.youtube.com/watch?v=41EfOY0Ldkc) | Connor Shorten | 2024 | 30m | 🟡 |
| 16 | [Vector Databases Explained](https://www.youtube.com/watch?v=klTvEwg3oJ4) | Fireship | 2023 | 8m | 🟢 |
| 17 | [Sam Altman on the Future of AI](https://www.youtube.com/watch?v=e1cf58VWzt8) | Lex Fridman Podcast | 2024 | 2.5h | 🟢 |
| 18 | [Dario Amodei on Anthropic's Vision](https://www.youtube.com/watch?v=ugvHCXCOmm4) | Lex Fridman Podcast | 2024 | 2.5h | 🟢 |
| 19 | [The REAL Problem with RAG (and How to Fix It)](https://www.youtube.com/watch?v=A2RRxQ86XGE) | James Briggs | 2024 | 25m | 🟡 |
| 20 | [Building Effective Agents](https://www.youtube.com/watch?v=T-D1OfcDW1M) | Anthropic | 2025 | 45m | 🟡 |
| 21 | [Context Windows Deep Dive](https://www.youtube.com/watch?v=cW8bkMH0psI) | Weights & Biases | 2024 | 40m | 🔴 |
| 22 | [Chunking Strategies for RAG](https://www.youtube.com/watch?v=8OJC21T2SL4) | Greg Kamradt | 2023 | 30m | 🟡 |

---

## 📝 Blog Posts & Articles

> Full list with summaries and key takeaways in **[blogs/README.md](blogs/README.md)**

| # | Title | Author / Source | Date | Level |
|:-:|:------|:---------------|:----:|:-----:|
| 1 | [Prompt Engineering Guide](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/overview) | Anthropic | 2024 | 🟢 |
| 2 | [OpenAI Prompt Engineering Guide](https://platform.openai.com/docs/guides/prompt-engineering) | OpenAI | 2024 | 🟢 |
| 3 | [Building RAG-Based LLM Applications](https://www.anyscale.com/blog/a-comprehensive-guide-for-building-rag-based-llm-applications-part-1) | Anyscale | 2024 | 🟡 |
| 4 | [The Illustrated Transformer](https://jalammar.github.io/illustrated-transformer/) | Jay Alammar | 2018 | 🟢 |
| 5 | [Chunking Strategies for LLM Applications](https://www.pinecone.io/learn/chunking-strategies/) | Pinecone | 2023 | 🟡 |
| 6 | [What We Learned from a Year of Building with LLMs](https://www.oreilly.com/radar/what-we-learned-from-a-year-of-building-with-llms-part-i/) | O'Reilly | 2024 | 🔴 |
| 7 | [Patterns for Building LLM-Based Systems](https://eugeneyan.com/writing/llm-patterns/) | Eugene Yan | 2023 | 🟡 |
| 8 | [RAG Is More Than Just Vector Search](https://www.llamaindex.ai/blog/rag-is-more-than-just-vector-search) | LlamaIndex | 2024 | 🟡 |
| 9 | [Large Language Model Agents (MOOC Materials)](https://llmagents-learning.org/f24) | Dawn Song / UC Berkeley | 2024 | 🔴 |
| 10 | [Long Context Prompting for Claude](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/long-context-tips) | Anthropic | 2024 | 🟡 |
| 11 | [Prompt Engineering vs Context Engineering](https://simonwillison.net/2025/Jan/context-engineering/) | Simon Willison | 2025 | 🟢 |
| 12 | [Building Effective Agents](https://www.anthropic.com/engineering/building-effective-agents) | Anthropic | 2024 | 🟡 |
| 13 | [A Visual Guide to Quantization](https://newsletter.maartengrootendorst.com/p/a-visual-guide-to-quantization) | Maarten Grootendorst | 2024 | 🟡 |
| 14 | [The Full Stack of AI Engineering](https://newsletter.pragmaticengineer.com/p/ai-engineering) | Pragmatic Engineer | 2024 | 🟢 |
| 15 | [Evaluation Driven Development for LLM Apps](https://hamel.dev/blog/posts/evals/) | Hamel Husain | 2024 | 🔴 |
| 16 | [Understanding Retrieval-Augmented Generation](https://lilianweng.github.io/posts/2024-07-07-hallucination/) | Lilian Weng | 2024 | 🔴 |
| 17 | [Agents Overview](https://lilianweng.github.io/posts/2023-06-23-agent/) | Lilian Weng | 2023 | 🔴 |
| 18 | [Prompt Engineering (Comprehensive Guide)](https://lilianweng.github.io/posts/2023-03-15-prompt-engineering/) | Lilian Weng | 2023 | 🟡 |
| 19 | [How to Build an AI Agent](https://blog.langchain.dev/how-to-build-an-ai-agent/) | LangChain | 2024 | 🟡 |
| 20 | [The Architecture of a Modern RAG System](https://blog.llamaindex.ai/the-architecture-of-modern-rag) | LlamaIndex | 2024 | 🔴 |
| 21 | [Context Engineering: The Next Frontier](https://www.latent.space/p/context-engineering) | Latent Space | 2025 | 🟡 |
| 22 | [Embedding Models: From OpenAI to Open Source](https://huggingface.co/blog/mteb) | Hugging Face | 2024 | 🟡 |
| 23 | [Why RAG Systems Fail and How to Fix Them](https://towardsdatascience.com/rag-failure-points/) | Towards Data Science | 2024 | 🟡 |
| 24 | [Structured Output from LLMs](https://www.boundaryml.com/blog/structured-output-from-llms) | BoundaryML | 2024 | 🟡 |
| 25 | [The Rise of the AI Engineer](https://www.latent.space/p/ai-engineer) | Latent Space | 2023 | 🟢 |
| 26 | [A Practitioner's Guide to RAG](https://cameronrwolfe.substack.com/p/a-practitioners-guide-to-retrieval) | Cameron Wolfe | 2024 | 🟡 |
| 27 | [Understanding Mixture of Experts](https://huggingface.co/blog/moe) | Hugging Face | 2024 | 🔴 |

---

## 🛠️ Tools & Frameworks

> Full comparison with features, pricing, and use cases in **[tools/README.md](tools/README.md)**

### Orchestration Frameworks

| Tool | Description | Language | Stars | License |
|:-----|:-----------|:--------:|:-----:|:-------:|
| [LangChain](https://github.com/langchain-ai/langchain) | Comprehensive LLM application framework | Python/JS | 98k+ | MIT |
| [LlamaIndex](https://github.com/run-llama/llama_index) | Data framework for LLM context augmentation | Python | 37k+ | MIT |
| [DSPy](https://github.com/stanfordnlp/dspy) | Programming (not prompting) language models | Python | 19k+ | MIT |
| [Haystack](https://github.com/deepset-ai/haystack) | End-to-end NLP / RAG framework | Python | 17k+ | Apache 2.0 |
| [Semantic Kernel](https://github.com/microsoft/semantic-kernel) | Microsoft's LLM orchestration SDK | C#/Python | 22k+ | MIT |
| [CrewAI](https://github.com/joaomdmoura/crewAI) | Multi-agent orchestration framework | Python | 24k+ | MIT |
| [AutoGen](https://github.com/microsoft/autogen) | Multi-agent conversation framework | Python | 35k+ | MIT |

### Vector Databases

| Database | Type | Hosted | Open Source | Key Feature |
|:---------|:----:|:------:|:-----------:|:-----------|
| [Pinecone](https://www.pinecone.io/) | Cloud-native | Yes | No | Fully managed, enterprise-grade |
| [Weaviate](https://weaviate.io/) | Hybrid | Yes | Yes | GraphQL API, hybrid search |
| [Chroma](https://www.trychroma.com/) | Embedded/Cloud | Yes | Yes | Developer-friendly, lightweight |
| [Milvus](https://milvus.io/) | Distributed | Yes | Yes | Billion-scale vector search |
| [Qdrant](https://qdrant.tech/) | Cloud/Self-hosted | Yes | Yes | Rust-based, filtering support |
| [pgvector](https://github.com/pgvector/pgvector) | PostgreSQL extension | No | Yes | Use existing Postgres infra |
| [FAISS](https://github.com/facebookresearch/faiss) | Library | No | Yes | Meta's similarity search library |

### Embedding Models

| Model | Provider | Dimensions | Context | Notes |
|:------|:--------:|:----------:|:-------:|:------|
| text-embedding-3-large | OpenAI | 3072 | 8191 | Best commercial embedding |
| text-embedding-3-small | OpenAI | 1536 | 8191 | Cost-effective |
| embed-v4 | Cohere | 1024 | 512 | Multilingual, compressed |
| voyage-3 | Voyage AI | 1024 | 32000 | Long-context embeddings |
| BGE-M3 | BAAI | 1024 | 8192 | Best open-source multilingual |
| GTE-Qwen2 | Alibaba | 1536 | 32000 | Long-context open-source |
| NomicEmbed | Nomic | 768 | 8192 | Fully open-source, auditable |

### Context Management & Agents

| Tool | Purpose | Key Feature |
|:-----|:--------|:-----------|
| [MemGPT / Letta](https://github.com/cpacker/MemGPT) | LLM memory management | Virtual context, self-editing memory |
| [Mem0](https://github.com/mem0ai/mem0) | Memory layer for AI | Personalized memory for agents |
| [LangMem](https://github.com/langchain-ai/langmem) | Long-term memory for LangChain | Persistent conversational memory |
| [Instructor](https://github.com/jxnl/instructor) | Structured output from LLMs | Pydantic-based extraction |
| [Guardrails AI](https://github.com/guardrails-ai/guardrails) | LLM output validation | Structure, type, and quality checks |

---

## 🎓 Courses & Tutorials

> Full list with curriculum details in **[courses/README.md](courses/README.md)**

| # | Course | Provider | Level | Format | Cost |
|:-:|:-------|:---------|:-----:|:------:|:----:|
| 1 | [ChatGPT Prompt Engineering for Developers](https://www.deeplearning.ai/short-courses/chatgpt-prompt-engineering-for-developers/) | DeepLearning.AI + OpenAI | 🟢 | Video | Free |
| 2 | [Building Systems with the ChatGPT API](https://www.deeplearning.ai/short-courses/building-systems-with-chatgpt/) | DeepLearning.AI + OpenAI | 🟡 | Video | Free |
| 3 | [LangChain for LLM Application Development](https://www.deeplearning.ai/short-courses/langchain-for-llm-application-development/) | DeepLearning.AI + LangChain | 🟡 | Video | Free |
| 4 | [Building and Evaluating Advanced RAG](https://www.deeplearning.ai/short-courses/building-evaluating-advanced-rag/) | DeepLearning.AI + LlamaIndex | 🟡 | Video | Free |
| 5 | [Stanford CS324: Large Language Models](https://stanford-cs324.github.io/winter2022/) | Stanford | 🔴 | Lecture | Free |
| 6 | [Stanford CS25: Transformers United](https://web.stanford.edu/class/cs25/) | Stanford | 🔴 | Seminar | Free |
| 7 | [Hugging Face NLP Course](https://huggingface.co/learn/nlp-course) | Hugging Face | 🟢 | Interactive | Free |
| 8 | [Full Stack LLM Bootcamp](https://fullstackdeeplearning.com/llm-bootcamp/) | FSDL | 🟡 | Video | Free |
| 9 | [Practical Deep Learning for Coders](https://course.fast.ai/) | fast.ai | 🟡 | Video | Free |
| 10 | [LLM University](https://cohere.com/llmu) | Cohere | 🟢 | Interactive | Free |
| 11 | [Prompt Engineering Specialization](https://www.deeplearning.ai/courses/prompt-engineering-specialization/) | DeepLearning.AI | 🟢 | Video | Paid |
| 12 | [UC Berkeley LLM Agents MOOC](https://llmagents-learning.org/f24) | UC Berkeley | 🔴 | Video | Free |

---

## 📊 Techniques & Patterns

> Full deep-dive with code examples in **[techniques/README.md](techniques/README.md)**

### 1. Chunking Strategies

The way you split documents determines retrieval quality.

```
┌──────────────────────────────────────────────────────────────┐
│                    CHUNKING STRATEGIES                        │
├──────────────────┬──────────────────┬────────────────────────┤
│   Fixed-Size     │    Semantic      │    Recursive           │
│                  │                  │                        │
│  Split every N   │  Split by        │  Try large chunks      │
│  tokens with     │  meaning/topic   │  first, then split     │
│  overlap         │  boundaries      │  smaller if needed     │
│                  │                  │                        │
│  ✅ Simple       │  ✅ Coherent     │  ✅ Adaptive           │
│  ✅ Predictable  │  ✅ Better       │  ✅ Respects           │
│  ❌ Breaks       │     retrieval    │     document           │
│     meaning      │  ❌ Expensive    │     structure          │
│                  │  ❌ Complex      │  ❌ More complex       │
└──────────────────┴──────────────────┴────────────────────────┘
```

### 2. Retrieval Patterns

```
┌─────────────┐    ┌──────────────────┐    ┌───────────────────┐
│  Naive RAG  │───>│  Advanced RAG    │───>│  Modular RAG      │
│             │    │                  │    │                   │
│ Query ──>   │    │ Query Rewrite    │    │ Router ──> RAG    │
│ Retrieve -> │    │ ──> HyDE         │    │       ──> Agent   │
│ Generate    │    │ ──> Retrieve     │    │       ──> Direct  │
│             │    │ ──> Rerank       │    │                   │
│             │    │ ──> Generate     │    │ Composable        │
│             │    │                  │    │ pipelines         │
└─────────────┘    └──────────────────┘    └───────────────────┘
     🟢                   🟡                       🔴
```

### 3. Context Compression

Reduce token usage while preserving signal:
- **Extractive**: Select only the most relevant sentences/paragraphs
- **Abstractive**: Summarize retrieved chunks before injection
- **Token-level**: Use LLMLingua to prune low-information tokens (up to 20x compression)
- **Semantic deduplication**: Remove redundant information across retrieved chunks

### 4. Context Caching

Reuse expensive context across requests:
- **Prefix caching**: Cache system prompts and few-shot examples (supported by Anthropic, Google)
- **KV-cache sharing**: Share key-value caches across similar requests
- **Semantic caching**: Cache responses for semantically similar queries

### 5. Sliding Window Attention

```
Full Attention (O(n^2)):     Sliding Window (O(n * w)):
┌─────────────┐              ┌─────────────┐
│ █ █ █ █ █ █ │              │ █ █ █ · · · │
│ █ █ █ █ █ █ │              │ · █ █ █ · · │
│ █ █ █ █ █ █ │              │ · · █ █ █ · │
│ █ █ █ █ █ █ │              │ · · · █ █ █ │
│ █ █ █ █ █ █ │              │ · · · · █ █ │
│ █ █ █ █ █ █ │              │ · · · · · █ │
└─────────────┘              └─────────────┘
```

### 6. Multi-hop Reasoning

Chain multiple retrieval steps to answer complex questions:
1. Decompose query into sub-questions
2. Retrieve for each sub-question independently
3. Synthesize intermediate answers
4. Use intermediate answers to refine retrieval
5. Generate final comprehensive answer

### 7. Few-Shot Learning Optimization

- **Dynamic few-shot**: Select examples most similar to the current query
- **Diverse few-shot**: Ensure coverage of edge cases and formats
- **Ordered few-shot**: Place most relevant examples closest to the query (recency bias)

### 8. System Prompt Engineering

```
┌────────────────────────────────────────────┐
│            SYSTEM PROMPT LAYERS             │
├────────────────────────────────────────────┤
│  1. IDENTITY   │ Role, persona, expertise  │
│  2. CONTEXT    │ Background information    │
│  3. RULES      │ Constraints, boundaries   │
│  4. FORMAT     │ Output structure          │
│  5. EXAMPLES   │ Reference behaviors       │
│  6. FALLBACK   │ Edge case handling        │
└────────────────────────────────────────────┘
```

---

## 🗺️ Roadmap

### Context Engineering Learning Path

```
                    🎯 CONTEXT ENGINEERING MASTERY
                              │
                 ┌────────────┴────────────┐
                 │                         │
            FOUNDATIONS              APPLICATIONS
                 │                         │
         ┌───────┴───────┐          ┌──────┴──────┐
         │               │          │             │
    THEORY          PRACTICE    PRODUCTION    RESEARCH
         │               │          │             │
         ▼               ▼          ▼             ▼

🟢 BEGINNER (Weeks 1-4)
├── Understand transformer attention mechanisms
├── Learn token counting and context window basics
├── Master basic prompt engineering patterns
├── Study the Illustrated Transformer blog post
├── Complete DeepLearning.AI prompt engineering course
└── Build a simple chatbot with system prompts

🟡 INTERMEDIATE (Weeks 5-10)
├── Implement naive RAG with vector database
├── Learn chunking strategies (fixed, semantic, recursive)
├── Study embedding models and similarity search
├── Implement context compression techniques
├── Build an advanced RAG system with reranking
├── Learn evaluation metrics (faithfulness, relevance, recall)
├── Study "Lost in the Middle" paper and information ordering
└── Complete LangChain / LlamaIndex course

🔴 ADVANCED (Weeks 11-16)
├── Design multi-agent systems with shared context
├── Implement hierarchical memory (short/long/working)
├── Build modular RAG pipelines with routing
├── Study DSPy for programmatic prompt optimization
├── Implement context caching and cost optimization
├── Learn to evaluate with RAGAS, DeepEval, or custom evals
├── Study agentic RAG patterns (CRAG, Self-RAG, FLARE)
└── Build a production system with monitoring and fallbacks

⭐ EXPERT (Ongoing)
├── Contribute to open-source context engineering tools
├── Publish research on novel context management techniques
├── Design context architectures for enterprise systems
├── Optimize for cost, latency, and quality simultaneously
└── Mentor others in context engineering practices
```

---

## Contributing

We welcome contributions from the community. Here is how you can help:

1. **Add a resource** — Open a PR with a new paper, video, blog post, or tool
2. **Fix errors** — Found a broken link or incorrect information? Open an issue
3. **Improve explanations** — Help make the techniques section clearer
4. **Add code examples** — Contribute working code for context engineering patterns
5. **Translate** — Help translate this guide to other languages

Please read our contribution guidelines before submitting.

### How to Contribute

```bash
# Fork the repository
git clone https://github.com/mlnjsh/context-engineering.git
cd context-engineering

# Create a feature branch
git checkout -b add-new-resource

# Make your changes and commit
git add .
git commit -m "Add [resource type]: [resource name]"

# Push and create a PR
git push origin add-new-resource
```

---

## Citation

If you find this resource helpful in your research or work, please consider citing it:

```bibtex
@misc{joshi2025contextengineering,
  title   = {Context Engineering: The Complete Guide},
  author  = {Joshi, Milan Amrut},
  year    = {2025},
  url     = {https://github.com/mlnjsh/context-engineering},
  note    = {A curated guide to context engineering for large language models}
}
```

---

## License

This work is licensed under the [MIT License](LICENSE).

---

<div align="center">

**Built with care by [Professor Milan Amrut Joshi](https://github.com/mlnjsh)**

*Professor of Data Science, Northwestern University*

If this resource helped you, please consider giving it a star.

[![Star History Chart](https://api.star-history.com/svg?repos=mlnjsh/context-engineering&type=Date)](https://star-history.com/#mlnjsh/context-engineering&Date)

</div>
