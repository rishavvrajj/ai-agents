# Agentic RAG

A simple Retrieval-Augmented Generation (RAG) pipeline built in a Jupyter notebook. It loads PDFs, chunks the text, generates embeddings, stores them in ChromaDB, and retrieves semantically relevant passages for any query.

## Pipeline

```
PDFs → load pages → chunk text → embed (MiniLM) → ChromaDB → semantic retrieval
```

## Stack

| Component | Library |
|---|---|
| PDF loading | `langchain-community` PyPDFLoader |
| Text splitting | `langchain-text-splitters` |
| Embeddings | `sentence-transformers` (all-MiniLM-L6-v2) |
| Vector store | `chromadb` (persisted locally) |

## Setup

```bash
# Install dependencies
uv sync

# Launch notebook
jupyter notebook src/notebook/document.ipynb
```

## Usage

Run the notebook cells in order:

1. **Imports** — load libraries
2. **Document Loading** — reads all PDFs under `src/data/`
3. **Chunking** — splits pages into 1 000-char overlapping chunks
4. **Embedding** — encodes chunks with MiniLM (384-dim)
5. **Vector Store** — persists embeddings in `src/data/vector_store/`
6. **Indexing** — embeds & stores all chunks (skip if already indexed)
7. **Retrieval** — `RAGRetriever.retrieve(query, top_k)` returns ranked results
8. **Example Query** — demo search against the loaded documents

## Project structure

```
src/
  data/
    text_files/   # put your PDFs here
    vector_store/ # ChromaDB persisted index (auto-created)
  notebook/
    document.ipynb
```
