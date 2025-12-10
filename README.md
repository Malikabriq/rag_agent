🚀 RAG Agent — Retrieval-Augmented Generation Pipeline

This project implements a Retrieval-Augmented Generation (RAG) agent using:

LangGraph for workflow orchestration

Ollama (gpt-oss, moondream) for LLM + embeddings

ChromaDB for vector storage

A multi-step pipeline with:

Query rewriting

Document retrieval

Relevance checking

Answer generation

It is designed to test and demonstrate graph-based, controllable RAG systems.

📌 Features
✅ 1. Graph-Orchestrated RAG Pipeline

The pipeline is built using StateGraph and contains these nodes:

agent → decides whether to retrieve or finish

tool → performs vector retrieval

check_relevance → evaluates if retrieved docs are relevant

rewrite → rewrites query to improve retrieval

generate → final answer generation

✅ 2. Automatic Query Rewriting Loop

If retrieved documents are not relevant, the system rewrites the query and retries until relevance is detected.

✅ 3. Custom Retrieval Logic

Uses Ollama Embeddings (moondream)

Stores vectors in ChromaDB

Supports persistent vector store (vector_store/ directory)

✅ 4. Full Logging / Step-by-Step Execution

Every step prints output so you can debug the internal flow.

📂 Project Structure
rag_agent/
│
├── rag_graph.py         # Main RAG graph / pipeline
├── vector_store/        # Chroma persistent DB
├── .gitignore
└── venv/                # Local environment (ignored)

🛠️ Installation
1. Clone repository
git clone https://github.com/Malikabriq/rag_agent.git
cd rag_agent

2. Create virtual environment
python -m venv venv
source venv/bin/activate      # Mac/Linux
venv\Scripts\activate         # Windows

3. Install dependencies
pip install -r requirements.txt

4. Install & run Ollama

Download Ollama:
https://ollama.com/download

Pull required models:

ollama pull gpt-oss:120b-cloud
ollama pull moondream:latest

▶️ Usage

Run the graph:

python rag_graph.py


You will see output showing every node:

STEP: agent decided to retrieve
STEP: tool retrieved 4 docs
STEP: relevance check = yes
STEP: generate produced the answer

🧠 How the RAG Graph Works

The logic matches this workflow:

START
  ↓
agent → (function_call or finish)
  ↓
tool (retriever)
  ↓
check_relevance
     ├── yes → generate → END
     └── no  → rewrite → tool → (loop)


This creates a self-improving retrieval loop until good results are found.

📦 Requirements

You can generate this file:

langgraph
langchain-ollama
langchain-chroma
chromadb
typing-extensions

🤝 Contributing

Pull requests are welcome!
Feel free to open issues for:

Improving the agent logic

Adding more graphs or nodes

Enhancing retrieval quality

Integrating third-party APIs

📄 License

MIT License — free to use for personal and commercial purposes.

⭐ Support

If this project helps you, consider giving the repo a star ⭐ on GitHub!
