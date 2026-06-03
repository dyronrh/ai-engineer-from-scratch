# Phase 2 - LLM Engineering

**Duration:** 4-6 weeks  
**Prerequisite:** Comfortable with async Python and HTTP APIs

---

## What this phase covers

How LLMs work at a conceptual level, how to call them through APIs, how to use function and tool calling, and how to write prompts that reliably produce the output you need.

This is the skill that appears in more AI Engineer job postings than anything else. OpenAI, Anthropic, Ollama, HuggingFace. You need to be comfortable with all of them.

---

## Modules

### [01 - How LLMs Work](./01-how-llms-work/)

You do not need to know the math. You do need to understand tokens, context windows, temperature, embeddings, and attention well enough to explain them and make good decisions when building.

**Topics:**
- Tokens and tokenization
- Context window constraints and how to work within them
- Temperature and sampling settings
- Embeddings and why they matter for RAG
- Transformer architecture at a high level

**Resources:**
| Resource | Time |
|---|---|
| [The Illustrated Transformer](https://jalammar.github.io/illustrated-transformer/) | 2 days |
| [Andrej Karpathy - Let's build GPT](https://www.youtube.com/watch?v=kCc8FmEb1nY) | 3 days |
| [HuggingFace Course Ch. 1](https://huggingface.co/learn/nlp-course/chapter1/1) | 2 days |

---

### [02 - API and Tool Use](./02-api-and-tool-use/) — highest priority

The core skill. Call APIs, get structured responses, let the model call your functions. Every company building AI products needs engineers who can do this reliably.

**Topics:**
- OpenAI API: chat completions, streaming, function calling, structured outputs
- Anthropic Claude API: tool use, system prompts, streaming, prompt caching
- Local models with Ollama, any open model, no API cost
- HuggingFace Inference API, thousands of models, one interface
- Structured output: reliable JSON responses with Pydantic

**Resources:**
| Resource | Time |
|---|---|
| [OpenAI Cookbook](https://cookbook.openai.com/) | 1 week |
| [Anthropic Docs - Tool use](https://docs.anthropic.com/en/docs/build-with-claude/tool-use) | 3 days |
| [Ollama docs](https://ollama.com/docs) | 2 days |
| [HuggingFace Inference API](https://huggingface.co/docs/api-inference/index) | 2 days |

---

### [03 - Prompt Engineering](./03-prompt-engineering/)

Not magic. Write a prompt, measure the output, iterate. These techniques have real, measurable impact on output quality and are expected knowledge in every AI Engineer role.

**Techniques:**
| Technique | When to use |
|---|---|
| Zero-shot | Simple tasks, capable models |
| Few-shot | When output format or style matters |
| Chain-of-Thought | Reasoning steps, complex logic |
| System prompt | Role, rules, constraints, context |
| Structured output instructions | Get JSON back reliably |
| Self-consistency | Run multiple times, take majority vote |

**Resources:**
| Resource | Time |
|---|---|
| [Anthropic Prompt Engineering Guide](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/overview) | 1 week |
| [OpenAI Prompt Engineering Guide](https://platform.openai.com/docs/guides/prompt-engineering) | 3 days |

---

### [04 - Context Engineering](./04-context-engineering/)

Managing what goes into the context window on every call. Context determines quality, cost, and latency — all three. Most engineers learn this late and it shows in their production costs.

**Topics:**
- Token budgeting: counting tokens, planning what fits
- Prompt caching: Anthropic's cache_control, OpenAI's automatic caching
- Context compression: rolling summaries, selective retention
- Dynamic context selection: embedding-based retrieval for message history
- Conversation management: multi-turn state at scale

**Resources:**
| Resource | Time |
|---|---|
| [Anthropic Prompt Caching Docs](https://docs.anthropic.com/en/docs/build-with-claude/prompt-caching) | 2 days |
| [OpenAI Prompt Caching](https://platform.openai.com/docs/guides/prompt-caching) | 1 day |
| [tiktoken](https://github.com/openai/tiktoken) | 1 day |

---

## Phase project

**Multi-provider LLM router**

A script that sends the same prompt to OpenAI, Anthropic, and Ollama in parallel, collects structured JSON responses, and compares outputs. Covers async API calls, tool use, structured output, and provider abstraction in one project.

Project folder: [`02-api-and-tool-use/project/`](./02-api-and-tool-use/project/)

---

## Phase checklist

- [ ] Called OpenAI with streaming and printed tokens as they arrived
- [ ] Used function calling to have the model invoke a real Python function
- [ ] Used Anthropic tool use with Claude
- [ ] Ran a local model with Ollama, no API key needed
- [ ] Got a reliable JSON response from a model using a Pydantic schema
- [ ] Wrote a few-shot prompt and measured the improvement over zero-shot
- [ ] Used prompt caching and measured the latency and cost difference
- [ ] Implemented conversation history compression when the window fills up

Next: [Phase 3 - Agentic AI](../phase-3-agentic-ai/)
