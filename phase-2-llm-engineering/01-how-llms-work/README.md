# 01 - How LLMs Work

Concepts, not math. The goal is to understand what's happening well enough to make good engineering decisions.

## The minimum you need to know

### Tokens

LLMs don't read words. They read tokens — chunks of characters. "unbelievable" might be 3 tokens. A token is roughly 0.75 words on average.

Why it matters: API pricing is per token. Context limits are in tokens. You need to estimate costs and debug "context exceeded" errors.

```python
import tiktoken

enc = tiktoken.encoding_for_model("gpt-4o")
tokens = enc.encode("Hello, world!")
print(len(tokens))  # 4
```

### Context window

The total tokens the model can see at once — input plus output combined. GPT-4o: 128k. Claude: up to 200k.

Why it matters: if your documents don't fit, you need RAG. If your conversation history grows too long, you need to truncate. This is a real engineering constraint you'll hit constantly.

### Temperature

Controls randomness. 0 = deterministic (same output every time). 1+ = more creative. For structured output like JSON or code, use 0. For creative tasks, use 0.7 to 1.

### Embeddings

Text converted to a list of numbers (a vector) that captures meaning. Similar texts have vectors close together in space.

Why it matters: the foundation of RAG. You embed your documents, embed the user's query, find the closest documents by vector similarity, and feed them to the model.

```python
from openai import OpenAI

client = OpenAI()
response = client.embeddings.create(
    model="text-embedding-3-small",
    input="What is RAG?"
)
vector = response.data[0].embedding  # list of 1536 floats
```

### How the Transformer works (high level)

Input tokens → embeddings → attention layers → output token probabilities → sample next token → repeat.

Attention is the key idea: each token looks at all other tokens in the context and decides how much to weight each one. That's how the model understands context and meaning.

You don't need to implement this. You need to understand it well enough to explain it clearly.

## Resources

- [The Illustrated Transformer](https://jalammar.github.io/illustrated-transformer/) - visual walkthrough, no code required
- [Andrej Karpathy - Let's build GPT](https://www.youtube.com/watch?v=kCc8FmEb1nY) - builds a small GPT from scratch in PyTorch
- [HuggingFace Course Chapter 1](https://huggingface.co/learn/nlp-course/chapter1/1) - practical intro to transformers
