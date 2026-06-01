# 01 - How LLMs Work

Concepts, not math. The goal is to understand what is happening well enough to make good engineering decisions.

## The minimum you need to know

### Tokens

LLMs do not read words. They read tokens, which are chunks of characters. "unbelievable" might be three tokens. On average, one token is about 0.75 words.

This matters because API pricing is per token. Context limits are in tokens. You need to estimate costs and debug "context length exceeded" errors without panicking.

```python
import tiktoken

enc = tiktoken.encoding_for_model("gpt-4o")
tokens = enc.encode("Hello, world!")
print(len(tokens))  # 4
```

### Context window

The total tokens a model can see in one call, input plus output combined. GPT-4o handles 128k tokens. Claude goes up to 200k.

If your documents do not fit, you need RAG. If your conversation history keeps growing, you need to truncate it. This constraint comes up constantly in real production systems.

### Temperature

Controls randomness. At 0, the model produces the same output every time. Higher values make responses more varied and creative. Use 0 for structured output like JSON or code. Use 0.7 to 1 for writing or brainstorming.

### Embeddings

A list of numbers (a vector) that represents the meaning of a piece of text. Similar texts end up with similar vectors. You use this to find relevant documents by meaning, not by keyword matching, which is the foundation of RAG.

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

Input tokens get converted to embeddings, pass through attention layers, produce output token probabilities, sample the next token, and repeat.

Attention is the key mechanism. Each token looks at every other token in the context and decides how much to weight each one. That is how the model understands relationships between words across long distances in the text.

You do not need to implement this. You need to understand it well enough to explain it in an interview.

## Resources

- [The Illustrated Transformer](https://jalammar.github.io/illustrated-transformer/) - visual walkthrough, no code required
- [Andrej Karpathy - Let's build GPT](https://www.youtube.com/watch?v=kCc8FmEb1nY) - builds a small GPT from scratch in PyTorch
- [HuggingFace Course Chapter 1](https://huggingface.co/learn/nlp-course/chapter1/1) - practical intro to transformers
