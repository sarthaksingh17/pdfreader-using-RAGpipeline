PDF RAG System

A Retrieval-Augmented Generation (RAG) system that reads PDF documents, stores semantic embeddings in a vector database, and answers user queries using an LLM grounded in document context.

Overview

This project implements a complete end-to-end RAG pipeline:

Document ingestion

Text chunking

Embedding generation

Vector storage using ChromaDB

Semantic retrieval

LLM-based response generation

The system ensures answers are generated from retrieved document context rather than relying solely on the LLM’s internal knowledge.

Architecture
1. Data Ingestion

Documents are loaded using:

TextLoader

DirectoryLoader

PyMuPDFLoader

Each document is structured as:

Document(
    page_content="...",
    metadata={...}
)


Metadata enables traceability and debugging.

2. Chunking

Uses RecursiveCharacterTextSplitter to:

Break large documents into smaller chunks

Improve semantic retrieval

Prevent token overflow

3. Embeddings

Model: all-MiniLM-L6-v2

Library: SentenceTransformers

Output: 384-dimensional vectors

Encapsulated in a modular EmbeddingManager.

4. Vector Database

Database: ChromaDB (PersistentClient)

Stores:

Document text

Metadata

Embeddings

Enables semantic similarity search.

5. Retrieval

The RAGRetriever:

Converts query to embedding

Performs similarity search

Filters by similarity threshold

Returns top-k relevant chunks

6. Generation

LLM: Groq (via ChatGroq)

Retrieved context is injected into a structured prompt

LLM generates grounded response

Project Structure
data/
 ├── pdf/
 ├── text_files/
 └── vector_store/

notebook/
 └── document.ipynb

main.py
requirements.txt
README.md

Example Usage
answer = rag_simple(
    "What is the flight number?",
    rag_retriever,
    llm
)

print(answer)

Environment Setup

API keys are managed securely using a .env file.

Example:

GROQ_API_KEY=your_api_key_here


Make sure .env is added to .gitignore.

Key Features

Modular design (EmbeddingManager, VectorStore, Retriever)

Persistent vector database

Semantic similarity search

Grounded LLM responses

End-to-end RAG pipeline from scratch

Why This Matters

This project demonstrates:

Understanding of RAG system design

Vector database integration

Embedding-based semantic search

LLM orchestration with external knowledge

Production-ready modular architecture

If you'd like, I can also generate:

A shorter recruiter-focused version

A technical deep-dive version

Or an interview explanation script tailored to this project
