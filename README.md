# VeriRAG

VeriRAG is an agentic retrieval-augmented generation chatbot that answers questions from your own documents. It retrieves relevant context before responding and declines when the answer is not supported by the indexed documents.

## Technology

- CrewAI for agent orchestration
- LlamaIndex for document loading, parsing, and retrieval
- ChromaDB for the persistent vector store
- Groq for the language model
- FastAPI for the chat API
- Streamlit for the web UI

## Quick start

### 1. Install dependencies

Use Python 3.10 or newer, create a virtual environment, and install the pinned dependencies:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

### 2. Configure environment variables

Copy the template and add a free Groq API key from [console.groq.com](https://console.groq.com/):

```powershell
Copy-Item env_template.txt .env
```

Then replace `your_groq_api_key` in `.env` with your key. The default template points to `docs/` for source files and `doc_vector_store/` for the generated ChromaDB data.

### 3. Add and index documents

Place PDF or text files in `docs/`. A small sample document is included at `docs/sample_verirag.txt` so the project can be tried immediately. Build the vector store with:

```powershell
python -m src.rag_doc_ingestion.ingest_docs
```

### 4. Start the backend

```powershell
uvicorn src.backend_src.main:app --port 8000
```

### 5. Start the UI

In a second terminal with the virtual environment activated:

```powershell
streamlit run src/frontend_src/app.py
```

Open the Streamlit URL shown in the terminal and ask a question about the indexed sample or your own documents.

## Project layout

```text
docs/                 Source PDFs and text files
src/agents_src/       CrewAI agents, tasks, and RAG tool
src/backend_src/      FastAPI application and chat service
src/frontend_src/     Streamlit application
src/rag_doc_ingestion/  Document ingestion and vector-store creation
```

Generated secrets and vector-store data are excluded from version control. See `.gitignore` for the complete list.