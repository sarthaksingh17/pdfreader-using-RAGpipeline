## PDF RAG System

This project implements a Retrieval-Augmented Generation (RAG) system that reads PDF documents and answers user queries using context retrieved from those documents.

### Overview

The system allows users to ask natural language questions about a PDF. Instead of relying only on the LLM’s internal knowledge, the system retrieves relevant chunks from the document and uses them to generate grounded responses.

### Pipeline

Data Ingestion
Documents are loaded using TextLoader, DirectoryLoader, and PyMuPDFLoader.
Each document is structured with page content and metadata for traceability.

Chunking
Large documents are split using RecursiveCharacterTextSplitter to improve retrieval accuracy and avoid token overflow.

Embedding Generation
Each chunk is converted into a vector using the SentenceTransformer model (all-MiniLM-L6-v2).
Embedding logic is handled through a modular EmbeddingManager.

Vector Storage
Embeddings and metadata are stored in ChromaDB using a persistent client.
This enables semantic similarity search over document content.

Retrieval
When a user asks a query:

The query is converted into an embedding

The vector database is searched

Top relevant chunks are returned based on similarity score

Generation
Retrieved context is inserted into a structured prompt and passed to a Groq LLM to generate a grounded answer.


### Environment Variables

API keys are stored in a .env file and are not hardcoded in the project.
The .env file is excluded using .gitignore.

Key Concepts Demonstrated

-- End-to-end RAG architecture

-- Semantic search with vector databases

-- Embedding generation using transformers

-- Context-grounded LLM responses

-- Modular system design

### Conclusion

This project demonstrates how to build a complete RAG pipeline from scratch — from document ingestion to retrieval and LLM-based response generation — using modern NLP tools and vector databases.
