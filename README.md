# 🧠 Conversational RAG API with PDF Support

A FastAPI-based Conversational Retrieval-Augmented Generation (RAG) backend that allows users to upload PDFs, extract content, store embeddings using FAISS, and interact with the content via a Groq-powered LLM (Gemma-2).
---

## 🚀 Features

- 📄 Upload PDF documents (max 20) having maximum 1000 pages
- 🧠 Chunk, embed, and store documents using FAISS and HuggingFace embeddings
- 🤖 Ask questions about uploaded PDFs via REST API
- 🔐 Secure API key management with `.env`
- 🐳 Dockerized for easy local/cloud deployment

---

## 🧰 Tech Stack

| Component       | Technology                         |
|----------------|-------------------------------------|
| Backend        | FastAPI                             |
| RAG Logic      | LangChain + HuggingFace             |
| Vector Store   | FAISS                               |
| Embeddings     | all-MiniLM-L6-v2                    |
| LLM            | Groq (Gemma-2-9b-it)                |
| Metadata Store | SQLite                              |
| Deployment     | Docker + Docker Compose             |

---

## 📦 Project Structure

```
conversational_rag_api/
├── app/ #
│ ├── main.py # FastAPI routes
│ ├── rag.py # RAG logic
│ └── db.py # Metadata storage 
├── tests/ # Test cases
├── vector_store/ # FAISS vector index 
├── documents.db # Metadata DB
├── .env # API keys
├── requirements.txt
├── Dockerfile
├── docker-compose.yml
└── README.md
```
---


---

## ⚙️ Setup Instructions

### 🔧 1. Clone and Setup

```bash
git clone https://github.com/28p07/Conversational_RAG_API.git
cd Conversational_RAG_API
```
---


---

## 🔐 2. Add your .env file
### Create a .env file in the root directory:

```env
GROQ_API_KEY=your_groq_api_key_here
HF_TOKEN=your_huggingface_token_here
```

#### 💡 You can get a Groq API key at https://console.groq.com/keys

---

---
## 📦 3. Install dependencies (Local)
### Using Conda
```bash
conda create -p venv python==3.10 -y
conda activate venv
pip install -r requirements.txt
```
---

---
## 🐳 4. Docker Setup 
### Build & Run with Docker Compose

```bash
docker-compose up --build
```

### API Docs
- Visit: http://localhost:8000/docs <br>
- Interactive Swagger UI is available for testing.

---

---
## 📡 5. API Endpoints
### a. POST /upload :

#### Upload one or more PDF files. 

#### Request: 
- multipart/form-data with files

#### Response:
```json
{
  "results": [
    { "filename": "sample.pdf", "status": "success" }
  ]
}
```

### b. GET /query?q=... :

#### Ask a question about uploaded documents.

#### Example: 

``` http
GET /query?q=What is this document about?
```

#### Response:

```json
"This document discusses..."
```

### c.  GET /documents

#### List all uploaded documents with metadata.

#### Response:

```json
[
  {
    "filename": "sample.pdf",
    "page_count": 2,
    "upload_time": "2025-05-21 13:12:00"
  }
]

```
---


---
## 6. 🧪 Running Tests

```bash
$env:PYTHONPATH="."
pytest -s
```
#### Includes unit + integration tests for upload, metadata, and query

---

## 7. 🚀 Deployment

### This app is ready to deploy:

- 🐳 Via Docker on any Linux server or cloud VM

- 🌐 Easily push to Render, Railway, Fly.io, or AWS ECS

- 🛡️ Store your API keys securely via environment variables

