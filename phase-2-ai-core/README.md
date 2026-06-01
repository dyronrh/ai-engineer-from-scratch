# Phase 2 - AI Core

**Estimated duration:** 6-10 weeks  
**Prerequisite:** Phase 1 done, or solid Python confidence

---

## Market context for this phase

Phase 2 ends with LLM Engineering — the skill that appears in more job postings than any other in 2024-2025. PyTorch and the transformer architecture give you the foundation to actually understand what LLMs are doing. Without that, you're a prompt engineer. With it, you're an AI engineer.

- PyTorch: 37.7% of AI Engineer job postings
- LangChain: 39.9% of agentic AI engineering roles  
- LLM APIs (OpenAI, Anthropic): standard across almost all companies

---

## Modules

### [01 - Deep Learning](./01-deep-learning/)

Neural networks from first principles. You don't need to be a researcher, but you do need to know what a gradient is, why training loops work, and how PyTorch autograd fits together. This is what separates engineers who can debug production models from those who can't.

**Topics:**
- Perceptron and feedforward networks
- Backpropagation step by step
- PyTorch: tensors, autograd, training loop
- CNNs for computer vision
- Batch normalization, dropout, regularization

**Resources:**
| Resource | Time |
|---|---|
| [fast.ai - Practical Deep Learning](https://course.fast.ai/) | 3 weeks |
| [PyTorch official tutorials](https://pytorch.org/tutorials/) | 1 week |
| [Andrej Karpathy - Neural Networks: Zero to Hero](https://www.youtube.com/playlist?list=PLAqhIrjkxbuWI23v9cThsA9GvCAUhRvKZ) | 1 week |

---

### [02 - NLP and Transformers](./02-nlp-and-transformers/)

Everything LLM-related runs on the transformer architecture. Understanding attention is not optional if you want to build serious AI systems. You don't need to implement one from scratch to get hired — but you need to know how it works well enough to explain it.

**Topics:**
- Word embeddings: Word2Vec, GloVe
- Self-attention mechanism
- Full Transformer architecture
- BERT: classification and fine-tuning
- GPT: autoregressive generation
- HuggingFace: tokenizers, pipelines, Trainer API

**Resources:**
| Resource | Time |
|---|---|
| [The Illustrated Transformer](https://jalammar.github.io/illustrated-transformer/) | 2 days |
| [HuggingFace NLP Course](https://huggingface.co/learn/nlp-course/chapter1/1) | 2 weeks |
| [Andrej Karpathy - Let's build GPT](https://www.youtube.com/watch?v=kCc8FmEb1nY) | 1 week |

---

### [03 - LLM Engineering](./03-llm-engineering/) — highest priority in this phase

This is the skill that gets you hired. Most companies building AI products are not training models — they are calling APIs, building pipelines, and shipping products on top of GPT-4, Claude, and similar models. That's what this module covers.

**Topics:**
- OpenAI API: chat completions, function calling, structured outputs
- Anthropic Claude API: system prompts, tool use, streaming, caching
- Open source models with Ollama (run models locally, no API cost)
- Prompt engineering: zero-shot, few-shot, chain-of-thought
- LangChain: chains, memory, document loaders

**Resources:**
| Resource | Time |
|---|---|
| [OpenAI Cookbook](https://cookbook.openai.com/) | 1 week |
| [Anthropic Docs](https://docs.anthropic.com/) | 3 days |
| [Anthropic Prompt Engineering Guide](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/overview) | 1 week |
| [Ollama docs](https://ollama.com/docs) | 3 days |

---

## Phase project

**Chatbot with memory and context**

A Q&A assistant that maintains conversation history, can load documents, and responds coherently. The goal is to build something you can demo and explain how it works.

**Stack:** Python, LangChain, OpenAI or Anthropic API, Gradio  
**Demonstrates:** API integration, context management, prompt design, working UI

Project folder: [`03-llm-engineering/project/`](./03-llm-engineering/project/)

---

## Phase checklist

- [ ] Implemented backprop manually at least once
- [ ] Trained a CNN with PyTorch on a real dataset
- [ ] Can explain self-attention in plain words
- [ ] Used function calling with OpenAI or tool use with Anthropic
- [ ] Built prompts with few-shot and chain-of-thought that measurably improve outputs
- [ ] Chatbot keeps context across a multi-turn conversation

Next: [Phase 3 - Advanced AI](../phase-3-advanced-ai/)
