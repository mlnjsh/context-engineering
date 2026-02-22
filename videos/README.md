<div align="center">

# 📹 YouTube Videos & Talks on Context Engineering

*Curated video resources for learning about context windows, RAG, and LLM systems*

[Back to Main Guide](../README.md)

</div>

---

## How to Use This List

Each video includes:
- **Title** with direct link
- **Channel/Speaker** information
- **Duration** and publication year
- **Level**: 🟢 Beginner | 🟡 Intermediate | 🔴 Advanced
- **Key Takeaways** (3-5 bullet points)

---

## Foundations & Concepts

### 1. Let's Build GPT: From Scratch, In Code

- **Channel:** Andrej Karpathy
- **Year:** 2023
- **Duration:** ~2 hours
- **Level:** 🔴
- **Link:** [youtube.com/watch?v=kCc8FmEb1nY](https://www.youtube.com/watch?v=kCc8FmEb1nY)

**Key Takeaways:**
- Builds a GPT model from scratch in Python, explaining every component
- Deep dive into attention mechanism and how context is processed
- Understanding of token embeddings and positional encodings
- Shows why context window size is bounded by positional encoding design

---

### 2. Intro to Large Language Models

- **Channel:** Andrej Karpathy
- **Year:** 2023
- **Duration:** ~1 hour
- **Level:** 🟢
- **Link:** [youtube.com/watch?v=zjkBMFhNj_g](https://www.youtube.com/watch?v=zjkBMFhNj_g)

**Key Takeaways:**
- Excellent high-level overview of how LLMs work
- Explains training vs inference and the role of context
- Covers system prompts, tool use, and retrieval augmentation
- Great starting point for understanding why context engineering matters

---

### 3. But What Is a GPT? Visual Intro to Transformers

- **Channel:** 3Blue1Brown
- **Year:** 2024
- **Duration:** ~27 minutes
- **Level:** 🟢
- **Link:** [youtube.com/watch?v=wjZofJX0v4M](https://www.youtube.com/watch?v=wjZofJX0v4M)

**Key Takeaways:**
- Beautiful visual explanations of transformer architecture
- Intuitive understanding of self-attention and how tokens interact
- Shows why context window size matters for attention computation
- Accessible to non-technical audiences

---

### 4. Visualizing Attention, a Transformer's Heart

- **Channel:** 3Blue1Brown
- **Year:** 2024
- **Duration:** ~26 minutes
- **Level:** 🟢
- **Link:** [youtube.com/watch?v=eMlx5fFNoYc](https://www.youtube.com/watch?v=eMlx5fFNoYc)

**Key Takeaways:**
- Deep visual dive into attention patterns
- Shows how different heads attend to different context patterns
- Explains key-query-value mechanism intuitively
- Understanding attention is foundational to understanding context utilization

---

### 5. Attention Is All You Need (Paper Explained)

- **Channel:** Yannic Kilcher
- **Year:** 2021
- **Duration:** ~45 minutes
- **Level:** 🟡
- **Link:** [youtube.com/watch?v=XowwKOAWYoQ](https://www.youtube.com/watch?v=XowwKOAWYoQ)

**Key Takeaways:**
- Detailed walkthrough of the original transformer paper
- Explains multi-head attention, positional encoding, and encoder-decoder architecture
- Historical context of why transformers replaced RNNs and LSTMs
- Understanding the O(n^2) attention complexity and its implications for context length

---

## RAG & Retrieval

### 6. RAG from Scratch (Full Course)

- **Channel:** LangChain
- **Year:** 2024
- **Duration:** ~2 hours
- **Level:** 🟡
- **Link:** [youtube.com/watch?v=sVcwVQRHIc8](https://www.youtube.com/watch?v=sVcwVQRHIc8)

**Key Takeaways:**
- Complete walkthrough of building RAG from scratch
- Covers document loading, chunking, embedding, retrieval, and generation
- Demonstrates evaluation of RAG quality
- Shows common pitfalls and how to avoid them

---

### 7. Context Engineering for AI Agents

- **Channel:** AI Jason
- **Year:** 2024
- **Duration:** ~20 minutes
- **Level:** 🟡
- **Link:** [youtube.com/watch?v=dC8HZO_qtXo](https://www.youtube.com/watch?v=dC8HZO_qtXo)

**Key Takeaways:**
- Explains the shift from prompt engineering to context engineering
- Covers tool definitions, memory management, and dynamic context assembly
- Shows real-world examples of context engineering in agent systems
- Discusses cost and latency optimization

---

### 8. Building Production RAG Systems

- **Channel:** AI Engineer
- **Year:** 2024
- **Duration:** ~35 minutes
- **Level:** 🔴
- **Link:** [youtube.com/watch?v=TRjq7t2Ms5I](https://www.youtube.com/watch?v=TRjq7t2Ms5I)

**Key Takeaways:**
- Lessons from building RAG systems at scale
- Discusses chunking strategies, reranking, and hybrid search
- Covers monitoring and evaluation in production
- Cost optimization and caching strategies

---

### 9. How ChatGPT Works Technically

- **Channel:** ByteByteGo
- **Year:** 2023
- **Duration:** ~15 minutes
- **Level:** 🟢
- **Link:** [youtube.com/watch?v=bSvTVREwSNw](https://www.youtube.com/watch?v=bSvTVREwSNw)

**Key Takeaways:**
- Clear technical overview in ByteByteGo's visual style
- Explains tokenization, context window, and inference process
- Good primer on the engineering behind chat-based LLMs
- System architecture overview

---

### 10. The Illustrated Retrieval Transformer

- **Channel:** Jay Alammar
- **Year:** 2023
- **Duration:** ~18 minutes
- **Level:** 🟡
- **Link:** [youtube.com/watch?v=SZorAJ4I-sA](https://www.youtube.com/watch?v=SZorAJ4I-sA)

**Key Takeaways:**
- Visual explanation of retrieval-augmented transformers
- Shows how retrieval integrates with the attention mechanism
- Covers RETRO and similar retrieval-augmented architectures
- Bridges the gap between retrieval and generation

---

## Advanced Topics

### 11. Advanced RAG Techniques

- **Channel:** DeepLearning.AI
- **Year:** 2024
- **Duration:** ~1 hour
- **Level:** 🟡
- **Link:** [youtube.com/watch?v=wd7TZ4w1mSw](https://www.youtube.com/watch?v=wd7TZ4w1mSw)

**Key Takeaways:**
- Advanced retrieval strategies: sentence window retrieval, auto-merging
- Evaluation frameworks for RAG systems
- Multi-document reasoning techniques
- Production best practices

---

### 12. Prompt Engineering Full Course

- **Channel:** freeCodeCamp
- **Year:** 2024
- **Duration:** ~4 hours
- **Level:** 🟢
- **Link:** [youtube.com/watch?v=_ZvnD96BbJI](https://www.youtube.com/watch?v=_ZvnD96BbJI)

**Key Takeaways:**
- Comprehensive coverage of prompt engineering techniques
- Chain-of-thought, few-shot, and zero-shot strategies
- System prompt design patterns
- Hands-on exercises with multiple LLMs

---

### 13. Building AI Agents with Long-Term Memory

- **Channel:** AI Jason
- **Year:** 2024
- **Duration:** ~22 minutes
- **Level:** 🟡
- **Link:** [youtube.com/watch?v=Eb8xBDy0Jss](https://www.youtube.com/watch?v=Eb8xBDy0Jss)

**Key Takeaways:**
- How to implement persistent memory for AI agents
- Different memory types: episodic, semantic, procedural
- Integration with vector databases for long-term storage
- Context window management across sessions

---

### 14. Stanford CS25 — Transformers United

- **Channel:** Stanford Online
- **Year:** 2024
- **Duration:** ~1.5 hours
- **Level:** 🔴
- **Link:** [youtube.com/watch?v=P127jhj-8-Y](https://www.youtube.com/watch?v=P127jhj-8-Y)

**Key Takeaways:**
- Cutting-edge research talks from Stanford researchers
- Covers long-context modeling, efficient attention, and scaling
- State-of-the-art methods for extending context
- Research directions in context-aware AI

---

### 15. DSPy Explained: The Framework for Programming LLMs

- **Channel:** Connor Shorten
- **Year:** 2024
- **Duration:** ~30 minutes
- **Level:** 🟡
- **Link:** [youtube.com/watch?v=41EfOY0Ldkc](https://www.youtube.com/watch?v=41EfOY0Ldkc)

**Key Takeaways:**
- How DSPy replaces manual prompt engineering with programming
- Compilation of declarative programs into optimized prompts
- Automatic few-shot example selection and optimization
- Represents the future of automated context engineering

---

### 16. Vector Databases Explained in 8 Minutes

- **Channel:** Fireship
- **Year:** 2023
- **Duration:** ~8 minutes
- **Level:** 🟢
- **Link:** [youtube.com/watch?v=klTvEwg3oJ4](https://www.youtube.com/watch?v=klTvEwg3oJ4)

**Key Takeaways:**
- Quick, clear explanation of vector databases and embeddings
- Why vector search is essential for RAG
- Comparison of major vector database options
- ANN (Approximate Nearest Neighbor) search explained

---

## Interviews & Thought Leadership

### 17. Sam Altman on the Future of AI (Lex Fridman)

- **Channel:** Lex Fridman Podcast
- **Year:** 2024
- **Duration:** ~2.5 hours
- **Level:** 🟢
- **Link:** [youtube.com/watch?v=e1cf58VWzt8](https://www.youtube.com/watch?v=e1cf58VWzt8)

**Key Takeaways:**
- OpenAI's vision for context and memory in AI systems
- Discussion of scaling context windows vs. smarter retrieval
- AGI roadmap and the role of context understanding
- Industry perspective on where LLMs are heading

---

### 18. Dario Amodei on Anthropic's Vision (Lex Fridman)

- **Channel:** Lex Fridman Podcast
- **Year:** 2024
- **Duration:** ~2.5 hours
- **Level:** 🟢
- **Link:** [youtube.com/watch?v=ugvHCXCOmm4](https://www.youtube.com/watch?v=ugvHCXCOmm4)

**Key Takeaways:**
- Anthropic's approach to long-context models (200K token windows)
- Constitutional AI and how context shapes model behavior
- Safety considerations in context engineering
- Research directions for more capable AI systems

---

### 19. The REAL Problem with RAG (and How to Fix It)

- **Channel:** James Briggs
- **Year:** 2024
- **Duration:** ~25 minutes
- **Level:** 🟡
- **Link:** [youtube.com/watch?v=A2RRxQ86XGE](https://www.youtube.com/watch?v=A2RRxQ86XGE)

**Key Takeaways:**
- Common RAG failures and their root causes
- How chunking strategy affects retrieval quality
- Reranking and hybrid search as solutions
- Practical debugging techniques for RAG systems

---

### 20. Building Effective Agents

- **Channel:** Anthropic
- **Year:** 2025
- **Duration:** ~45 minutes
- **Level:** 🟡
- **Link:** [youtube.com/watch?v=T-D1OfcDW1M](https://www.youtube.com/watch?v=T-D1OfcDW1M)

**Key Takeaways:**
- Anthropic's framework for building reliable AI agents
- Context management patterns for multi-step tasks
- Tool use and function calling best practices
- When to use agents vs. simpler approaches

---

### 21. Context Windows Deep Dive

- **Channel:** Weights & Biases
- **Year:** 2024
- **Duration:** ~40 minutes
- **Level:** 🔴
- **Link:** [youtube.com/watch?v=cW8bkMH0psI](https://www.youtube.com/watch?v=cW8bkMH0psI)

**Key Takeaways:**
- Technical deep dive into context window internals
- KV-cache management and memory requirements
- How different models handle long context differently
- Benchmarking context utilization across models

---

### 22. Chunking Strategies for RAG

- **Channel:** Greg Kamradt
- **Year:** 2023
- **Duration:** ~30 minutes
- **Level:** 🟡
- **Link:** [youtube.com/watch?v=8OJC21T2SL4](https://www.youtube.com/watch?v=8OJC21T2SL4)

**Key Takeaways:**
- Comprehensive comparison of chunking strategies
- Fixed-size, sentence-based, semantic, and recursive chunking
- Impact of chunk size on retrieval quality
- Practical recommendations for different document types

---

## Suggested Viewing Order

### For Beginners (Start Here)

1. Intro to Large Language Models (Karpathy) — 🟢
2. But What Is a GPT? (3Blue1Brown) — 🟢
3. How ChatGPT Works Technically (ByteByteGo) — 🟢
4. Vector Databases Explained (Fireship) — 🟢
5. Prompt Engineering Full Course (freeCodeCamp) — 🟢

### For Intermediate Learners

6. Visualizing Attention (3Blue1Brown) — 🟢
7. Attention Is All You Need Explained (Kilcher) — 🟡
8. RAG from Scratch (LangChain) — 🟡
9. Context Engineering for AI Agents (AI Jason) — 🟡
10. Chunking Strategies for RAG (Kamradt) — 🟡

### For Advanced Practitioners

11. Let's Build GPT (Karpathy) — 🔴
12. Advanced RAG Techniques (DeepLearning.AI) — 🟡
13. DSPy Explained (Shorten) — 🟡
14. Building Production RAG (AI Engineer) — 🔴
15. Stanford CS25 — Transformers United — 🔴

---

<div align="center">

**[Back to Main Guide](../README.md)**

</div>
