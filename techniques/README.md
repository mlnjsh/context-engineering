<div align="center">

# 📊 Context Engineering Techniques & Patterns

*Deep dive into the core techniques with pseudo-code examples and implementation guidance*

[Back to Main Guide](../README.md)

</div>

---

## Table of Contents

1. [Chunking Strategies](#1-chunking-strategies)
2. [Retrieval Patterns](#2-retrieval-patterns)
3. [Context Compression](#3-context-compression)
4. [Context Caching](#4-context-caching)
5. [Sliding Window Attention](#5-sliding-window-attention)
6. [Multi-hop Reasoning](#6-multi-hop-reasoning)
7. [Few-shot Learning Optimization](#7-few-shot-learning-optimization)
8. [System Prompt Engineering](#8-system-prompt-engineering)
9. [Token Budget Management](#9-token-budget-management)
10. [Information Ordering](#10-information-ordering)

---

## 1. Chunking Strategies

Chunking determines how documents are split before embedding and retrieval. The quality of your chunks directly determines the quality of your retrieval and, ultimately, your LLM's answers.

### Fixed-Size Chunking

Split documents into chunks of a fixed number of tokens/characters, with optional overlap.

```python
# Pseudo-code: Fixed-Size Chunking
def fixed_size_chunk(text, chunk_size=512, overlap=50):
    tokens = tokenize(text)
    chunks = []
    for i in range(0, len(tokens), chunk_size - overlap):
        chunk = tokens[i : i + chunk_size]
        chunks.append(detokenize(chunk))
    return chunks
```

| Pros | Cons |
|:-----|:-----|
| Simple to implement | Breaks semantic boundaries |
| Predictable chunk sizes | May split sentences/paragraphs |
| Easy to reason about token budgets | Overlap wastes tokens |

**Best For:** Homogeneous text, initial prototyping.

---

### Semantic Chunking

Split documents based on semantic similarity between consecutive sentences. When similarity drops below a threshold, a new chunk begins.

```python
# Pseudo-code: Semantic Chunking
def semantic_chunk(text, threshold=0.5):
    sentences = split_into_sentences(text)
    embeddings = embed(sentences)
    chunks = []
    current_chunk = [sentences[0]]

    for i in range(1, len(sentences)):
        similarity = cosine_similarity(embeddings[i-1], embeddings[i])
        if similarity < threshold:
            chunks.append(" ".join(current_chunk))
            current_chunk = [sentences[i]]
        else:
            current_chunk.append(sentences[i])

    chunks.append(" ".join(current_chunk))
    return chunks
```

| Pros | Cons |
|:-----|:-----|
| Preserves semantic coherence | More expensive (requires embeddings) |
| Better retrieval quality | Variable chunk sizes |
| Topic-aware boundaries | Threshold tuning needed |

**Best For:** Long documents with multiple topics, when retrieval quality is paramount.

---

### Recursive Character Splitting

Try to split on larger structural boundaries first (paragraphs), then sentences, then words. This preserves document structure while ensuring chunks fit within size limits.

```python
# Pseudo-code: Recursive Splitting
def recursive_split(text, max_size=512, separators=["\n\n", "\n", ". ", " "]):
    if len(tokenize(text)) <= max_size:
        return [text]

    # Try each separator in order of preference
    for sep in separators:
        parts = text.split(sep)
        if len(parts) > 1:
            chunks = []
            current = ""
            for part in parts:
                candidate = current + sep + part if current else part
                if len(tokenize(candidate)) > max_size:
                    if current:
                        chunks.append(current)
                    current = part
                else:
                    current = candidate
            if current:
                chunks.append(current)
            return chunks

    # Fallback: hard split
    return fixed_size_chunk(text, max_size)
```

| Pros | Cons |
|:-----|:-----|
| Respects document structure | More complex logic |
| Adaptive to content | May produce uneven chunks |
| Good default choice | Separator list needs tuning per format |

**Best For:** General-purpose chunking, structured documents (Markdown, HTML, code).

---

### Document-Aware Chunking

Split based on document structure: headers, sections, code blocks, tables.

```python
# Pseudo-code: Document-Aware Chunking (Markdown)
def markdown_chunk(text, max_size=512):
    sections = split_by_headers(text)  # Split on # ## ###
    chunks = []
    for section in sections:
        header = section["header"]
        body = section["body"]
        if len(tokenize(header + body)) <= max_size:
            chunks.append({"text": header + "\n" + body, "metadata": {"header": header}})
        else:
            sub_chunks = recursive_split(body, max_size)
            for sc in sub_chunks:
                chunks.append({"text": header + "\n" + sc, "metadata": {"header": header}})
    return chunks
```

**Best For:** Structured documents (docs, wikis, codebases).

---

### Chunking Decision Tree

```
What type of document are you chunking?
│
├── Structured (Markdown, HTML, code)
│   └── Use document-aware chunking
│       └── Fallback to recursive splitting for large sections
│
├── Long-form prose (articles, books)
│   └── Use semantic chunking
│       └── Fallback to sentence-level splitting
│
├── Short documents (<1000 tokens)
│   └── Do not chunk — embed the whole document
│
├── Mixed content (tables + text + images)
│   └── Split by content type first, then chunk each type
│
└── Unknown / prototyping
    └── Start with recursive character splitting (chunk_size=512, overlap=50)
```

---

## 2. Retrieval Patterns

### Naive RAG

The simplest RAG pattern: embed the query, retrieve top-k chunks, concatenate into context, generate.

```python
# Pseudo-code: Naive RAG
def naive_rag(query, knowledge_base, llm, k=5):
    # Step 1: Embed the query
    query_embedding = embed(query)

    # Step 2: Retrieve top-k similar chunks
    results = knowledge_base.similarity_search(query_embedding, k=k)

    # Step 3: Build context
    context = "\n\n".join([r.text for r in results])

    # Step 4: Generate
    prompt = f"""Answer the question based on the context below.

Context:
{context}

Question: {query}

Answer:"""

    return llm.generate(prompt)
```

**Limitations:** No query refinement, no relevance filtering, sensitive to chunk quality.

---

### Advanced RAG

Adds query transformation, hybrid search, reranking, and post-processing.

```python
# Pseudo-code: Advanced RAG Pipeline
def advanced_rag(query, knowledge_base, llm, k=20, top_n=5):
    # Step 1: Query transformation
    expanded_query = llm.generate(f"Rewrite this query for better search: {query}")
    hypothetical_doc = llm.generate(f"Write a passage that would answer: {query}")  # HyDE

    # Step 2: Hybrid retrieval
    dense_results = knowledge_base.dense_search(embed(expanded_query), k=k)
    sparse_results = knowledge_base.bm25_search(query, k=k)
    hyde_results = knowledge_base.dense_search(embed(hypothetical_doc), k=k)

    # Step 3: Fusion and deduplication
    all_results = reciprocal_rank_fusion(dense_results, sparse_results, hyde_results)

    # Step 4: Reranking
    reranked = reranker.rank(query, all_results)[:top_n]

    # Step 5: Context compression (optional)
    compressed_context = compress(query, reranked)

    # Step 6: Generate with citation
    prompt = f"""Answer the question based on the sources below. Cite sources by number.

Sources:
{format_sources(compressed_context)}

Question: {query}

Answer:"""

    return llm.generate(prompt)
```

---

### Agentic RAG

The LLM decides when and what to retrieve, can reformulate queries, and iterates.

```python
# Pseudo-code: Agentic RAG (CRAG-style)
def agentic_rag(query, knowledge_base, llm, max_iterations=3):
    context = []

    for iteration in range(max_iterations):
        # Retrieve
        results = knowledge_base.search(query, k=5)

        # Evaluate relevance
        evaluation = llm.generate(
            f"Are these results relevant to '{query}'? "
            f"Rate: CORRECT / AMBIGUOUS / INCORRECT\n{results}"
        )

        if "CORRECT" in evaluation:
            context.extend(results)
            break
        elif "AMBIGUOUS" in evaluation:
            # Refine and add partial results
            context.extend([r for r in results if is_relevant(r, query)])
            query = llm.generate(f"Refine this query for better results: {query}")
        else:  # INCORRECT
            # Fall back to web search or query reformulation
            query = llm.generate(f"Completely rewrite this query: {query}")
            web_results = web_search(query)
            context.extend(web_results)
            break

    # Generate final answer
    return llm.generate(build_prompt(query, context))
```

---

### RAG Pattern Comparison

| Pattern | Quality | Latency | Cost | Complexity |
|:--------|:-------:|:-------:|:----:|:----------:|
| Naive RAG | Low-Medium | Low | Low | Low |
| Advanced RAG | High | Medium | Medium | Medium |
| Agentic RAG | Highest | High | High | High |
| Modular RAG | High | Variable | Variable | High |

---

## 3. Context Compression

### Extractive Compression

Select only the most relevant sentences from retrieved documents.

```python
# Pseudo-code: Extractive Context Compression
def extractive_compress(query, documents, max_tokens=2000):
    all_sentences = []
    for doc in documents:
        sentences = split_into_sentences(doc.text)
        for sent in sentences:
            score = relevance_score(query, sent)
            all_sentences.append((sent, score, doc.source))

    # Sort by relevance and select top sentences within budget
    all_sentences.sort(key=lambda x: x[1], reverse=True)

    compressed = []
    token_count = 0
    for sent, score, source in all_sentences:
        sent_tokens = count_tokens(sent)
        if token_count + sent_tokens > max_tokens:
            break
        compressed.append(sent)
        token_count += sent_tokens

    return "\n".join(compressed)
```

---

### Abstractive Compression

Use an LLM to summarize retrieved content, preserving key information in fewer tokens.

```python
# Pseudo-code: Abstractive Context Compression
def abstractive_compress(query, documents, llm, max_tokens=1000):
    # First pass: summarize each document
    summaries = []
    for doc in documents:
        summary = llm.generate(
            f"Summarize the following text, focusing on information "
            f"relevant to: '{query}'\n\n{doc.text}\n\nSummary:"
        )
        summaries.append(summary)

    # Second pass: merge summaries if still too long
    merged = "\n\n".join(summaries)
    if count_tokens(merged) > max_tokens:
        merged = llm.generate(
            f"Combine these summaries into a concise context "
            f"(max {max_tokens} tokens) for answering: '{query}'\n\n{merged}"
        )

    return merged
```

---

### Token-Level Compression (LLMLingua-style)

Remove low-information tokens based on perplexity scores from a small model.

```python
# Pseudo-code: Token-Level Compression
def token_compress(text, small_model, target_ratio=0.5):
    tokens = tokenize(text)
    # Compute perplexity/importance of each token
    importance_scores = small_model.compute_token_importance(tokens)

    # Keep only the most informative tokens
    target_length = int(len(tokens) * target_ratio)
    sorted_indices = sorted(
        range(len(tokens)),
        key=lambda i: importance_scores[i],
        reverse=True
    )
    keep_indices = sorted(sorted_indices[:target_length])

    compressed_tokens = [tokens[i] for i in keep_indices]
    return detokenize(compressed_tokens)
```

**Compression ratios achievable:** 2x-20x with minimal quality loss.

---

## 4. Context Caching

### Prefix Caching

Cache the system prompt and few-shot examples that are shared across requests.

```python
# Pseudo-code: Prefix Caching
class CachedLLM:
    def __init__(self, llm, system_prompt, few_shot_examples):
        self.llm = llm
        # Pre-compute KV cache for the static prefix
        self.prefix = system_prompt + "\n\n" + format_examples(few_shot_examples)
        self.cached_kv = llm.compute_kv_cache(self.prefix)

    def generate(self, user_query, retrieved_context):
        # Only compute attention for the dynamic part
        dynamic_input = f"\nContext:\n{retrieved_context}\n\nQuery: {user_query}\nAnswer:"
        return self.llm.generate(
            dynamic_input,
            prefix_kv_cache=self.cached_kv
        )
```

**Supported by:** Anthropic (prompt caching), Google (context caching), vLLM.

---

### Semantic Caching

Cache responses for semantically similar queries to avoid redundant LLM calls.

```python
# Pseudo-code: Semantic Cache
class SemanticCache:
    def __init__(self, similarity_threshold=0.95):
        self.cache = VectorStore()
        self.threshold = similarity_threshold

    def get(self, query):
        query_embedding = embed(query)
        results = self.cache.search(query_embedding, k=1)
        if results and results[0].score > self.threshold:
            return results[0].response  # Cache hit
        return None  # Cache miss

    def set(self, query, response):
        self.cache.insert(embed(query), {"query": query, "response": response})

def cached_rag(query, cache, rag_pipeline):
    cached = cache.get(query)
    if cached:
        return cached

    response = rag_pipeline(query)
    cache.set(query, response)
    return response
```

---

## 5. Sliding Window Attention

Standard self-attention has O(n^2) complexity. Sliding window restricts attention to a local window of size w, reducing complexity to O(n * w).

```
Standard Attention Matrix (n=6):    Sliding Window (w=3):

  t1 t2 t3 t4 t5 t6               t1 t2 t3 t4 t5 t6
t1 [1  1  1  1  1  1]           t1 [1  1  1  0  0  0]
t2 [1  1  1  1  1  1]           t2 [1  1  1  1  0  0]
t3 [1  1  1  1  1  1]           t3 [0  1  1  1  1  0]
t4 [1  1  1  1  1  1]           t4 [0  0  1  1  1  1]
t5 [1  1  1  1  1  1]           t5 [0  0  0  1  1  1]
t6 [1  1  1  1  1  1]           t6 [0  0  0  0  1  1]

Parameters: O(n^2)                 Parameters: O(n * w)
```

### Variants

| Pattern | Description | Used By |
|:--------|:-----------|:--------|
| **Sliding Window** | Each token attends to w nearest neighbors | Mistral, Phi |
| **Global + Sliding** | Some tokens attend to all, rest use window | Longformer, BigBird |
| **Dilated Window** | Gaps in the window for larger receptive field | Longformer |
| **Block Sparse** | Attend to blocks rather than individual tokens | BigBird |
| **Linear Attention** | Approximate attention in O(n) | RWKV, Mamba |

---

## 6. Multi-hop Reasoning

Complex questions often require synthesizing information from multiple sources, with each retrieval step informed by the previous.

```python
# Pseudo-code: Multi-hop Retrieval
def multi_hop_rag(complex_query, knowledge_base, llm, max_hops=3):
    # Step 1: Decompose query into sub-questions
    sub_questions = llm.generate(
        f"Break this complex question into {max_hops} simpler sub-questions "
        f"that can be answered independently:\n{complex_query}"
    )

    intermediate_answers = []

    for i, sub_q in enumerate(sub_questions):
        # Incorporate previous answers into the query
        augmented_query = sub_q
        if intermediate_answers:
            context_from_previous = "\n".join(
                [f"Known fact {j+1}: {a}" for j, a in enumerate(intermediate_answers)]
            )
            augmented_query = f"{context_from_previous}\n\nNew question: {sub_q}"

        # Retrieve for this sub-question
        results = knowledge_base.search(augmented_query, k=3)

        # Generate intermediate answer
        answer = llm.generate(
            f"Context:\n{format_results(results)}\n\n"
            f"Question: {sub_q}\n\nAnswer concisely:"
        )
        intermediate_answers.append(answer)

    # Final synthesis
    final_answer = llm.generate(
        f"Original question: {complex_query}\n\n"
        f"Sub-answers:\n{format_answers(intermediate_answers)}\n\n"
        f"Synthesize a comprehensive final answer:"
    )

    return final_answer
```

---

## 7. Few-Shot Learning Optimization

### Dynamic Few-Shot Selection

Select examples most similar to the current query rather than using fixed examples.

```python
# Pseudo-code: Dynamic Few-Shot Selection
class DynamicFewShot:
    def __init__(self, example_pool):
        self.examples = example_pool
        # Pre-embed all examples
        self.example_embeddings = [
            embed(ex["input"]) for ex in example_pool
        ]
        self.index = build_index(self.example_embeddings)

    def select(self, query, k=3):
        query_embedding = embed(query)
        indices = self.index.search(query_embedding, k=k)
        return [self.examples[i] for i in indices]

def few_shot_prompt(query, example_selector, llm):
    examples = example_selector.select(query, k=3)

    prompt = "Here are some examples:\n\n"
    for ex in examples:
        prompt += f"Input: {ex['input']}\nOutput: {ex['output']}\n\n"
    prompt += f"Input: {query}\nOutput:"

    return llm.generate(prompt)
```

---

### Diverse Few-Shot Selection

Ensure selected examples cover different patterns and edge cases, not just the most similar.

```python
# Pseudo-code: Diverse Few-Shot (MMR-style)
def diverse_few_shot(query, example_pool, k=5, lambda_param=0.7):
    query_emb = embed(query)
    selected = []
    candidates = list(range(len(example_pool)))

    for _ in range(k):
        best_score = -inf
        best_idx = None

        for idx in candidates:
            # Relevance to query
            relevance = cosine_similarity(query_emb, example_embeddings[idx])

            # Diversity from already selected
            if selected:
                max_sim_to_selected = max(
                    cosine_similarity(example_embeddings[idx], example_embeddings[s])
                    for s in selected
                )
            else:
                max_sim_to_selected = 0

            # MMR score: balance relevance and diversity
            score = lambda_param * relevance - (1 - lambda_param) * max_sim_to_selected

            if score > best_score:
                best_score = score
                best_idx = idx

        selected.append(best_idx)
        candidates.remove(best_idx)

    return [example_pool[i] for i in selected]
```

---

## 8. System Prompt Engineering

### Layered System Prompt Pattern

```python
# Pseudo-code: System Prompt Builder
def build_system_prompt(config):
    layers = []

    # Layer 1: Identity
    layers.append(f"""You are {config['role']}.
Expertise: {config['expertise']}
Communication style: {config['style']}""")

    # Layer 2: Context
    if config.get('background'):
        layers.append(f"""Background information:
{config['background']}""")

    # Layer 3: Rules & Constraints
    rules = "\n".join([f"- {r}" for r in config['rules']])
    layers.append(f"""Rules you must follow:
{rules}""")

    # Layer 4: Output Format
    layers.append(f"""Output format:
{config['output_format']}""")

    # Layer 5: Examples (if provided)
    if config.get('examples'):
        examples_text = "\n\n".join([
            f"Example Input: {ex['input']}\nExample Output: {ex['output']}"
            for ex in config['examples']
        ])
        layers.append(f"""Examples of expected behavior:
{examples_text}""")

    # Layer 6: Fallback Instructions
    layers.append(f"""If you are unsure or the query is outside your scope:
{config['fallback_instruction']}""")

    return "\n\n---\n\n".join(layers)
```

### System Prompt Checklist

```
SYSTEM PROMPT QUALITY CHECKLIST
================================
[ ] Identity is clear and specific (not generic)
[ ] Constraints are explicit (what NOT to do)
[ ] Output format is specified (JSON, markdown, plain text)
[ ] Edge cases are handled (what to do when uncertain)
[ ] Examples demonstrate expected behavior
[ ] Token budget is reasonable (< 10% of context window)
[ ] No conflicting instructions
[ ] Tested with adversarial inputs
```

---

## 9. Token Budget Management

### Budget Allocation Strategy

```python
# Pseudo-code: Token Budget Manager
class TokenBudgetManager:
    def __init__(self, model_context_limit=128000, response_buffer=4000):
        self.total = model_context_limit
        self.response_buffer = response_buffer
        self.available = self.total - self.response_buffer

    def allocate(self, system_prompt, examples, tools, history, retrieved_docs, query):
        # Fixed allocations
        system_tokens = count_tokens(system_prompt)
        query_tokens = count_tokens(query)
        tool_tokens = count_tokens(format_tools(tools))

        # Remaining budget for dynamic content
        remaining = self.available - system_tokens - query_tokens - tool_tokens

        # Priority allocation: history gets 25%, retrieval gets 75%
        history_budget = int(remaining * 0.25)
        retrieval_budget = remaining - history_budget

        # Trim history from oldest to newest
        trimmed_history = trim_from_start(history, history_budget)

        # Select retrieved docs within budget
        selected_docs = select_within_budget(retrieved_docs, retrieval_budget)

        return {
            "system_prompt": system_prompt,
            "tools": tools,
            "history": trimmed_history,
            "retrieved_docs": selected_docs,
            "query": query,
            "total_tokens": self.available,
            "used_tokens": (system_tokens + query_tokens + tool_tokens +
                          count_tokens(trimmed_history) + count_tokens(selected_docs)),
        }
```

### Budget Allocation Guidelines

```
Context Window Budget Allocation
═══════════════════════════════════════════

For a 128K token model:

┌────────────────────────────────┬─────────┬──────────┐
│ Component                      │ Percent │ Tokens   │
├────────────────────────────────┼─────────┼──────────┤
│ System Prompt                  │ 3-5%    │ 4K-6K    │
│ Tool/Function Definitions      │ 2-5%    │ 3K-6K    │
│ Few-Shot Examples              │ 5-10%   │ 6K-13K   │
│ Retrieved Documents (RAG)      │ 40-60%  │ 51K-77K  │
│ Conversation History           │ 15-25%  │ 19K-32K  │
│ User Query                     │ 1-2%    │ 1K-3K    │
│ Response Buffer                │ 5-10%   │ 6K-13K   │
├────────────────────────────────┼─────────┼──────────┤
│ Total                          │ 100%    │ 128K     │
└────────────────────────────────┴─────────┴──────────┘
```

---

## 10. Information Ordering

Research (particularly "Lost in the Middle") shows that LLMs are better at using information placed at the beginning and end of the context window.

### Ordering Strategy

```python
# Pseudo-code: Context Ordering for Maximum Recall
def order_context(retrieved_chunks, query):
    # Rank by relevance
    ranked = sorted(retrieved_chunks, key=lambda c: c.score, reverse=True)

    if len(ranked) <= 2:
        return ranked

    # Place most relevant at beginning and end
    # Place least relevant in the middle
    most_relevant = ranked[0]        # Position: first
    second_most = ranked[1]          # Position: last
    rest = ranked[2:]                # Position: middle (descending relevance)

    ordered = [most_relevant] + rest + [second_most]
    return ordered
```

### Information Ordering Patterns

```
Pattern 1: "Bookend" (Recommended)
┌──────────────────────────────────────┐
│ [MOST RELEVANT] ...middle... [2ND]   │
│  ↑ High recall    Low recall  ↑      │
│  Beginning                    End    │
└──────────────────────────────────────┘

Pattern 2: "Front-loaded" (For short contexts)
┌──────────────────────────────────────┐
│ [1ST] [2ND] [3RD] ... [LEAST]       │
│  ↑ Most important ──────> Least     │
└──────────────────────────────────────┘

Pattern 3: "Sandwich" (For very long contexts)
┌──────────────────────────────────────┐
│ [INSTRUCTION + KEY FACTS]            │
│ [RETRIEVED DOCUMENTS]                │
│ [RETRIEVED DOCUMENTS]                │
│ [RETRIEVED DOCUMENTS]                │
│ [INSTRUCTION REMINDER + QUERY]       │
└──────────────────────────────────────┘
```

The "Sandwich" pattern repeats the key instruction at the end, which helps the model remember what it was asked even after processing a large context.

---

## Summary: Technique Selection Guide

| Technique | When to Use | Impact | Complexity |
|:----------|:-----------|:------:|:----------:|
| Recursive Chunking | Default starting point | Medium | Low |
| Semantic Chunking | High-quality retrieval needed | High | Medium |
| Naive RAG | Prototyping, simple use cases | Low | Low |
| Advanced RAG | Production quality requirements | High | Medium |
| Agentic RAG | Complex, multi-step questions | Highest | High |
| Extractive Compression | Reduce cost, fit more context | Medium | Low |
| Abstractive Compression | Maximum compression needed | High | Medium |
| Token-level Compression | Extreme cost optimization | Medium | Medium |
| Prefix Caching | Shared system prompts | Cost savings | Low |
| Semantic Caching | Repeated similar queries | Latency/Cost | Medium |
| Dynamic Few-Shot | Variable query types | High | Medium |
| Multi-hop Reasoning | Complex analytical questions | High | High |
| Information Ordering | Long contexts (>50K tokens) | Medium | Low |
| Token Budget Management | Production systems | Medium | Medium |

---

<div align="center">

**[Back to Main Guide](../README.md)**

</div>
