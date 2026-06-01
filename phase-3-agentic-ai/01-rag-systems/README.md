# 01 - RAG Systems

Making LLMs answer questions about your own data. The most deployed production pattern for LLM applications in 2024-2025.

## Why RAG instead of fine-tuning

Fine-tuning bakes knowledge into model weights. It is expensive to run, slow to update, and every answer is impossible to trace back to a source.

RAG retrieves at inference time. It is cheap, always current, and every answer can be traced to the exact document chunk that produced it.

Default to RAG. Fine-tune only when RAG and prompt engineering have both failed you.

## The pipeline

```
Your documents
    |
    v chunk (split into pieces, 200 to 1000 tokens each)
    |
    v embed (convert each chunk to a vector)
    |
    v store (save vectors in a vector database)

At query time:
User question
    |
    v embed question
    |
    v search (find top-k most similar chunks by vector distance)
    |
    v generate (send chunks + question to LLM, get grounded answer)
```

## Chunking

How you split documents matters more than most people expect. Chunks that are too large dilute the signal. Chunks that are too small lose context. Overlap helps prevent information loss at boundaries.

```python
from langchain.text_splitter import RecursiveCharacterTextSplitter

splitter = RecursiveCharacterTextSplitter(
    chunk_size=512,
    chunk_overlap=64,
    separators=["\n\n", "\n", ".", " "],
)
chunks = splitter.split_text(document_text)
```

## Vector databases

| Database | Best for |
|---|---|
| ChromaDB | Local dev and small production |
| Pinecone | Managed, scalable production |
| pgvector | You already use Postgres |
| Weaviate | Advanced search features |
| Qdrant | High performance, self-hosted |

```python
import chromadb

client = chromadb.Client()
collection = client.create_collection("my-docs")

collection.add(
    documents=chunks,
    embeddings=embeddings,
    ids=[f"chunk-{i}" for i in range(len(chunks))],
)

results = collection.query(query_texts=["What is RAG?"], n_results=5)
```

## Advanced RAG

### HyDE (Hypothetical Document Embeddings)

Instead of embedding the user's question directly, ask the LLM to write a hypothetical answer first, then embed that. It often retrieves better chunks because the hypothetical answer looks more like the documents than the question does.

```python
hypothetical_answer = await llm("Write a short paragraph answering: " + question)
results = collection.query(query_texts=[hypothetical_answer], n_results=5)
```

### Reranking

After retrieval, use a cross-encoder to score and reorder chunks for better precision. The initial retrieval casts a wide net. Reranking picks the best fish.

```python
from sentence_transformers import CrossEncoder

reranker = CrossEncoder("cross-encoder/ms-marco-MiniLM-L-6-v2")
scores = reranker.predict([(question, chunk) for chunk in retrieved_chunks])
ranked = sorted(zip(scores, retrieved_chunks), reverse=True)
```

## Evaluating RAG

Do not ship a RAG system without measuring it first. Use RAGAS.

```python
from ragas import evaluate
from ragas.metrics import faithfulness, answer_relevancy, context_recall

results = evaluate(
    dataset,
    metrics=[faithfulness, answer_relevancy, context_recall],
)
print(results)
# faithfulness: 0.87, answer_relevancy: 0.91, context_recall: 0.83
```

Target faithfulness above 0.80 and answer relevancy above 0.80 before shipping anything to production.

## Exercises

| Notebook | What you build |
|---|---|
| `01_basic_rag.ipynb` | End-to-end RAG from scratch with Chroma |
| `02_advanced_rag.ipynb` | HyDE + reranking pipeline |
| `03_rag_evaluation.ipynb` | RAGAS metrics on your pipeline |
| `04_rag_api.py` | RAG wrapped as a FastAPI endpoint |

## Resources

- [Pinecone Learning Center](https://www.pinecone.io/learn/)
- [LlamaIndex Docs](https://docs.llamaindex.ai/)
- [RAGAS docs](https://docs.ragas.io/)
- [OpenAI Embeddings Guide](https://platform.openai.com/docs/guides/embeddings)
