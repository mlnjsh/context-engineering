<div align="center">

# 📝 Blog Posts & Articles on Context Engineering

*Curated collection of the best written resources on context engineering, RAG, and LLM systems*

[Back to Main Guide](../README.md)

</div>

---

## How to Use This List

Each article includes:
- **Title** with direct link
- **Author/Source** and publication date
- **Level**: 🟢 Beginner | 🟡 Intermediate | 🔴 Advanced
- **Key Points** (3-5 bullet points)
- **Category** badge

---

## Official Guides & Documentation

### 1. Prompt Engineering Guide

- **Source:** Anthropic
- **Date:** 2024 (continuously updated)
- **Level:** 🟢
- **Link:** [docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/overview](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/overview)
- **Category:** ![Official](https://img.shields.io/badge/-Official_Guide-blue)

**Key Points:**
- Comprehensive guide to prompting Claude models effectively
- Covers system prompts, multimodal prompting, and tool use
- Includes long-context prompting tips specific to 200K token windows
- Best practices for structured output and chain-of-thought

---

### 2. OpenAI Prompt Engineering Guide

- **Source:** OpenAI
- **Date:** 2024 (continuously updated)
- **Level:** 🟢
- **Link:** [platform.openai.com/docs/guides/prompt-engineering](https://platform.openai.com/docs/guides/prompt-engineering)
- **Category:** ![Official](https://img.shields.io/badge/-Official_Guide-blue)

**Key Points:**
- Six core strategies for better prompting
- Tactics for complex tasks, splitting, and external tools
- Systematic testing and evaluation methodology
- Function calling and structured output patterns

---

### 3. Long Context Prompting Tips for Claude

- **Source:** Anthropic
- **Date:** 2024
- **Level:** 🟡
- **Link:** [docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/long-context-tips](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/long-context-tips)
- **Category:** ![Official](https://img.shields.io/badge/-Official_Guide-blue)

**Key Points:**
- Specific strategies for using Claude's 200K token context window
- Document placement and ordering recommendations
- How to structure queries for multi-document reasoning
- Techniques for extracting information from large contexts

---

### 4. Building Effective Agents

- **Source:** Anthropic
- **Date:** 2024
- **Level:** 🟡
- **Link:** [anthropic.com/engineering/building-effective-agents](https://www.anthropic.com/engineering/building-effective-agents)
- **Category:** ![Official](https://img.shields.io/badge/-Official_Guide-blue)

**Key Points:**
- Anthropic's framework for when and how to build AI agents
- Augmented LLMs vs. agentic systems taxonomy
- Workflow patterns: prompt chaining, routing, parallelization
- Context management for multi-step agent tasks

---

## Foundational Articles

### 5. The Illustrated Transformer

- **Author:** Jay Alammar
- **Date:** 2018 (evergreen)
- **Level:** 🟢
- **Link:** [jalammar.github.io/illustrated-transformer/](https://jalammar.github.io/illustrated-transformer/)
- **Category:** ![Foundational](https://img.shields.io/badge/-Foundational-red)

**Key Points:**
- The gold standard visual explanation of transformer architecture
- Step-by-step walkthrough of self-attention
- Explains positional encoding and why it matters for context
- Essential reading before diving into context engineering

---

### 6. Prompt Engineering (Comprehensive Guide)

- **Author:** Lilian Weng (OpenAI)
- **Date:** 2023
- **Level:** 🟡
- **Link:** [lilianweng.github.io/posts/2023-03-15-prompt-engineering/](https://lilianweng.github.io/posts/2023-03-15-prompt-engineering/)
- **Category:** ![Deep_Dive](https://img.shields.io/badge/-Deep_Dive-purple)

**Key Points:**
- Exhaustive survey of prompt engineering techniques
- Covers zero-shot, few-shot, CoT, ToT, and more
- Mathematical framing of prompting strategies
- Excellent bibliography for further reading

---

### 7. LLM Powered Autonomous Agents

- **Author:** Lilian Weng (OpenAI)
- **Date:** 2023
- **Level:** 🔴
- **Link:** [lilianweng.github.io/posts/2023-06-23-agent/](https://lilianweng.github.io/posts/2023-06-23-agent/)
- **Category:** ![Deep_Dive](https://img.shields.io/badge/-Deep_Dive-purple)

**Key Points:**
- Defines the architecture of LLM-based agents
- Memory types: sensory, short-term, long-term
- Planning strategies: task decomposition, self-reflection
- Tool use and context management for agents

---

### 8. Extrinsic Hallucinations in LLMs

- **Author:** Lilian Weng (OpenAI)
- **Date:** 2024
- **Level:** 🔴
- **Link:** [lilianweng.github.io/posts/2024-07-07-hallucination/](https://lilianweng.github.io/posts/2024-07-07-hallucination/)
- **Category:** ![Deep_Dive](https://img.shields.io/badge/-Deep_Dive-purple)

**Key Points:**
- Comprehensive analysis of hallucination causes and mitigations
- How context quality affects hallucination rates
- RAG as a hallucination reduction strategy
- Evaluation metrics for factuality

---

## RAG & Retrieval

### 9. Chunking Strategies for LLM Applications

- **Source:** Pinecone
- **Date:** 2023
- **Level:** 🟡
- **Link:** [pinecone.io/learn/chunking-strategies/](https://www.pinecone.io/learn/chunking-strategies/)
- **Category:** ![Practical](https://img.shields.io/badge/-Practical-green)

**Key Points:**
- Detailed comparison of chunking approaches
- Fixed-size, sentence-level, recursive, and semantic chunking
- Impact of chunk size on retrieval quality and LLM generation
- Practical recommendations with code examples

---

### 10. RAG Is More Than Just Vector Search

- **Source:** LlamaIndex Blog
- **Date:** 2024
- **Level:** 🟡
- **Link:** [llamaindex.ai/blog/rag-is-more-than-just-vector-search](https://www.llamaindex.ai/blog/rag-is-more-than-just-vector-search)
- **Category:** ![Practical](https://img.shields.io/badge/-Practical-green)

**Key Points:**
- RAG as a complete system, not just retrieval
- Query understanding, routing, and multi-step reasoning
- Post-retrieval processing: reranking, compression, fusion
- Evaluation and iteration of RAG pipelines

---

### 11. A Practitioner's Guide to Retrieval-Augmented Generation

- **Author:** Cameron Wolfe
- **Date:** 2024
- **Level:** 🟡
- **Link:** [cameronrwolfe.substack.com/p/a-practitioners-guide-to-retrieval](https://cameronrwolfe.substack.com/p/a-practitioners-guide-to-retrieval)
- **Category:** ![Deep_Dive](https://img.shields.io/badge/-Deep_Dive-purple)

**Key Points:**
- End-to-end guide from document processing to generation
- Embedding model selection and comparison
- Retrieval optimization techniques
- Production deployment considerations

---

### 12. Building RAG-Based LLM Applications (Part 1)

- **Source:** Anyscale
- **Date:** 2024
- **Level:** 🟡
- **Link:** [anyscale.com/blog/a-comprehensive-guide-for-building-rag-based-llm-applications-part-1](https://www.anyscale.com/blog/a-comprehensive-guide-for-building-rag-based-llm-applications-part-1)
- **Category:** ![Practical](https://img.shields.io/badge/-Practical-green)

**Key Points:**
- Step-by-step guide to building production RAG
- Data ingestion, embedding, and indexing pipeline
- Scaling considerations for large document collections
- Evaluation framework for RAG quality

---

### 13. The Architecture of Modern RAG Systems

- **Source:** LlamaIndex Blog
- **Date:** 2024
- **Level:** 🔴
- **Link:** [blog.llamaindex.ai/the-architecture-of-modern-rag](https://blog.llamaindex.ai/the-architecture-of-modern-rag)
- **Category:** ![Architecture](https://img.shields.io/badge/-Architecture-teal)

**Key Points:**
- Modular RAG architecture patterns
- Router-based query handling
- Multi-index and multi-source retrieval
- Advanced patterns: self-correcting RAG, agentic RAG

---

## Production & Engineering

### 14. What We Learned from a Year of Building with LLMs (Part I)

- **Source:** O'Reilly
- **Authors:** Eugene Yan, Bryan Bischof, Charles Frye, Hamel Husain, Jason Liu, Shreya Shankar
- **Date:** 2024
- **Level:** 🔴
- **Link:** [oreilly.com/radar/what-we-learned-from-a-year-of-building-with-llms-part-i/](https://www.oreilly.com/radar/what-we-learned-from-a-year-of-building-with-llms-part-i/)
- **Category:** ![Production](https://img.shields.io/badge/-Production-orange)

**Key Points:**
- Lessons from six experienced LLM practitioners
- Prompting tactics, RAG strategies, and workflow engineering
- Evaluation and monitoring in production
- Cost optimization and latency management

---

### 15. Patterns for Building LLM-Based Systems & Products

- **Author:** Eugene Yan
- **Date:** 2023
- **Level:** 🟡
- **Link:** [eugeneyan.com/writing/llm-patterns/](https://eugeneyan.com/writing/llm-patterns/)
- **Category:** ![Architecture](https://img.shields.io/badge/-Architecture-teal)

**Key Points:**
- Seven key patterns: evals, RAG, fine-tuning, caching, guardrails, defensive UX, collection
- Practical decision framework for choosing patterns
- Trade-offs between approaches
- Real-world implementation examples

---

### 16. Evaluation Driven Development for AI/LLM Apps

- **Author:** Hamel Husain
- **Date:** 2024
- **Level:** 🔴
- **Link:** [hamel.dev/blog/posts/evals/](https://hamel.dev/blog/posts/evals/)
- **Category:** ![Production](https://img.shields.io/badge/-Production-orange)

**Key Points:**
- Why evaluation should drive development, not follow it
- Building domain-specific evaluation metrics
- Human evaluation vs. LLM-as-judge approaches
- Continuous evaluation in production systems

---

### 17. The Full Stack of AI Engineering

- **Source:** Pragmatic Engineer
- **Date:** 2024
- **Level:** 🟢
- **Link:** [newsletter.pragmaticengineer.com/p/ai-engineering](https://newsletter.pragmaticengineer.com/p/ai-engineering)
- **Category:** ![Overview](https://img.shields.io/badge/-Overview-lightblue)

**Key Points:**
- Overview of the AI engineering role and skill set
- How AI engineering differs from ML engineering
- Context engineering as a core competency
- Career path and learning resources

---

## Context Engineering Specific

### 18. Context Engineering: The Next Frontier

- **Source:** Latent Space
- **Date:** 2025
- **Level:** 🟡
- **Link:** [latent.space/p/context-engineering](https://www.latent.space/p/context-engineering)
- **Category:** ![Context_Engineering](https://img.shields.io/badge/-Context_Engineering-gold)

**Key Points:**
- Defines context engineering as a distinct discipline
- Evolution from prompt engineering to context engineering
- Real-world case studies and examples
- Future directions and open problems

---

### 19. Prompt Engineering vs Context Engineering

- **Author:** Simon Willison
- **Date:** 2025
- **Level:** 🟢
- **Link:** [simonwillison.net/2025/Jan/context-engineering/](https://simonwillison.net/2025/Jan/context-engineering/)
- **Category:** ![Context_Engineering](https://img.shields.io/badge/-Context_Engineering-gold)

**Key Points:**
- Clear articulation of the difference between prompting and context engineering
- Practical examples of context engineering in action
- How context engineering encompasses the full LLM pipeline
- Implications for how we build AI systems

---

### 20. The Rise of the AI Engineer

- **Source:** Latent Space
- **Date:** 2023
- **Level:** 🟢
- **Link:** [latent.space/p/ai-engineer](https://www.latent.space/p/ai-engineer)
- **Category:** ![Career](https://img.shields.io/badge/-Career-pink)

**Key Points:**
- Defines the emerging role of AI Engineer
- How it differs from ML Engineer and data scientist
- Context engineering as a core skill
- Industry trends and career opportunities

---

## Embeddings & Search

### 21. MTEB: Massive Text Embedding Benchmark

- **Source:** Hugging Face Blog
- **Date:** 2024
- **Level:** 🟡
- **Link:** [huggingface.co/blog/mteb](https://huggingface.co/blog/mteb)
- **Category:** ![Benchmark](https://img.shields.io/badge/-Benchmark-yellow)

**Key Points:**
- Comprehensive benchmark for evaluating embedding models
- Comparison across retrieval, classification, clustering, and more
- Guidance on choosing embedding models for RAG
- Open-source leaderboard and evaluation tools

---

### 22. A Visual Guide to Quantization

- **Author:** Maarten Grootendorst
- **Date:** 2024
- **Level:** 🟡
- **Link:** [newsletter.maartengrootendorst.com/p/a-visual-guide-to-quantization](https://newsletter.maartengrootendorst.com/p/a-visual-guide-to-quantization)
- **Category:** ![Technical](https://img.shields.io/badge/-Technical-grey)

**Key Points:**
- Visual explanation of quantization techniques
- Impact of quantization on model quality and context usage
- Practical guidance on choosing quantization levels
- Relevant for deploying models with large context windows

---

## LLM Agents & Memory

### 23. How to Build an AI Agent

- **Source:** LangChain Blog
- **Date:** 2024
- **Level:** 🟡
- **Link:** [blog.langchain.dev/how-to-build-an-ai-agent/](https://blog.langchain.dev/how-to-build-an-ai-agent/)
- **Category:** ![Practical](https://img.shields.io/badge/-Practical-green)

**Key Points:**
- Step-by-step guide to building agents with LangChain
- Tool definition and context management
- Memory patterns for multi-step agents
- Common pitfalls and debugging strategies

---

### 24. Large Language Model Agents (MOOC Materials)

- **Source:** UC Berkeley / Dawn Song
- **Date:** 2024
- **Level:** 🔴
- **Link:** [llmagents-learning.org/f24](https://llmagents-learning.org/f24)
- **Category:** ![Academic](https://img.shields.io/badge/-Academic-darkblue)

**Key Points:**
- University-level course materials on LLM agents
- Covers planning, memory, tool use, and multi-agent systems
- Research-oriented with cutting-edge topics
- Includes lectures, readings, and assignments

---

### 25. Structured Output from LLMs

- **Source:** BoundaryML
- **Date:** 2024
- **Level:** 🟡
- **Link:** [boundaryml.com/blog/structured-output-from-llms](https://www.boundaryml.com/blog/structured-output-from-llms)
- **Category:** ![Practical](https://img.shields.io/badge/-Practical-green)

**Key Points:**
- How to get reliable structured data from LLMs
- JSON mode, function calling, and schema enforcement
- How output format requirements affect context design
- Comparison of approaches across providers

---

### 26. Why RAG Systems Fail and How to Fix Them

- **Source:** Towards Data Science
- **Date:** 2024
- **Level:** 🟡
- **Link:** [towardsdatascience.com/rag-failure-points/](https://towardsdatascience.com/rag-failure-points/)
- **Category:** ![Practical](https://img.shields.io/badge/-Practical-green)

**Key Points:**
- Taxonomy of RAG failure modes
- Retrieval failures: wrong chunks, missing context, noisy results
- Generation failures: hallucination, incoherence, wrong format
- Systematic debugging and improvement strategies

---

### 27. Understanding Mixture of Experts

- **Source:** Hugging Face Blog
- **Date:** 2024
- **Level:** 🔴
- **Link:** [huggingface.co/blog/moe](https://huggingface.co/blog/moe)
- **Category:** ![Technical](https://img.shields.io/badge/-Technical-grey)

**Key Points:**
- How MoE architectures work and why they matter
- Impact on context processing efficiency
- Models like Mixtral, DeepSeek V3, and their MoE designs
- Trade-offs between dense and sparse models for context-heavy tasks

---

## Suggested Reading Order

### For Beginners

1. The Illustrated Transformer (Alammar)
2. OpenAI Prompt Engineering Guide
3. Anthropic Prompt Engineering Guide
4. Prompt Engineering vs Context Engineering (Willison)
5. The Full Stack of AI Engineering (Pragmatic Engineer)

### For Intermediate Practitioners

6. Chunking Strategies (Pinecone)
7. RAG Is More Than Just Vector Search (LlamaIndex)
8. Patterns for Building LLM-Based Systems (Eugene Yan)
9. Building Effective Agents (Anthropic)
10. Context Engineering: The Next Frontier (Latent Space)

### For Advanced Engineers

11. What We Learned from a Year of Building with LLMs (O'Reilly)
12. Evaluation Driven Development (Husain)
13. LLM Powered Autonomous Agents (Weng)
14. The Architecture of Modern RAG (LlamaIndex)
15. UC Berkeley LLM Agents MOOC

---

<div align="center">

**[Back to Main Guide](../README.md)**

</div>
