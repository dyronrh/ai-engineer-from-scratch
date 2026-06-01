# Phase 2 · AI Core

> The engine room. Master deep learning and LLMs.

**Estimated duration:** 6–10 weeks  
**Prerequisite:** Phase 1 complete (or solid confidence in Python and classical ML)

---

## What you'll be able to do after this phase

- Understand how neural networks work from weights to gradients
- Implement and train models with PyTorch
- Understand the Transformer architecture (the foundation of all modern LLMs)
- Call LLM APIs (OpenAI, Anthropic, Ollama) and build on top of them
- Write prompts that actually work, not prompts that "seem" to work

---

## Modules

### [01 · Deep Learning](./01-deep-learning/)

Neural networks: not just using frameworks - understanding what's happening inside.

**Topics:**
- Perceptron and feedforward networks
- Backpropagation step by step
- CNNs for computer vision
- RNNs and LSTMs (historical context, precursors to transformers)
- PyTorch: tensors, autograd, training loop
- Batch normalization, dropout, regularization

**Resources:**
| Resource | Time |
|---|---|
| [fast.ai - Practical Deep Learning](https://course.fast.ai/) | 4 weeks |
| [CS231n Stanford - CNNs](https://cs231n.github.io/) | 2 weeks |
| [PyTorch official tutorials](https://pytorch.org/tutorials/) | 1 week |

---

### [02 · NLP & Transformers](./02-nlp-and-transformers/)

The architecture that changed everything. Understanding attention means understanding LLMs.

**Topics:**
- Word embeddings: Word2Vec, GloVe
- Self-attention mechanism
- Full Transformer architecture
- BERT: pre-training and fine-tuning
- GPT: autoregressive generation
- HuggingFace: tokenizers, pipelines, Trainer

**Resources:**
| Resource | Time |
|---|---|
| [The Illustrated Transformer](https://jalammar.github.io/illustrated-transformer/) | 2 days |
| [HuggingFace NLP Course](https://huggingface.co/learn/nlp-course/chapter1/1) | 2 weeks |
| [Andrej Karpathy - makemore](https://github.com/karpathy/makemore) | 1 week |

---

### [03 · LLM Engineering](./03-llm-engineering/)

Building real applications on LLMs: API calls, function calling, prompt engineering.

**Topics:**
- OpenAI API: chat completions, function calling, structured outputs
- Anthropic Claude API: system prompts, tool use, streaming
- Open source models with Ollama
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

A Q&A assistant that remembers the conversation, can query documents, and responds coherently.

**Stack:** Python · LangChain · OpenAI or Claude API · Gradio  
**Demonstrates:** API integration · Context management · Prompt design · Functional UI

Project folder: [`03-llm-engineering/project/`](./03-llm-engineering/project/)

---

## Phase checklist

- [ ] Implemented backprop from scratch (even for a small network)
- [ ] Trained a CNN with PyTorch on a real dataset
- [ ] Can explain self-attention without looking at notes
- [ ] Used function calling with OpenAI or tool use with Anthropic
- [ ] Wrote prompts using few-shot and chain-of-thought
- [ ] Chatbot works with conversation context

Next: [Phase 3 · Advanced AI](../phase-3-advanced-ai/)
