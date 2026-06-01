# Phase 2 - LLM Engineering

**Duration:** 4-6 weeks  
**Prerequisite:** Comfortable with async Python and HTTP APIs

---

## What this phase covers

How LLMs work at a conceptual level, how to call them through APIs, how to use function/tool calling, and how to write prompts that reliably produce the output you need.

This is the skill that shows up in more job postings than any other in the AI Engineer category — OpenAI, Anthropic, Ollama, HuggingFace. You need to be fluent with all of them.

---

## Modules

### [01 - How LLMs Work](./01-how-llms-work/)

You don't need to know the math. You do need to understand the concepts — tokens, context window, temperature, embeddings, attention — well enough to explain them and make good decisions when building.

**Topics:**
- Tokens and tokenization (what goes in and comes out)
- Context window and how to work within it in practice
- Temperature and sampling — when to use each setting
- Embeddings — what they are and why they matter for RAG
- Transformer architecture at a high level

**Resources:**
| Resource | Time |
|---|---|
| [The Illustrated Transformer](https://jalammar.github.io/illustrated-transformer/) | 2 days |
| [Andrej Karpathy - Let's build GPT](https://www.youtube.com/watch?v=kCc8FmEb1nY) | 3 days |
| [HuggingFace Course Ch. 1](https://huggingface.co/learn/nlp-course/chapter1/1) | 2 days |

---

### [02 - API and Tool Use](./02-api-and-tool-use/) — highest priority

The core skill. Call APIs, get structured responses, let the model call your functions. This is what every company building AI products needs.

**Topics:**
- OpenAI API: chat completions, streaming, function calling, structured outputs
- Anthropic Claude API: tool use, system prompts, streaming, prompt caching
- Local models with Ollama — run any open model for free, no API cost
- HuggingFace Inference API — thousands of models, one interface
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

Not magic. Engineering: write a prompt, measure the output, iterate. These techniques have measurable impact and are expected in every AI Engineer role.

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

## Phase project

**Multi-provider LLM router**

A script that sends the same prompt to OpenAI, Anthropic, and Ollama in parallel, collects structured JSON responses, and compares the outputs.

Demonstrates: async API calls, tool/function use, structured output, provider abstraction.

Project folder: [`02-api-and-tool-use/project/`](./02-api-and-tool-use/project/)

---

## Phase checklist

- [ ] Called OpenAI with streaming and printed tokens as they arrive
- [ ] Used function calling to have the model invoke a real Python function
- [ ] Used Anthropic tool use with Claude
- [ ] Ran a local model with Ollama — no API key needed
- [ ] Got a reliable JSON response from a model using a Pydantic schema
- [ ] Wrote a few-shot prompt and measured the improvement over zero-shot

Next: [Phase 3 - Agentic AI](../phase-3-agentic-ai/)
