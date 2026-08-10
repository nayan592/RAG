# RAG Project

A small Retrieval-Augmented Generation (RAG) project using LangChain, ChromaDB, and OpenRouter-compatible OpenAI models.

## Project structure

- `answer_generation.py` - Builds a query from a user prompt, searches the persisted Chroma vector store, and generates a response with `ChatOpenAI`.
- `ingetion_pipline.py` - Loads `.txt` documents from `docs/`, splits them into chunks, creates embeddings, and persists a ChromaDB vector store.
- `retrival_pipeline.py` - Loads the persisted vector store and performs semantic retrieval from the collection.
- `docs/` - Contains source text documents used to create embeddings and answer questions.
- `db/chroma_db/` - Persisted Chroma vector store directory.
- `.env` - Environment variables for API keys (not committed).
   ```

## Usage

### 1. Build or refresh the vector store

Run the ingestion pipeline to load documents, split them into chunks, and persist embeddings:

```bash
python ingetion_pipline.py
```

### 2. Retrieve documents

Use the retrieval pipeline to load the persisted Chroma store and perform semantic search:

```bash
python retrival_pipeline.py
```

### 3. Generate an answer

Run the main answer-generation script:

```bash
python answer_generation.py
```

This script reads relevant documents from the persisted vector store, combines them into a prompt, and queries the chat model to create an answer.
