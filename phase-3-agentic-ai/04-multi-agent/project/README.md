# Project · Research Agent with RAG

An agent that takes a research question, retrieves relevant information from a document collection, and generates a structured report with cited sources.

## What it does

1. User submits a research question
2. Agent plans the research strategy (what to look for, in which documents)
3. RAG retrieves the most relevant chunks from the document collection
4. Agent synthesizes findings into a structured report
5. Report includes section headers, key findings, and source citations

## Stack

- **Agent framework:** LangGraph
- **Vector DB:** ChromaDB
- **LLM:** OpenAI GPT-4o or Anthropic Claude
- **Embeddings:** OpenAI `text-embedding-3-small`

## How to run

```bash
cd phase-3-advanced-ai/02-ai-agents/project
pip install -r requirements.txt

cp .env.example .env
# add your API key

# index your documents
python ingest.py --docs-path ./documents/

# run the agent
python main.py --question "What are the main findings about X?"
```

## Structure

```
project/
├── agent.py            ← LangGraph agent definition
├── rag.py              ← RAG pipeline (embed, store, retrieve)
├── ingest.py           ← document ingestion script
├── report_generator.py ← structured report formatting
├── tools.py            ← agent tools (search, retrieve, summarize)
├── main.py             ← entry point
├── documents/          ← your document collection (PDFs, text files)
├── .env.example
├── requirements.txt
└── README.md
```

## What it demonstrates

- Stateful agents with LangGraph
- RAG pipeline in a real application
- Planning and task decomposition
- Structured output generation
- Source attribution
