***Document-Based RAG Chatbot (No LLM / No API)
This is a lightweight, offline-compatible Retrieval-Augmented Generation (RAG) chatbot that uses only local document chunks and embedding-based retrieval to answer user queries — without using any LLM or APIs.

*** Project Objective:
 Build a chatbot capable of answering questions only based on the content inside uploaded PDF or Word documents using a RAG pipeline.
 No LangChain
 No LLM (e.g., TinyLlama, OpenAI, Claude, etc.)
 No external APIs
 Uses Jina AI V4 embedding model (via sentence-transformers)
 Uses Qdrant vector DB
 Gradio for simple UI

 ***Architecture:
             +---------------------+
             |  User Input (Query) |
             +----------+----------+
                        |
                        v
        +---------------+------------------+
        | Embed Query (Jina AI Embedding)  |
        +---------------+------------------+
                        |
                        v
        +---------------+------------------+
        | Search Vector DB (Qdrant)        |
        | - One vector search only         |
        | - Filters by top match           |
        +---------------+------------------+
                        |
                        v
        +---------------+------------------+
        | Return Exact Chunk from Document |
        | - Includes source metadata       |
        +---------------+------------------+
                        |
                        v
               +--------+--------+
               |   Answer Box    |
               +----------------+
 ***Features:
 
 Only one vector search per query
 Source metadata shown: filename | page number | chunk ID
 Fully local (no internet needed after model downloads)
 Works within 15s response time on Google Colab / Tesla T4 GPU
 Extractive QA: pulls direct answers from matched chunks

***Tech Stack:
Component	      Used Tool / Library
Embedding Model	jinaai/jina-embeddings-v2-small-en
Vector DB	      Qdrant (in-memory mode for Colab)
UI	            Gradio
Chunking	      Custom text splitter with overlap
PDF Reader	    PyPDF2
DOCX Reader   	python-docx
Notebook	      Colab Notebook (.ipynb)

***Setup Instructions:
!pip install qdrant-client sentence-transformers PyPDF2 python-docx gradio

***Chunking Strategy:
Fixed-size chunking: chunk_size = 300, overlap = 50
Keeps semantic continuity
Includes metadata for filename, page, and chunk_id
Helps trace the exact source of every returned answer

 
