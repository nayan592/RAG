# RAG Project

A small Retrieval-Augmented Generation (RAG) project using LangChain, ChromaDB, and OpenRouter-compatible OpenAI models.

## Project structure

- `answer_generation.py` - Builds a query from a user prompt, searches the persisted Chroma vector store, and generates a response with `ChatOpenAI`.
- `ingetion_pipline.py` - Loads `.txt` documents from `docs/`, splits them into chunks, creates embeddings, and persists a ChromaDB vector store.
- `retrival_pipeline.py` - Loads the persisted vector store and performs semantic retrieval from the collection.
- `docs/` - Contains source text documents used to create embeddings and answer questions.
- `db/chroma_db/` - Persisted Chroma vector store directory.
- `.env` - Environment variables for API keys (not committed).

## Setup

1. Create and activate a Python virtual environment:

   ```bash
   python3 -m venv venv
   source venv/bin/activate
   ```

2. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

   If `requirements.txt` is not present, install the main dependencies manually:

   ```bash
   pip install langchain langchain-chroma langchain-openai python-dotenv
   ```

3. Add your OpenRouter API key to `.env`:

   ```env
   OPENROUTER_API_KEY=your_openrouter_api_key_here
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

## Notes

- The project uses OpenRouter-compatible OpenAI clients, so you need a valid `OPENROUTER_API_KEY`.
- The current `answer_generation.py` script limits chat output with `max_tokens=1000` to avoid hitting OpenRouter credit restrictions.
- If you encounter `402` credit errors, reduce `max_tokens` or shorten the query/context input.
- The `docs/` folder must contain `.txt` files for ingestion.

## Customization

- Change `query` values in `answer_generation.py` or `retrival_pipeline.py` to test different questions.
- Tune `split_documents()` chunk size and overlap in `ingetion_pipline.py`
- Adjust `search_kwargs` in `answer_generation.py` or `retrival_pipeline.py` to control how many relevant chunks are returned.

