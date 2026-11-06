# Production RAG Agent

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
- Python 3.10+
- Node.js 18+
- Docker & Docker Compose

### 1. Backend Setup
```bash
cd backend
# Create virtual environment
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Configure environment variables
cp .env.example .env # Create .env and fill in your GOOGLE_API_KEY and DB credentials
```

### 2. Frontend Setup
```bash
# Install dependencies
npm install

# Start development server
npm run dev
```

### 3. Infrastructure
```bash
# Start PostgreSQL and Qdrant using Docker
docker-compose up -d
```

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
