# AI Mastery Learning Plan
# Target: Veteran software engineer → AI practitioner/architect

## How This Works
- Each module has a brief, a set of concepts, and hands-on exercises
- We dive into modules together in sessions — you ask, I guide
- Drill-downs branch off into sub-topics as complexity warrants
- Progress is tracked in PROGRESS.md
- Each completed module gets a notes file under topics/

## Assessment System
Every module has two assessment layers before it can be marked complete:

1. **Pop quizzes** — 2-3 questions after each major concept section, woven naturally
   into the session. Ratings: solid / partial / gap. Gaps get inline clarification.

2. **Final assessment** — 8-12 questions after all material is presented.
   Completion threshold: ≤1 gap AND ≤2 partial.
   Gaps trigger remediation; remediated topics are re-assessed.

Assessment records: `assessments/module-NN-assessment.md`

## Adaptive Curriculum
Modules and sub-modules are added based on assessment results:
- A knowledge gap not covered by existing material → new drill-down (`topics/NNa-*.md`)
- A pattern of related gaps → new sub-module inserted into this plan
- A gap that's prerequisite to a future module → flagged as a prereq check

New additions appear below their parent module in this file.

---

## Curriculum Overview

| # | Module | Core Theme | Status |
|---|--------|-----------|--------|
| 1 | LLM Foundations | How the technology actually works | [ ] |
| 2 | Prompt Engineering | Systematic, not vibe-driven | [ ] |
| 3 | AI APIs & SDKs | Direct programmatic control | [ ] |
| 4 | Tool Use & Function Calling | Giving models real capabilities | [ ] |
| 5 | AI Agents | Autonomous goal-directed systems | [ ] |
| 6 | Model Context Protocol (MCP) | The USB-C of AI integrations | [ ] |
| 7 | RAG & Knowledge Systems | Making models know your stuff | [ ] |
| 8 | Multi-Agent Systems | Orchestrating AI workforces | [ ] |
| 9 | Evals & Testing | Trusting what you ship | [ ] |
| 10 | Fine-tuning & Customization | When prompts aren't enough | [ ] |
| 11 | Production AI Systems | Reliability, cost, observability | [ ] |
| 12 | Frontier Topics | What's coming next | [ ] |

---

## Module 1: LLM Foundations
**Why**: Everything else builds on this. Knowing the internals — even conceptually — makes you a better practitioner.

### Concepts
- Transformers and attention (intuition, not math)
- Tokenization: what tokens are, why they matter, surprising edge cases
- Context windows: limits, chunking, attention costs
- Embeddings: meaning as geometry, similarity search
- How training works: pre-training, RLHF, Constitutional AI
- Model families: GPT-4, Claude, Gemini, Llama — what differs and why
- Capabilities vs. limitations: hallucination, reasoning limits, knowledge cutoffs
- Multimodality: vision, audio, documents — how they're added

### Hands-on
- Play with a tokenizer to see how text is split
- Compare the same prompt across model families
- Observe how context window filling degrades quality

---

## Module 2: Prompt Engineering
**Why**: Your "vibe coding" approach works but leaves 70% of capability on the table. This is the highest leverage skill.

### Concepts
- Anatomy of a prompt: system / user / assistant turns
- Zero-shot vs. few-shot prompting
- Chain-of-Thought (CoT) and why "think step by step" works
- Tree-of-Thought and self-consistency
- Role prompting and persona assignment
- Structured output prompting (JSON, XML, markdown)
- Prompt templating and variable injection
- Negative prompting / telling the model what NOT to do
- Meta-prompting: asking the model to improve your prompt
- Temperature, top-p, top-k, max tokens — what they actually do
- Common failure modes and how to diagnose them

### Hands-on
- Rewrite a vague prompt as a structured prompt — measure quality difference
- Build a few-shot example set for a real use case
- Force structured JSON output reliably
- Experiment with temperature on creative vs. precise tasks

---

## Module 3: AI APIs & SDKs
**Why**: Moving from chat UIs to programmatic control unlocks everything that follows.

### Concepts
- REST API anatomy: request/response, headers, auth
- Messages API vs. completions API (the history)
- Anthropic SDK (Python and TypeScript)
- Streaming responses: why and how
- System prompts vs. injected context vs. user messages
- Multi-turn conversations: managing message history
- Rate limits, retries, and exponential backoff
- Cost modeling: input tokens vs. output tokens, pricing
- Caching: prompt caching and its economics
- Error handling: types of failures, how to recover

