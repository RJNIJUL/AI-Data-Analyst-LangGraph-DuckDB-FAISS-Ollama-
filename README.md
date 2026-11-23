<img width="1911" height="840" alt="Screenshot 2026-11-23 105950" src="https://github.com/user-attachments/assets/cb71815d-71c8-4f69-afce-1b95695d80cb" />
<img width="1901" height="940" alt="Screenshot 2026-11-23 105736" src="https://github.com/user-attachments/assets/d3033837-333b-4915-92f6-be667c137e7f" />
<img width="1902" height="943" alt="Screenshot 2026-11-23 105648" src="https://github.com/user-attachments/assets/32749a6e-2451-403d-b949-0cea3eceb99d" />
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





## How to Use

### Step 1: Launch the App
- **In Google Colab:** Run all cells in `AI_Data_Analyst.ipynb` and click the `https://xxxx.gradio.live` public link at the bottom.
- **Locally:** Run `ollama pull qwen2.5:3b`, install dependencies (`pip install -r requirements.txt`), and run all cells in `AI_Data_Analyst.ipynb`.

### Step 2: Explore & Ask Questions (Tab 1 — Data & Ask AI)
1. **Upload Dataset (Optional):** Click **Upload CSV or Excel** to load your own `.csv` or `.xlsx` file. The app automatically cleans duplicates and missing values. (If skipped, the built-in 500-row sales dataset is used.)
2. **Ask in Plain English:** Type any question in **Ask a Question** and click **Ask AI**:
   - *Data questions* (e.g., `"Which category has the highest total sales?"`) run a safe DuckDB SQL query for exact numbers.
   - *Definition questions* (e.g., `"How is Profit Margin calculated?"`) search the FAISS vector database for context.

### Step 3: Visualize & Predict (Tab 2 — Charts & ML)
1. **View Charts:** Pick a chart from the dropdown (`Category Sales` or `Region Sales`) and click **Show Chart**.
2. **Train ML Model:** Choose any column in **Select Target Column to Predict** (e.g., `Profit` for regression or `Category` for classification) and click **Train & Predict** to see model accuracy/$R^2$ score and predictions.

### Step 4: Export Report (Tab 3 — Report)
1. Click **Generate Report** to create an executive summary backed by verified DuckDB calculations.
2. Click the `sales_report.txt` link in **Download Report** to save it to your device.
