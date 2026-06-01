# 02 · NLP & Transformers

The architecture that changed everything. Understanding attention means understanding modern LLMs.

## Learning path

1. Start with [The Illustrated Transformer](https://jalammar.github.io/illustrated-transformer/) - visual, no code
2. Implement self-attention from scratch (notebook included)
3. Use HuggingFace for text classification
4. Fine-tune a small model on a custom dataset

## Notebooks

| Notebook | Description |
|---|---|
| `01_word_embeddings.ipynb` | Word2Vec and embedding visualization |
| `02_attention_from_scratch.ipynb` | Self-attention implemented in NumPy |
| `03_transformer_from_scratch.ipynb` | Full Transformer following Karpathy |
| `04_huggingface_pipeline.ipynb` | Classification with pre-trained models |
| `05_finetune_bert.ipynb` | Fine-tuning BERT for custom classification |

## Setup

```bash
pip install transformers datasets tokenizers torch
```

## Resources

- [The Illustrated Transformer](https://jalammar.github.io/illustrated-transformer/)
- [HuggingFace Course](https://huggingface.co/learn/nlp-course/chapter1/1)
- [Andrej Karpathy - Let's build GPT](https://www.youtube.com/watch?v=kCc8FmEb1nY)
- [Attention is All You Need (original paper)](https://arxiv.org/abs/1706.03762)