### Hands-on
- Write a minimal Claude API call from scratch
- Build a simple multi-turn chat CLI
- Implement streaming output
- Add prompt caching to an expensive repeated call
- Calculate the cost of a realistic workload

---

## Module 4: Tool Use & Function Calling
**Why**: This is the bridge between "text in, text out" and actual software integration.

### Concepts
- What tool use is: the model decides, your code executes
- JSON Schema for defining tools
- The tool use loop: request → tool call → result → continue
- Parallel tool calls
- Tool choice: auto vs. required vs. specific tool
- Building safe tools: validation, sandboxing
- Error handling in tool loops
- Designing good tool interfaces (DX for models)

### Hands-on
- Give a model a calculator tool and watch it use it
- Build a web search tool and wire it to an API
- Handle parallel tool calls correctly
- Design a file system tool with appropriate safety limits

---

## Module 5: AI Agents
**Why**: This is the shift from "assistant" to "autonomous worker." Foundation for everything in the industry right now.

### Concepts
- What an agent is: perception → planning → action → observation loop
- ReAct pattern (Reason + Act): the dominant paradigm
- Memory types: in-context (short), external (long), episodic, semantic
- Planning strategies: one-shot, iterative, hierarchical
- Agent scaffolding: what your code does vs. what the model does
- Tool use as the action space
- When to use agents vs. simple pipelines
- Reliability problems: loops, hallucinated tool calls, scope creep
- Frameworks: LangChain, LlamaIndex, AutoGen, CrewAI, LangGraph — tradeoffs
- Anthropic's recommended patterns for agentic systems
- Claude Code as a live example: how it works

### Hands-on
- Build a minimal agent from scratch (no framework)
- Add memory to an agent using a file/DB
- Observe and debug a runaway agent loop
- Port the scratch agent to a framework — compare

---

## Module 6: Model Context Protocol (MCP)
**Why**: MCP is the emerging standard for connecting AI to tools/data. It's what you're using right now with Claude Code.

### Concepts
- What MCP is: a protocol for AI ↔ tool communication
- The three primitives: Tools, Resources, Prompts
- Architecture: Host (Claude) → Client (in-process) → Server (external)
- Transport options: stdio, HTTP/SSE
- MCP vs. raw tool use: when each is appropriate
- Existing MCP server ecosystem (filesystem, git, GitHub, databases, etc.)
- Building an MCP server from scratch
- Security model: what servers can and cannot do
- MCP in Claude Desktop, Claude Code, and custom apps
- The future: MCP as the USB-C of AI integrations

### Hands-on
- Configure and use 3 existing MCP servers
- Build a minimal custom MCP server exposing a local API
- Debug MCP communication (inspect the wire protocol)
- Extend Claude Code with your own MCP server

---

## Module 7: RAG & Knowledge Systems
**Why**: Makes models accurate about your domain without fine-tuning. Standard component of production AI.

### Concepts
- Why models hallucinate and what RAG solves
- Embeddings as semantic coordinates
- Vector databases: Pinecone, Chroma, Weaviate, pgvector — tradeoffs
- Chunking strategies: fixed, semantic, hierarchical
- Retrieval: cosine similarity, HNSW, approximate nearest neighbor
- Hybrid search: vector + keyword (BM25)
- Reranking: two-stage retrieval for precision
- RAG pipeline: ingest → embed → store → query → augment → generate
- Agentic RAG: retrieval as a tool the agent decides to call
- Evaluation: relevance, faithfulness, context precision
- Knowledge graphs as an alternative/complement

### Hands-on
- Build a RAG pipeline over a local document set
- Experiment with chunk sizes — observe quality difference
- Add reranking and measure improvement
- Wire RAG as a tool into an agent

---

## Module 8: Multi-Agent Systems
**Why**: The frontier of applied AI. Parallel specialized agents outperform single monolithic ones on complex tasks.

### Concepts
- Orchestrator / worker pattern
- Specialization: why domain-specific agents outperform generalists
- Communication patterns: blackboard, message passing, shared state
- Parallelization: when it helps, when it hurts
- Hierarchical multi-agent: agents that spawn agents
- Frameworks: AutoGen, CrewAI, LangGraph, Magentic-One
- Anthropic's published multi-agent patterns
- Consistency and coordination: avoiding conflicting actions
- Human-in-the-loop checkpoints
- Evaluating multi-agent systems

