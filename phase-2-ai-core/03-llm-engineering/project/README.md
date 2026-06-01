# Project · Chatbot with Memory and Context

A Q&A assistant that remembers the conversation, can query documents, and responds coherently.

## What it does

- Maintains conversation history across messages
- Can load PDF or text documents and answer questions about them
- Functional chat interface with Gradio
- Handles API errors gracefully

## Stack

- **LLM:** OpenAI GPT-4o or Anthropic Claude (configurable)
- **Framework:** LangChain for memory and chains
- **UI:** Gradio
- **Memory:** ConversationBufferWindowMemory (last N messages)

## How to run

```bash
cd phase-2-ai-core/03-llm-engineering/project
pip install -r requirements.txt

cp .env.example .env
# edit .env with your API key

python app.py
# opens at http://localhost:7860
```

## Structure

```
project/
├── app.py              ← Gradio interface
├── chatbot.py          ← chatbot logic and memory
├── document_loader.py  ← document loading and processing
├── .env.example
├── requirements.txt
└── README.md
```

## What it demonstrates

- State management across conversations
- LLM API integration
- Document loading and querying
- Functional UI to show in a portfolio
