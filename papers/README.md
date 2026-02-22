<div align="center">

# 📚 Research Papers on Context Engineering

*A comprehensive, annotated bibliography of key research papers*

[Back to Main Guide](../README.md)

</div>

---

## How to Use This List

Each paper includes:
- **Full citation** with link to the paper
- **Abstract summary** (2-3 sentences)
- **Key contribution** badge
- **Relevance** to context engineering
- **Difficulty level**: 🟢 Beginner | 🟡 Intermediate | 🔴 Advanced

---

## 1. Context Window & Long Context

### 1.1 Lost in the Middle: How Language Models Use Long Contexts

- **Authors:** Nelson F. Liu, Kevin Lin, John Hewitt, Ashwin Paranjape, Michele Bevilacqua, Fabio Petroni, Percy Liang
- **Year:** 2023
- **Link:** [arXiv:2307.03172](https://arxiv.org/abs/2307.03172)
- **Badge:** ![Foundational](https://img.shields.io/badge/-Foundational-red)
- **Level:** 🟡

**Summary:** Demonstrates that language models struggle to use information in the middle of long contexts. Performance is highest when relevant information is placed at the very beginning or end of the input. This has major implications for how we order information in context windows.

**Key Insight for Context Engineering:** Always place the most critical information at the beginning or end of the context window. Avoid placing essential data in the middle of long prompts.

---

### 1.2 Extending Context Window of Large Language Models via Positional Interpolation

- **Authors:** Shouyuan Chen, Sherman Wong, Liangjian Chen, Yuandong Tian
- **Year:** 2023
- **Link:** [arXiv:2306.15595](https://arxiv.org/abs/2306.15595)
- **Badge:** ![Method](https://img.shields.io/badge/-Method-blue)
- **Level:** 🔴

**Summary:** Proposes Position Interpolation (PI) to extend the context window of RoPE-based LLMs. Instead of extrapolating position encodings beyond training length, PI downscales position indices to fit within the original range, then fine-tunes briefly. Extends LLaMA to 32K tokens with minimal quality loss.

**Key Insight for Context Engineering:** Context window extension is possible post-training through positional encoding modifications, enabling models to handle longer contexts without training from scratch.

---

### 1.3 LongRoPE: Extending LLM Context Window Beyond 2 Million Tokens

- **Authors:** Yiran Ding, Li Lyna Zhang, Chengruidong Zhang, Yuanyuan Xu, Ning Shang, Jiahang Xu, Fan Yang, Mao Yang
- **Year:** 2024
- **Link:** [arXiv:2402.13753](https://arxiv.org/abs/2402.13753)
- **Badge:** ![Scaling](https://img.shields.io/badge/-Scaling-purple)
- **Level:** 🔴

**Summary:** Introduces a progressive extension strategy to push context windows beyond 2 million tokens. Uses non-uniform positional interpolation and a search algorithm to find optimal rescaling factors. Demonstrates effective long-context performance at extreme lengths.

**Key Insight for Context Engineering:** Extreme context lengths (millions of tokens) are technically achievable, but effective utilization of that context remains an open challenge.

---

### 1.4 Ring Attention with Blockwise Transformers for Near-Infinite Context

- **Authors:** Hao Liu, Matei Zaharia, Pieter Abbeel
- **Year:** 2023
- **Link:** [arXiv:2310.01889](https://arxiv.org/abs/2310.01889)
- **Badge:** ![Infrastructure](https://img.shields.io/badge/-Infrastructure-orange)
- **Level:** 🔴

**Summary:** Proposes Ring Attention, which distributes long sequences across multiple devices in a ring topology. Each device processes a block of the sequence while communicating key-value blocks with neighbors. Enables processing of sequences that are orders of magnitude longer than a single device's memory.

**Key Insight for Context Engineering:** Infrastructure-level solutions like Ring Attention enable the scaling of context windows beyond single-device memory limits.

---

### 1.5 YaRN: Efficient Context Window Extension of Large Language Models

- **Authors:** Bowen Peng, Jeffrey Quesnelle, Honglu Fan, Enrico Shippole
- **Year:** 2023
- **Link:** [arXiv:2309.00071](https://arxiv.org/abs/2309.00071)
- **Badge:** ![Method](https://img.shields.io/badge/-Method-blue)
- **Level:** 🔴

**Summary:** Introduces Yet another RoPE extensioN method (YaRN), which combines NTK-aware interpolation with attention scaling. Achieves superior performance over previous methods like PI and NTK-aware scaling. Extends LLaMA 2 to 128K context with only 400 training steps.

**Key Insight for Context Engineering:** RoPE-based extensions offer efficient ways to expand context windows. YaRN shows that careful interpolation design can dramatically reduce the fine-tuning needed for context extension.

---

### 1.6 Effective Long-Context Scaling of Foundation Models

- **Authors:** Wenhan Xiong, Jingyu Liu, Igor Molybog, Hejia Zhang, Prajjwal Bhargava, Rui Hou, Louis Martin, Rashi Rungta, Karthik Abinav Sankararaman, Barlas Oguz, et al.
- **Year:** 2023
- **Link:** [arXiv:2309.16039](https://arxiv.org/abs/2309.16039)
- **Badge:** ![Scaling](https://img.shields.io/badge/-Scaling-purple)
- **Level:** 🔴

**Summary:** Meta's approach to training long-context LLMs from the ground up. Introduces a continual pretraining recipe using long text data to extend Llama 2 to 32K tokens. Provides insights on data mixing, curriculum learning, and evaluation for long-context models.

**Key Insight for Context Engineering:** Long-context capability requires careful data curation during pretraining, not just architectural changes.

---

### 1.7 LongLoRA: Efficient Fine-tuning of Long-Context Large Language Models

- **Authors:** Yukang Chen, Shengju Qian, Haotian Tang, Xin Lai, Zhijian Liu, Song Han, Jiaya Jia
- **Year:** 2023
- **Link:** [arXiv:2309.12307](https://arxiv.org/abs/2309.12307)
- **Badge:** ![Efficiency](https://img.shields.io/badge/-Efficiency-green)
- **Level:** 🔴

**Summary:** Proposes an efficient method for extending context window during fine-tuning using shifted sparse attention. Reduces computational cost while maintaining performance. Demonstrates that long-context fine-tuning does not require full attention patterns during training.

**Key Insight for Context Engineering:** Efficient attention patterns during training can dramatically reduce the cost of building long-context models.

---

### 1.8 RULER: What's the Real Context Size of Your Long-Context Language Model?

- **Authors:** Cheng-Ping Hsieh, Simeng Sun, Samuel Kriman, Shantanu Acharya, Dima Rekesh, Fei Jia, Boris Ginsburg
- **Year:** 2024
- **Link:** [arXiv:2404.06654](https://arxiv.org/abs/2404.06654)
- **Badge:** ![Benchmark](https://img.shields.io/badge/-Benchmark-yellow)
- **Level:** 🟡

**Summary:** Introduces RULER, a comprehensive benchmark for evaluating long-context LLMs beyond simple needle-in-a-haystack tests. Tests retrieval, multi-hop reasoning, aggregation, and question answering at various context lengths. Reveals that many models claiming large context windows perform poorly at longer lengths.

**Key Insight for Context Engineering:** Stated context window size and effective context utilization are very different things. Always evaluate empirically for your use case.

---

### 1.9 Leave No Context Behind: Efficient Infinite Context Transformers with Infini-attention

- **Authors:** Tsendsuren Munkhdalai, Manaal Faruqui, Siddharth Gopal
- **Year:** 2024
- **Link:** [arXiv:2404.07143](https://arxiv.org/abs/2404.07143)
- **Badge:** ![Architecture](https://img.shields.io/badge/-Architecture-teal)
- **Level:** 🔴

**Summary:** Proposes Infini-attention, which combines compressive memory with standard attention. Allows processing of infinitely long sequences by storing compressed representations of past context. The model can attend to both local context (via standard attention) and global context (via compressive memory).

**Key Insight for Context Engineering:** Hybrid attention mechanisms that combine local and global context may be the key to truly unbounded context processing.

---

### 1.10 Data Engineering for Scaling Language Models to 128K Context

- **Authors:** Yao Fu, Rameswar Panda, Xinyao Niu, Xiang Yue, Hanna Hajishirzi, Yoon Kim, Hao Peng
- **Year:** 2024
- **Link:** [arXiv:2402.10171](https://arxiv.org/abs/2402.10171)
- **Badge:** ![Data](https://img.shields.io/badge/-Data-brown)
- **Level:** 🔴

**Summary:** Studies the data engineering aspects of long-context training. Identifies that data quality and diversity are more important than sheer volume for long-context performance. Provides practical recipes for curating long-context training data.

**Key Insight for Context Engineering:** The quality of long-context training data is paramount. Well-curated datasets of moderate size outperform massive but noisy datasets.

---

## 2. Retrieval-Augmented Generation (RAG)

### 2.1 Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks

- **Authors:** Patrick Lewis, Ethan Perez, Aleksandra Piktus, Fabio Petroni, Vladimir Karpukhin, Naman Goyal, Heinrich Kuttler, Mike Lewis, Wen-tau Yih, Tim Rocktaschel, Sebastian Riedel, Douwe Kiela
- **Year:** 2020
- **Link:** [arXiv:2005.11401](https://arxiv.org/abs/2005.11401)
- **Badge:** ![Foundational](https://img.shields.io/badge/-Foundational-red)
- **Level:** 🟡

**Summary:** The seminal RAG paper. Proposes combining a pre-trained retriever (DPR) with a pre-trained generator (BART) and fine-tuning end-to-end. Demonstrates that RAG models outperform purely parametric models on knowledge-intensive tasks like open-domain QA.

**Key Insight for Context Engineering:** RAG established the paradigm of augmenting LLMs with external retrieval, enabling access to knowledge beyond the model's training data.

---

### 2.2 Self-RAG: Learning to Retrieve, Generate, and Critique Through Self-Reflection

- **Authors:** Akari Asai, Zeqiu Wu, Yizhong Wang, Avirup Sil, Hannaneh Hajishirzi
- **Year:** 2023
- **Link:** [arXiv:2310.11511](https://arxiv.org/abs/2310.11511)
- **Badge:** ![Method](https://img.shields.io/badge/-Method-blue)
- **Level:** 🔴

**Summary:** Introduces Self-RAG, where the LLM learns to adaptively retrieve, generate, and critique its own outputs using special reflection tokens. The model decides when retrieval is needed and evaluates the relevance and support of retrieved passages for its generation.

**Key Insight for Context Engineering:** Models can learn to manage their own context by deciding when to retrieve and evaluating retrieved content quality.

---

### 2.3 RAPTOR: Recursive Abstractive Processing for Tree-Organized Retrieval

- **Authors:** Parth Sarthi, Salman Abdullah, Aditi Tuli, Shubh Khanna, Anna Goldie, Christopher D. Manning
- **Year:** 2024
- **Link:** [arXiv:2401.18059](https://arxiv.org/abs/2401.18059)
- **Badge:** ![Architecture](https://img.shields.io/badge/-Architecture-teal)
- **Level:** 🟡

**Summary:** Proposes a tree-based retrieval structure where documents are recursively summarized into a hierarchical tree. Retrieval can operate at different levels of abstraction: detailed chunks at the leaves, summaries at intermediate nodes, and high-level themes at the root.

**Key Insight for Context Engineering:** Hierarchical indexing structures enable retrieval at multiple levels of abstraction, supporting both detailed and thematic queries.

---

### 2.4 Corrective Retrieval-Augmented Generation (CRAG)

- **Authors:** Shi-Qi Yan, Jia-Chen Gu, Yun Zhu, Zhen-Hua Ling
- **Year:** 2024
- **Link:** [arXiv:2401.15884](https://arxiv.org/abs/2401.15884)
- **Badge:** ![Method](https://img.shields.io/badge/-Method-blue)
- **Level:** 🟡

**Summary:** Addresses the problem of noisy or irrelevant retrievals in RAG. CRAG uses a lightweight retrieval evaluator to assess document quality and triggers corrective actions: if retrieved documents are ambiguous, it refines the query; if irrelevant, it falls back to web search.

**Key Insight for Context Engineering:** Not all retrieved context is helpful. Systems need mechanisms to evaluate and correct poor retrievals before they contaminate generation.

---

### 2.5 Active Retrieval Augmented Generation (FLARE)

- **Authors:** Zhengbao Jiang, Frank F. Xu, Luyu Gao, Zhiqing Sun, Qian Liu, Jane Dwivedi-Yu, Yiming Yang, Jamie Callan, Graham Neubig
- **Year:** 2023
- **Link:** [arXiv:2305.06983](https://arxiv.org/abs/2305.06983)
- **Badge:** ![Method](https://img.shields.io/badge/-Method-blue)
- **Level:** 🟡

**Summary:** Proposes Forward-Looking Active REtrieval (FLARE), where the model iteratively generates text and actively decides when and what to retrieve. When the model detects low confidence in its next generation, it formulates a retrieval query based on the upcoming content it anticipates needing.

**Key Insight for Context Engineering:** Retrieval should be interleaved with generation, not just performed once upfront. Active retrieval adapts the context dynamically during generation.

---

### 2.6 Dense Passage Retrieval for Open-Domain Question Answering

- **Authors:** Vladimir Karpukhin, Barlas Oguz, Sewon Min, Patrick Lewis, Ledell Wu, Sergey Edunov, Danqi Chen, Wen-tau Yih
- **Year:** 2020
- **Link:** [arXiv:2004.04906](https://arxiv.org/abs/2004.04906)
- **Badge:** ![Foundational](https://img.shields.io/badge/-Foundational-red)
- **Level:** 🟡

**Summary:** Introduced Dense Passage Retrieval (DPR), which uses dual BERT encoders for question and passage encoding. DPR outperformed BM25 and other sparse retrieval methods on multiple open-domain QA benchmarks, establishing dense retrieval as the standard.

**Key Insight for Context Engineering:** Dense (learned) retrieval representations are superior to sparse (keyword) methods for semantic matching, forming the basis of modern RAG.

---

### 2.7 ColBERT: Efficient and Effective Passage Search via Contextualized Late Interaction over BERT

- **Authors:** Omar Khattab, Matei Zaharia
- **Year:** 2020
- **Link:** [arXiv:2004.12832](https://arxiv.org/abs/2004.12832)
- **Badge:** ![Efficiency](https://img.shields.io/badge/-Efficiency-green)
- **Level:** 🔴

**Summary:** Introduces late interaction for efficient retrieval. Rather than computing a single vector per document, ColBERT encodes tokens independently and performs a MaxSim late interaction. Offers a strong balance of effectiveness and efficiency.

**Key Insight for Context Engineering:** Late interaction models like ColBERT provide near-cross-encoder quality with near-bi-encoder speed, making them ideal for production RAG systems.

---

### 2.8 Adaptive-RAG: Learning to Adapt Retrieval-Augmented Large Language Models through Question Complexity

- **Authors:** Soyeong Jeong, Jinheon Baek, Sukmin Cho, Sung Ju Hwang, Jong C. Park
- **Year:** 2024
- **Link:** [arXiv:2403.14403](https://arxiv.org/abs/2403.14403)
- **Badge:** ![Method](https://img.shields.io/badge/-Method-blue)
- **Level:** 🟡

**Summary:** Proposes a routing mechanism that classifies queries by complexity and routes them to different retrieval strategies. Simple queries may not need retrieval at all, moderate queries use single-step RAG, and complex queries use multi-step retrieval with iterative refinement.

**Key Insight for Context Engineering:** Not all queries benefit from retrieval. Adaptive systems that route based on query complexity are more efficient and can be more accurate.

---

### 2.9 Seven Failure Points When Engineering a Retrieval Augmented Generation System

- **Authors:** Scott Barnett, Stefanus Kurniawan, Srikanth Thudumu, Zach Brannelly, Mohamed Abdelrazek
- **Year:** 2024
- **Link:** [arXiv:2401.05856](https://arxiv.org/abs/2401.05856)
- **Badge:** ![Survey](https://img.shields.io/badge/-Survey-grey)
- **Level:** 🟡

**Summary:** Identifies seven common failure points in production RAG systems: missing content, missed top-ranked documents, not in context (context limit), not extracted, wrong format, incorrect specificity, and incomplete responses. Provides practical mitigation strategies for each.

**Key Insight for Context Engineering:** Understanding where RAG systems fail is critical. This taxonomy provides an actionable checklist for debugging and improving RAG pipelines.

---

### 2.10 A Survey on Retrieval-Augmented Generation Meets Large Language Models

- **Authors:** Yujuan Fan, Yikai Zhang, Jinfeng Wang, et al.
- **Year:** 2024
- **Link:** [arXiv:2405.06211](https://arxiv.org/abs/2405.06211)
- **Badge:** ![Survey](https://img.shields.io/badge/-Survey-grey)
- **Level:** 🟡

**Summary:** Comprehensive survey covering the RAG landscape as of 2024, including retrieval models, generation models, augmentation strategies, and evaluation methods. Categorizes RAG approaches into naive, advanced, and modular paradigms.

**Key Insight for Context Engineering:** This survey provides a unified taxonomy and overview of the rapidly evolving RAG landscape.

---

## 3. Prompt Engineering & Optimization

### 3.1 Chain-of-Thought Prompting Elicits Reasoning in Large Language Models

- **Authors:** Jason Wei, Xuezhi Wang, Dale Schuurmans, Maarten Bosma, Brian Ichter, Fei Xia, Ed Chi, Quoc Le, Denny Zhou
- **Year:** 2022
- **Link:** [arXiv:2201.11903](https://arxiv.org/abs/2201.11903)
- **Badge:** ![Foundational](https://img.shields.io/badge/-Foundational-red)
- **Level:** 🟢

**Summary:** Demonstrates that including intermediate reasoning steps ("chain of thought") in few-shot examples dramatically improves LLM performance on reasoning tasks. A simple prompting technique that requires no model modification.

**Key Insight for Context Engineering:** The structure and content of few-shot examples in the context window directly impacts reasoning quality. CoT shows that context engineering is about what information to include, not just what question to ask.

---

### 3.2 Tree of Thoughts: Deliberate Problem Solving with Large Language Models

- **Authors:** Shunyu Yao, Dian Yu, Jeffrey Zhao, Izhak Shafran, Tom Griffiths, Yuan Cao, Karthik Narasimhan
- **Year:** 2023
- **Link:** [arXiv:2305.10601](https://arxiv.org/abs/2305.10601)
- **Badge:** ![Method](https://img.shields.io/badge/-Method-blue)
- **Level:** 🟡

**Summary:** Extends chain-of-thought to a tree structure where the model can explore multiple reasoning paths, evaluate intermediate states, and backtrack. Frames LLM inference as search over a reasoning tree.

**Key Insight for Context Engineering:** Context can be used not just for one-shot generation but for structured exploration of solution spaces. Context management becomes critical when maintaining multiple reasoning branches.

---

### 3.3 DSPy: Compiling Declarative Language Model Calls into Self-Improving Pipelines

- **Authors:** Omar Khattab, Arnav Singhvi, Paridhi Maheshwari, Zhiyuan Zhang, Keshav Santhanam, Sri Vardhamanan, Saiful Haq, Ashutosh Sharma, Thomas T. Joshi, Hanna Moazam, Heather Miller, Matei Zaharia, Christopher Potts
- **Year:** 2023
- **Link:** [arXiv:2310.03714](https://arxiv.org/abs/2310.03714)
- **Badge:** ![Framework](https://img.shields.io/badge/-Framework-cyan)
- **Level:** 🔴

**Summary:** Introduces DSPy, a framework that replaces hand-written prompts with declarative modules and optimizes them through compilation. DSPy programs define signatures (input/output types) and the compiler automatically generates effective prompts through few-shot bootstrapping.

**Key Insight for Context Engineering:** Context engineering can be automated. DSPy demonstrates that programmatic optimization of prompts and few-shot examples outperforms manual engineering.

---

### 3.4 Automatic Prompt Optimization with Gradient Descent and Beam Search

- **Authors:** Reid Pryzant, Dan Iter, Jerry Li, Yin Tat Lee, Chenguang Zhu, Michael Zeng
- **Year:** 2023
- **Link:** [arXiv:2305.03495](https://arxiv.org/abs/2305.03495)
- **Badge:** ![Method](https://img.shields.io/badge/-Method-blue)
- **Level:** 🔴

**Summary:** Proposes using "textual gradients" (natural language feedback on prompt failures) to iteratively optimize prompts. The LLM generates candidate improvements based on error analysis, and beam search selects the best variants.

**Key Insight for Context Engineering:** Prompts (and by extension, context) can be optimized using search-based methods, moving beyond human intuition to systematic optimization.

---

### 3.5 Large Language Models Are Human-Level Prompt Engineers

- **Authors:** Yongchao Zhou, Andrei Ioan Muresanu, Ziwen Han, Keiran Paster, Silviu Pitis, Harris Chan, Jimmy Ba
- **Year:** 2022
- **Link:** [arXiv:2211.01910](https://arxiv.org/abs/2211.01910)
- **Badge:** ![Method](https://img.shields.io/badge/-Method-blue)
- **Level:** 🟡

**Summary:** Introduces Automatic Prompt Engineer (APE), which uses LLMs to generate and select effective prompts. Given a task description and examples, APE generates candidate prompts, evaluates them, and selects the best-performing one.

**Key Insight for Context Engineering:** LLMs themselves can serve as tools for optimizing the context provided to other LLMs, creating a meta-optimization loop.

---

### 3.6 Principled Instructions Are All You Need for Questioning LLaMA-1/2, GPT-3.5/4

- **Authors:** Sondos Mahmoud Bsharat, Aidar Myrzakhan, Zhiqiang Shen
- **Year:** 2023
- **Link:** [arXiv:2312.16171](https://arxiv.org/abs/2312.16171)
- **Badge:** ![Guidelines](https://img.shields.io/badge/-Guidelines-pink)
- **Level:** 🟢

**Summary:** Provides 26 empirically validated principles for effective prompting. Principles range from simple formatting tips (use affirmative language) to structural guidelines (assign a role, break down complex tasks). Each principle is tested across multiple models.

**Key Insight for Context Engineering:** Concrete, empirically tested principles for prompt construction provide a foundation for systematic context engineering.

---

### 3.7 Graph of Thoughts: Solving Elaborate Problems with Large Language Models

- **Authors:** Maciej Besta, Nils Blach, Ales Kubicek, Robert Gerstenberger, Lukas Gianinazzi, Joanna Gajda, Tomasz Lehmann, Michal Podstawski, Hubert Niewiadomski, Piotr Nyczyk, Torsten Hoefler
- **Year:** 2023
- **Link:** [arXiv:2308.09687](https://arxiv.org/abs/2308.09687)
- **Badge:** ![Method](https://img.shields.io/badge/-Method-blue)
- **Level:** 🔴

**Summary:** Extends Tree of Thoughts to a graph structure where reasoning steps can be combined, refined, and form loops. Enables more complex reasoning patterns like merging intermediate results from different branches.

**Key Insight for Context Engineering:** Complex problem-solving requires flexible context management that supports branching, merging, and iterative refinement of reasoning chains.

---

## 4. Memory & Context Management

### 4.1 MemGPT: Towards LLMs as Operating Systems

- **Authors:** Charles Packer, Sarah Wooders, Kevin Lin, Vivian Fang, Shishir G. Patil, Ion Stoica, Joseph E. Gonzalez
- **Year:** 2023
- **Link:** [arXiv:2310.08560](https://arxiv.org/abs/2310.08560)
- **Badge:** ![Architecture](https://img.shields.io/badge/-Architecture-teal)
- **Level:** 🟡

**Summary:** Draws an analogy between LLM context management and operating system memory management. Introduces a hierarchical memory system with main context (limited), archival storage (unlimited), and recall storage (conversational). The LLM learns to manage its own context through function calls.

**Key Insight for Context Engineering:** The OS memory hierarchy (registers, cache, RAM, disk) maps directly to LLM context management. Virtual context management enables unbounded conversations and knowledge.

---

### 4.2 Reflexion: Language Agents with Verbal Reinforcement Learning

- **Authors:** Noah Shinn, Federico Cassano, Ashwin Gopinath, Karthik Narasimhan, Shunyu Yao
- **Year:** 2023
- **Link:** [arXiv:2303.11366](https://arxiv.org/abs/2303.11366)
- **Badge:** ![Agents](https://img.shields.io/badge/-Agents-violet)
- **Level:** 🟡

**Summary:** Proposes Reflexion, where language agents learn from failures by generating verbal self-reflections that are stored in an episodic memory buffer. These reflections are included in future context windows, enabling the agent to avoid repeating mistakes without weight updates.

**Key Insight for Context Engineering:** Context can serve as a learning mechanism. By including self-reflections in the context window, agents improve over time without fine-tuning.

---

### 4.3 LLMLingua: Compressing Prompts for Accelerated Inference of Large Language Models

- **Authors:** Huiqiang Jiang, Qianhui Wu, Chin-Yew Lin, Yuqing Yang, Lili Qiu
- **Year:** 2023
- **Link:** [arXiv:2310.05736](https://arxiv.org/abs/2310.05736)
- **Badge:** ![Compression](https://img.shields.io/badge/-Compression-darkgreen)
- **Level:** 🟡

**Summary:** Uses a small language model to compute token-level perplexity and removes low-information tokens from prompts. Achieves up to 20x compression with minimal quality loss. Includes iterative token pruning and budget-aware allocation across prompt components.

**Key Insight for Context Engineering:** Not all tokens in a prompt are equally important. Token-level compression can dramatically reduce costs while preserving performance, a core context engineering optimization.

---

### 4.4 Voyager: An Open-Ended Embodied Agent with Large Language Models

- **Authors:** Guanzhi Wang, Yuqi Xie, Yunfan Jiang, Ajay Mandlekar, Chaowei Xiao, Yuke Zhu, Linxi Fan, Anima Anandkumar
- **Year:** 2023
- **Link:** [arXiv:2305.16291](https://arxiv.org/abs/2305.16291)
- **Badge:** ![Agents](https://img.shields.io/badge/-Agents-violet)
- **Level:** 🔴

**Summary:** An embodied LLM agent that explores, learns, and stores skills as code in a skill library (Minecraft). Voyager dynamically retrieves relevant skills from its library to include in the context window for new tasks.

**Key Insight for Context Engineering:** Skill/code libraries function as a form of long-term context. Dynamic retrieval of relevant past solutions is a powerful pattern for agentic systems.

---

### 4.5 Cognitive Architectures for Language Agents

- **Authors:** Theodore R. Sumers, Shunyu Yao, Karthik Narasimhan, Thomas L. Griffiths
- **Year:** 2023
- **Link:** [arXiv:2309.02427](https://arxiv.org/abs/2309.02427)
- **Badge:** ![Survey](https://img.shields.io/badge/-Survey-grey)
- **Level:** 🟡

**Summary:** Proposes a systematic framework for designing language agents based on cognitive science. The framework includes perception (input processing), memory (working, episodic, semantic, procedural), action (tool use, generation), and decision-making (planning, reflection).

**Key Insight for Context Engineering:** Cognitive science provides principled frameworks for designing context management systems. Different types of memory serve different functions in agent architectures.

---

### 4.6 Augmenting Language Models with Long-Term Memory (LongMem)

- **Authors:** Weizhi Wang, Li Dong, Hao Cheng, Xiaodong Liu, Xifeng Yan, Jianfeng Gao, Furu Wei
- **Year:** 2023
- **Link:** [arXiv:2306.07174](https://arxiv.org/abs/2306.07174)
- **Badge:** ![Architecture](https://img.shields.io/badge/-Architecture-teal)
- **Level:** 🔴

**Summary:** Proposes a decoupled architecture where a frozen backbone LLM is augmented with a trainable side network that accesses a long-term memory bank. The memory bank stores key-value pairs from past contexts, enabling the model to access information far beyond its context window.

**Key Insight for Context Engineering:** Decoupled memory architectures can extend effective context without modifying the base model, making this applicable to any LLM.

---

### 4.7 Walking Down the Memory Maze: Beyond Context Limit through Interactive Reading

- **Authors:** Howard Chen, Ramakanth Pasunuru, Jason Weston, Asli Celikyilmaz
- **Year:** 2023
- **Link:** [arXiv:2310.05029](https://arxiv.org/abs/2310.05029)
- **Badge:** ![Method](https://img.shields.io/badge/-Method-blue)
- **Level:** 🔴

**Summary:** Proposes an interactive reading approach where the model processes long documents in segments, building a structured memory as it reads. The model can revisit earlier segments based on questions that arise during reading, mimicking how humans read complex documents.

**Key Insight for Context Engineering:** Interactive, multi-pass reading strategies can overcome context limits by building structured representations during incremental processing.

---

<div align="center">

**[Back to Main Guide](../README.md)**

</div>