### Note on WorkIQ
- "WorkIQ" may refer to workflow intelligence platforms that orchestrate AI agents across enterprise processes. Will clarify as you share more context on what you've heard.

### Hands-on
- Build a 2-agent system: researcher + writer
- Add a critic agent for review loops
- Implement a parallel map-reduce over a large task
- Use LangGraph to model a stateful multi-agent workflow

---

## Module 9: Evals & Testing
**Why**: "It seems to work" is not engineering. This is how you ship AI with confidence.

### Concepts
- Why evals are different from unit tests
- Evaluation dimensions: correctness, relevance, faithfulness, safety, latency
- Eval approaches: human, LLM-as-judge, automated metrics
- Building eval datasets: golden sets, adversarial sets, edge cases
- Regression testing for prompts (prompt engineering is code)
- Red teaming: jailbreaks, prompt injection, data exfiltration
- Frameworks: Promptfoo, DeepEval, LangSmith, Braintrust
- A/B testing prompts and models in production
- Continuous eval in CI/CD pipelines

### Hands-on
- Write an eval suite for a prompt you've built
- Set up LLM-as-judge scoring
- Perform basic red teaming on your own agent
- Add prompt regression tests to a CI pipeline

---

## Module 10: Fine-tuning & Customization
**Why**: Knowing when NOT to fine-tune is as important as knowing how. Most practitioners reach for it too soon.

### Concepts
- Fine-tuning vs. prompt engineering vs. RAG: decision framework
- When fine-tuning is the right call (style, latency, cost, privacy)
- How fine-tuning works: supervised, RLHF, DPO
- Parameter-efficient methods: LoRA, QLoRA, PEFT
- Dataset preparation: format, size, quality requirements
- Training on Anthropic / OpenAI APIs vs. open weights
- Open-weight models: Llama, Mistral, Qwen — the ecosystem
- Running local models: Ollama, llama.cpp, vLLM
- Distillation: training small models from large ones
- Evaluation after fine-tuning

### Hands-on
- Run a local model with Ollama
- Fine-tune a small open model on a classification task
- Compare: RAG vs. fine-tuned for a specific knowledge task
- Distill a GPT-4 behavior into a smaller model

---

## Module 11: Production AI Systems
**Why**: You've shipped software at scale. This module maps your existing expertise onto AI-specific concerns.

### Concepts
- Latency optimization: streaming, caching, parallel calls, model selection
- Cost management: token budgeting, model tiering, cache hit rates
- Prompt caching economics (Anthropic: 90% cost reduction on cache hits)
- Observability: tracing, logging, token counting in production
- Tools: LangSmith, Helicone, Arize, OpenTelemetry + custom
- Reliability: fallbacks, circuit breakers, retry strategies
- Safety & guardrails: input/output filtering, content policies
- PII handling and data privacy in AI pipelines
- Deployment patterns: Lambda, containers, dedicated GPU
- Versioning: models change, your prompts must be versioned too
- SLAs for AI: setting realistic latency and quality expectations

### Hands-on
- Add tracing to an agent with OpenTelemetry
- Implement a model fallback chain (GPT-4 → Claude → local)
- Set up a prompt registry with versioning
- Calculate and optimize cost for a production workload

---

## Module 12: Frontier Topics
**Why**: Awareness of what's coming lets you make architectural decisions that don't age out in 12 months.

### Concepts
- Multimodal: vision, audio, video — current state and limitations
- Computer use: models that operate browsers/desktops (Anthropic's tool)
- Code generation at scale: AI pair programming → AI-driven development
- Reasoning models: o1/o3, Claude's extended thinking — when to use them
- Long context: 1M token windows and new architectural patterns they enable
- Memory and personalization: persistent agent identity across sessions
- AI-native software development: beyond copilots, toward autonomous dev loops
- Mixture of Experts (MoE): why it matters for cost/capability
- Speculative decoding, quantization: making inference faster/cheaper
- The agent web: agents calling agents across orgs via MCP and APIs

---

## Recommended Learning Sequence

For someone with your background, the highest-leverage order:

```
1 → 2 → 3 → 4 → 5 → 6 → 7 → 8 → 9 → 10 → 11 → 12
```

But you can jump to what's immediately useful:
- Want to use AI in your projects NOW? → 2, 3, 4
- Heard about agents and want to get it? → 5 (requires 4)
- Using Claude Code and want to extend it? → 6
- Building a RAG chatbot? → 7 (requires 3, 4)
- Production concerns? → 11 (can read in parallel)
