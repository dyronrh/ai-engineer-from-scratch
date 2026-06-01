# 01 · RAG Systems

Making LLMs work with data they weren't trained on.

## Why RAG before fine-tuning

Fine-tuning bakes knowledge into model weights — expensive, slow to update, hard to audit.  
RAG retrieves knowledge at inference time — cheap, always fresh, traceable to sources.

Use RAG first. Fine-tune only when prompt engineering and RAG aren't enough.

## The basic pipeline

```
Documents
   │
   ▼ chunk (split into pieces)
   │
   ▼ embed (convert to vectors)
   │
   ▼ store (vector database)
   │
User query ──▶ embed query ──▶ retrieve top-k chunks
                                       │
                                       ▼
                              LLM generates answer
                              grounded in retrieved chunks
```

## Notebooks

| Notebook | Description |
|---|---|
| `01_embeddings.ipynb` | Understanding and comparing embedding models |
| `02_vector_db_chroma.ipynb` | ChromaDB setup, store and query |
| `03_basic_rag.ipynb` | Full RAG pipeline from scratch |
| `04_advanced_rag.ipynb` | HyDE, reranking, hybrid search |
| `05_rag_evaluation.ipynb` | Evaluate with RAGAS |

## Setup

```bash
pip install chromadb langchain openai ragas llama-index
```

## Resources

- [Pinecone Learning Center](https://www.pinecone.io/learn/)
- [LlamaIndex Docs](https://docs.llamaindex.ai/)
- [RAGAS — RAG evaluation](https://docs.ragas.io/)
- [OpenAI Embeddings Guide](https://platform.openai.com/docs/guides/embeddings)
