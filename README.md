# DOCUMIND RAG Agent

A professional-grade Retrieval-Augmented Generation (RAG) system that allows users to upload private documents, organize them into collections, and chat with them using an AI agent.

## 🚀 Features

- **Enterprise-Grade RAG Pipeline**: Built with **LangGraph** for structured, predictable AI workflows.
- **Multi-Format Support**: Integrated OCR (Tesseract/PaddleOCR) and PDF parsing for high-accuracy text extraction.
- **Hybrid Storage**: 
  - **PostgreSQL**: Manages metadata, collections, and conversation history.
  - **Qdrant**: High-performance vector database for fast semantic retrieval.
- **Advanced AI Orchestration**: 
  - Powered by **Google Gemini** for generation and embeddings.
  - Streaming responses via Server-Sent Events (SSE) for a real-time chat experience.
  - Strict prompt engineering to prevent hallucinations and ensure source citations.
- **Modern Frontend**: A sleek **Next.js 15** dashboard with real-time chat and document management.

## 🛠️ Tech Stack

### Frontend
- **Framework**: Next.js 15 (App Router), React 19
- **Styling**: Tailwind CSS, Radix UI
- **Animations**: Framer Motion
- **Icons**: Lucide React

### Backend
- **API**: FastAPI (Python)
- **Orchestration**: LangGraph, LangChain
- **LLM**: Google Gemini (`gemini-2.5-flash`)
- **Vector DB**: Qdrant
- **Database**: PostgreSQL (SQLAlchemy, Alembic)
- **Parsing/OCR**: Tesseract, PaddleOCR

## ⚙️ Installation & Setup

### Prerequisites
- Node.js 18+
- Docker & Docker Compose

### 1. Configure Environment
Create a `.env` file in the `backend/` directory and configure the following:
- **Google Gemini API Key** (`GOOGLE_API_KEY`)
- **PostgreSQL Credentials** (`POSTGRES_PASSWORD`)
- **Qdrant Configuration**

### 2. Start Backend
```bash
cd backend
docker compose up --build
```

### 3. Start Frontend
```bash
# From the project root
npm install
npm run dev
```

### 🌐 Access Points
- **Frontend**: [http://localhost:3000](http://localhost:3000)
- **Backend API**: [http://localhost:8000](http://localhost:8000)
- **Swagger API Docs**: [http://localhost:8000/docs](http://localhost:8000/docs)

## 📖 How It Works

1.  **Ingestion**: Documents are uploaded $\rightarrow$ Parsed via OCR/PDF service $\rightarrow$ Split into chunks $\rightarrow$ Embedded using Gemini $\rightarrow$ Stored in Qdrant.
2.  **Retrieval**: When a user asks a question, the query is embedded and the most relevant chunks are retrieved from Qdrant.
3.  **Generation**: The retrieved context and conversation history are passed to the Gemini LLM via a LangGraph state machine.
4.  **Response**: The AI generates a factual answer with inline citations (e.g., `doc.pdf, p. 2`), streaming the result back to the UI.

## 🛡️ Production Readiness
- **Resiliency**: Implements exponential backoff and retries for embedding API calls.
- **Observability**: Built-in Request-ID tracking and latency monitoring middleware.
- **Security**: CORS protection and environment-based configuration.
- **Stability**: Database migrations managed via Alembic.
