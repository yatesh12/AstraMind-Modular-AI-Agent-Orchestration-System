# AstraMind — Modular AI Agent Orchestration System

Smart, extensible platform for orchestrating multi-agent workflows, Retrieval-Augmented Generation (RAG) with FAISS, and domain workflows for customer intelligence and financial planning.

---

## Key Features
- **Modular multi-agent orchestration** with pluggable agent definitions and plan execution.  
- **Retrieval-Augmented Generation (RAG)** using local FAISS index and vector store.  
- **Customer intelligence**: clustering artifacts, example datasets, and forecasting pipelines.  
- **Demo UIs**: Streamlit and Flask entry points for rapid exploration.  
- **Reproducible artifacts**: model checkpoints, index files, and sample notebooks included.  
- **Extensible tooling**: prompt templates, agent tools, and plan templates for fast iteration.

---

## Quick Start

1. Clone and prepare environment
```bash
git clone <repo-url>
cd astramind
python -m venv .venv
# Windows
.venv\Scripts\activate
# macOS / Linux
source .venv/bin/activate
pip install -r requirements.txt
```

2. Add environment variables
- Copy `.env.example` to `.env` (or create `.env`) and populate keys for any external APIs or storage adapters you plan to use.

3. Run demos
- Flask demo:
```bash
python app.py
```
- Orchestrator demo:
```bash
python demo_ai_agent.py
```
- Streamlit UI:
```bash
streamlit run rag_system/streamlit_app.py
```

4. Inspect RAG index
- FAISS index files live in `rag_index_faiss/`. Rebuild using `rag_system/document_ingestion.py` if you change embeddings or data.

---

## Project Layout (concise)
- **app.py, demo_ai_agent.py, main.py, enhanced_app*.py** — entry points and demos  
- **multi_agent_orchestrator.py, ai_agent_system.py, agent_config.py** — orchestration and agent definitions  
- **rag_system/** — ingestion, vector store, pipeline, tools, and Streamlit app  
- **rag_index_faiss/** — FAISS index artifacts (`index.faiss`, `index.pkl`)  
- **data/** — PDFs, CSVs, model artifacts, notebooks (`model data/`)  
- **plans/** — agent plan templates (generic, user)  
- **prompt.py, three_plan.py, schemas_v2.py** — prompts, plan logic, typed schemas  
- **requirements.txt, .env, README.md**

---

## Architecture Overview
- **Agents & Orchestrator**: Agents expose tools and capabilities; the orchestrator coordinates plan generation and execution.  
- **Retrieval Layer**: Documents are embedded and stored in FAISS; pipeline components handle ingestion, retrieval, and context assembly.  
- **Model Artifacts**: Local model checkpoints and metadata live in `data/model data/` for reproducible experiments.  
- **UI & Demos**: Streamlit and Flask endpoints allow fast validation and demos for stakeholders.

---

## How to Extend
- Add new agent types in **agent_config.py** and implement their tool adapters in **rag_system/tools.py**.  
- Add ingestion sources by extending **rag_system/document_ingestion.py** and hooking into the vector store.  
- Swap the local JSON stores for a production DB (Postgres / Mongo) and move FAISS to a persistent store for scale.  
- Containerize with Docker and orchestrate with Kubernetes for production deployments.

---

## Best Practices & Recommendations
- Keep prompt templates in `prompt.py` versioned and minimal; push complex logic into agents/tools.  
- Rebuild FAISS when embedding model or corpus changes.  
- Secure secrets in a secrets manager for production; never commit `.env` with real credentials.  
- Add unit tests around orchestrator flows and vector store operations before large refactors.

---

## Contributing
- Fork, create a feature branch, add tests, and submit a PR with clear context and changelog notes.  
- Follow existing code patterns for prompts, tools, and schema validation.  
- Add or update notebooks and demo flows when adding new capabilities.

---

## License
Add a LICENSE file to declare project licensing. If you want a recommendation, the **Apache 2.0** or **MIT** license are industry-standard and permissive.
