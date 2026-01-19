# RAG Starter Repo

A **production-ready starter template** for building Generative AI applications — chat systems, RAG pipelines, multi-model orchestration, and inference services — **without hardcoding logic or coupling your app to a single LLM provider**.

This repo gives you a clean separation between:

* models
* prompts
* retrieval
* preprocessing
* inference

So your system doesn’t collapse the moment requirements change.

---

## Why this exists

Most “GenAI repos” are:

* notebooks pretending to be systems
* tightly coupled to one model
* impossible to extend without rewrites

This repo is different.

**Design goals:**

* Model-agnostic (OpenAI, Anthropic, local, future models)
* RAG-first but optional
* Clean abstractions (no LangChain lock-in)
* Easy to deploy, test, and scale
* Works for real products, not demos

---

## Project Structure

```
generative_ai_project/
├── config/                 # Model & logging configs
│   ├── model_config.yaml
│   └── logging_config.yaml
│
├── data/                   # Local runtime data
│   ├── cache/              # Cached responses
│   ├── embeddings/         # Generated embeddings
│   └── vectordb/           # Vector DB indexes (FAISS / Chroma)
│
├── src/
│   ├── core/               # LLM abstraction layer
│   │   ├── base_llm.py
│   │   ├── gpt_client.py
│   │   ├── claude_client.py
│   │   ├── local_llm.py
│   │   └── model_factory.py
│   │
│   ├── prompts/            # Prompt templates & chains
│   │   ├── templates.py
│   │   └── chain.py
│   │
│   ├── rag/                # Retrieval-Augmented Generation
│   │   ├── embedder.py
│   │   ├── retriever.py
│   │   ├── vector_store.py
│   │   └── indexer.py
│   │
│   ├── processing/         # Text preprocessing
│   │   ├── chunking.py
│   │   ├── tokenizer.py
│   │   └── preprocessor.py
│   │
│   └── inference/          # Inference orchestration
│       ├── inference_engine.py
│       └── response_parser.py
│
├── docs/                   # Documentation
│   ├── README.md
│   └── SETUP.md
│
├── scripts/                # Automation scripts
│   ├── setup_env.sh
│   ├── run_tests.sh
│   ├── build_embeddings.py
│   └── cleanup.py
│
├── Dockerfile
├── docker-compose.yml
├── requirements.txt
└── .gitignore
```

---

## Core Concepts

### 1. Model Abstraction (No Vendor Lock-in)

All models implement a shared interface:

```python
class BaseLLM:
    def generate(self, prompt: str) -> str:
        ...
```

Switch providers via config — not code.

---

### 2. Prompt Engineering Is a First-Class Citizen

Prompts live in `src/prompts/`, not scattered across files.

* Reusable templates
* Multi-step chains
* Versionable logic

No magic strings buried in handlers.

---

### 3. RAG Without Framework Hell

RAG is split into:

* Embedding
* Indexing
* Retrieval
* Generation

Each component is replaceable.

Use FAISS today, Chroma tomorrow, or your own store.

---

### 4. Deterministic Preprocessing

Text cleaning, chunking, and tokenization are **explicit**.

This matters for:

* reproducibility
* evals
* debugging hallucinations

---

### 5. Inference as an Engine

Inference is orchestrated, not improvised.

This is where you add:

* guardrails
* retries
* fallbacks
* structured outputs

---

## Quick Start

### 1. Clone

```bash
git clone <repo-url>
cd generative_ai_project
```

### 2. Create virtual environment

```bash
python -m venv .venv
source .venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure models

Edit:

```
config/model_config.yaml
```

Example:

```yaml
provider: openai
model: gpt-4o-mini
temperature: 0.2
```

---

## Example Flow

```text
Input
  ↓
Preprocessing
  ↓
( Optional ) Retrieval
  ↓
Prompt Chain
  ↓
LLM Generation
  ↓
Response Parsing
  ↓
Output
```

---

## Common Use Cases

* Chatbots with memory
* RAG over PDFs / docs
* Internal copilots
* Multi-model routing
* AI APIs (FastAPI / Flask)
* Agent-based systems

---

## What this repo is NOT

* ❌ A LangChain wrapper
* ❌ A tutorial notebook
* ❌ A one-off demo
* ❌ A “just add prompts” repo

This is a **foundation**, not a toy.

---

## Extending the Repo

You can easily add:

* FastAPI service layer
* Agent frameworks
* Tool calling
* Evaluation pipelines
* Observability (Langfuse, OpenTelemetry)
* Multi-tenant memory

The structure won’t fight you.

---

## Who should use this

* Engineers building GenAI products
* Hackathon teams shipping fast
* Founders prototyping real systems
* Anyone tired of rewriting GenAI code every month

---

## License

MIT — do whatever you want, just don’t pretend you wrote it from scratch 😉


