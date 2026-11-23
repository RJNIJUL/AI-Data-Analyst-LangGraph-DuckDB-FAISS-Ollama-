# AI Data Analyst (LangGraph + DuckDB + FAISS + Ollama)

An end-to-end, 100% local **AI Data Analyst** that enables users to upload CSV or Excel datasets, ask questions in plain English, generate interactive visualizations, train machine learning models, and export verified analytical reports—**without relying on paid API keys**.

---

## Key Features

- **Zero-Hallucination SQL Analysis:** Translates natural-language questions into validated, read-only DuckDB `SELECT` queries using Pydantic structured outputs, ensuring every numerical answer comes from real computation rather than LLM guessing.
- **RAG Context Retrieval:** Uses Hugging Face Sentence Transformers (`all-MiniLM-L6-v2`) and a FAISS vector index to retrieve dataset metadata, cleaning logs, column definitions, and business formulas.
- **Agentic Routing with LangGraph:** A stateful LangGraph workflow automatically classifies user intent and routes questions either to the FAISS RAG knowledge base or the DuckDB SQL engine.
- **Automated Machine Learning:** Automatically detects Classification vs. Regression tasks based on the target column, prevents data leakage by splitting before encoding, trains a Random Forest model, and displays evaluation metrics alongside sample predictions.
- **Interactive Web Interface & Reports:** Built with Gradio and Plotly, offering live dataset uploads, interactive charts, and one-click downloadable executive reports.

---

## Tech Stack

- **LLM & Agent Orchestration:** Ollama (`qwen2.5:3b`), LangChain, LangGraph, Pydantic
- **RAG & Vector Search:** FAISS (`faiss-cpu`), Sentence Transformers (`all-MiniLM-L6-v2`)
- **Data Processing & SQL:** Python, Pandas, NumPy, DuckDB
- **Machine Learning & Visualization:** Scikit-learn, Plotly
- **Web Interface:** Gradio

---

## System Architecture

```text
                  User Question (Gradio UI)
                             │
                             ▼
                     LangGraph Router
                    /                \
                   /                  \
  [Definitions / Rules]            [Numbers / Metrics]
          │                                 │
          ▼                                 ▼
  FAISS Vector Search             Structured SQL Generation
          │                                 │
          ▼                                 ▼
  Retrieved Context               Read-Only DuckDB Execution
          \                                 /
           \                               /
            ▼                             ▼
           Verified Grounded Answer (Ollama)
