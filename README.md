# 🩺 Medical Chatbot

An intelligent medical assistant chatbot powered by AI that provides accurate medical information using Retrieval-Augmented Generation (RAG) with LangChain, Pinecone, and Groq.

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Architecture](#architecture)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [API Endpoints](#api-endpoints)

## 🎯 Overview

This Medical Chatbot uses state-of-the-art natural language processing to answer medical questions by retrieving relevant information from a curated knowledge base of medical documents. The system combines semantic search with large language models to provide accurate, context-aware responses.

## ✨ Features

- 🤖 **AI-Powered Responses**: Uses Groq's Llama 3.3 70B model for intelligent answers
- 🔍 **Semantic Search**: Leverages Pinecone vector database for fast, accurate document retrieval
- 📚 **PDF Knowledge Base**: Processes medical PDFs to build a comprehensive knowledge base
- 💬 **Interactive Web Interface**: User-friendly chat interface built with Flask
- 🎯 **Context-Aware**: Retrieves top 3 most relevant documents for each query
- ⚡ **Fast Response Time**: Optimized for quick inference with Groq API

## 🛠️ Tech Stack

### Backend
- **Python 3.10+**
- **Flask**: Web framework
- **LangChain**: LLM orchestration framework
- **LangChain Groq**: Groq integration for LLM inference
- **LangChain Pinecone**: Vector store integration
- **LangChain HuggingFace**: Embeddings model

### AI/ML
- **Groq API**: Fast LLM inference (Llama 3.3 70B Versatile)
- **HuggingFace**: Embeddings (sentence-transformers/all-MiniLM-L6-v2)
- **Pinecone**: Vector database for semantic search

### Data Processing
- **PyPDF**: PDF parsing
- **RecursiveCharacterTextSplitter**: Text chunking

## 🏗️ Architecture

```
User Query
    ↓
Flask Web App
    ↓
LangChain RAG Pipeline
    ↓
    ├─→ HuggingFace Embeddings (384-dim vectors)
    ↓
Pinecone Vector Store (Similarity Search)
    ↓
Top 3 Relevant Documents
    ↓
Groq LLM (Llama 3.3 70B)
    ↓
Generated Response
    ↓
User Interface
```

## 📦 Installation

### Prerequisites
- Python 3.10 or higher
- Anaconda/Miniconda (recommended)
- Pinecone account
- Groq API account

### Step 1: Clone the Repository
```bash
git clone https://github.com/nadamankai/Medical-Chatbot.git
cd Medical-Chatbot
```

### Step 2: Create Virtual Environment
```bash
conda create -n medibot python=3.10 -y
conda activate medibot
```

### Step 3: Install Dependencies
```bash
pip install -r requirements.txt
```

## ⚙️ Configuration

### Step 1: Create Environment File
Create a `.env` file in the root directory:

```env
PINECONE_API_KEY=your_pinecone_api_key_here
GROQ_API_KEY=your_groq_api_key_here
```

### Step 2: Get API Keys

#### Pinecone API Key
1. Go to [https://www.pinecone.io/](https://www.pinecone.io/)
2. Sign up for a free account
3. Navigate to API Keys section
4. Copy your API key

#### Groq API Key
1. Go to [https://console.groq.com/](https://console.groq.com/)
2. Sign up for a free account
3. Navigate to API Keys section
4. Create a new API key
5. Copy your API key (starts with `gsk_`)

### Step 3: Prepare Your Data
1. Place your medical PDF files in the `data/` directory
2. Run the indexing script to create embeddings:

```bash
python store_index.py
```

This will:
- Load all PDFs from the `data/` directory
- Split documents into chunks (500 chars with 20 char overlap)
- Generate embeddings using HuggingFace model
- Store vectors in Pinecone index named `medical-bot`

## 🚀 Usage

### Start the Application
```bash
python app.py
```

The application will start on `http://localhost:8080`

### Using the Chatbot
1. Open your browser and navigate to `http://localhost:8080`
2. Type your medical question in the chat interface
3. Press Enter or click Send
4. Wait for the AI-generated response

### Example Queries
- "What is diabetes?"
- "What are the symptoms of hypertension?"
- "How is acne treated?"
- "What causes anemia?"

## 📁 Project Structure

```
Medical-Chatbot/
├── app.py                      # Main Flask application
├── store_index.py              # Script to create Pinecone index
├── requirements.txt            # Python dependencies
├── setup.py                    # Package setup file
├── .env                        # Environment variables (not in repo)
├── README.md                   # Project documentation
│
├── data/                       # Medical PDF documents
│   └── *.pdf
│
├── src/                        # Source code modules
│   ├── __init__.py
│   ├── helper.py               # Helper functions for data processing
│   └── prompt_template.py     # System prompt for the chatbot
│
├── templates/                  # HTML templates
│   └── chat.html               # Chat interface
│
└── research/                   # Jupyter notebooks for experimentation
    └── trials.ipynb
```

## 🔌 API Endpoints

### `GET /`
Renders the main chat interface.

**Response**: HTML page

### `POST /get`
Handles chat messages and returns bot responses.

**Request**:
```json
{
  "msg": "What is diabetes?"
}
```

**Response**:
```
Diabetes is a chronic condition characterized by high blood sugar levels...
```
![Capture d'écran 2025-11-30 141244.png](assets/Capture%20d%27%C3%A9cran%202025-11-30%20141244.png)

![Capture d'écran 2025-11-30 141421.png](assets/Capture%20d%27%C3%A9cran%202025-11-30%20141421.png)