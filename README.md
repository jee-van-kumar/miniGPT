# miniGPT

miniGPT is a FastAPI-based AI chat application powered by Google Gemini models, LangGraph, RAG (retrieval-augmented generation), and a web-based frontend. It allows users to chat with an agent, upload documents, search through uploaded files, remember user preferences, and use web search when needed.

# Demo

## Features

- Chat with an AI assistant using Gemini models
- Streaming chat responses in the browser
- Upload and index documents for retrieval
- Search uploaded documents with RAG
- Persistent conversations and chat history
- Long-term memory for user preferences or important facts
- Web search support via Tavily
- Calculator tool for simple math
- SQLite-based persistence for conversations and memories

## Tech Stack

- Python 3.10+
- FastAPI
- Jinja2 templates
- LangChain
- LangGraph
- Google Generative AI
- Chroma vector database
- SQLite
- Tavily search
- SQLAlchemy

## Project Structure

```text
miniGPT/
│
├── app.py              # FastAPI app and streaming chat endpoints
├── agent.py            # LangGraph agent builder and Gemini model setup
├── rag.py              # Document ingestion and vector search logic
├── database.py         # SQLite + SQLAlchemy models and database helpers
├── tools.py            # Tools used by the agent (calculator, memory, RAG, web search)
├── requirements.txt    # Python dependencies
├── templates/          # HTML frontend templates
├── uploads/            # Uploaded files
├── data/               # SQLite and checkpoint data
├── chroma_db/          # Chroma vector database storage
└── test.py             # Example/test script
```

## Prerequisites

Before running the project, make sure you have:

- Python 3.10 or above
- A Google AI API key
- A Tavily API key
- Internet access for model calls and web search

## Environment Variables

Create a `.env` file in the project root with the following values:

```env
GOOGLE_API_KEY=your_google_generative_ai_key
TAVILY_API_KEY=your_tavily_api_key
GEMINI_MODEL=gemini-2.5-flash
```

You can optionally change `GEMINI_MODEL` to one of the supported values:

- `gemini-2.5-flash`
- `gemini-2.5-pro`
- `gemini-2.5-flash-lite`
- `gemini-1.5-flash`
- `gemini-1.5-pro`

## Installation

1. Clone or open the project folder.
2. Create and activate a virtual environment:

```bash
python -m venv myenv
myenv\Scripts\activate
```

3. Install dependencies:

```bash
pip install -r requirements.txt
```

## Running the Application

Start the FastAPI app with:

```bash
uvicorn app:app --reload
```

Then open:

```text
http://127.0.0.1:8000
```

## Usage

### Chat

- Open the app in your browser.
- Type a message in the chat box.
- The assistant will respond using Gemini and any available tools.

### Upload Documents

- Use the upload feature in the UI.
- Supported file types:
  - `.pdf`
  - `.docx`
  - `.txt`
  - `.md`
  - `.py`
  - `.csv`

Uploaded files are indexed into Chroma and can be searched later by the assistant.

### Memory and RAG

The assistant can:

- search uploaded documents when you ask about them
- remember important facts you tell it
- recall previous saved memories in the same conversation thread
- use web search for current or time-sensitive information

## API Endpoints

The app exposes these main endpoints:

- `GET /` — Home page
- `GET /conversations` — List stored conversations
- `DELETE /conversation/{thread_id}` — Delete a conversation
- `GET /history/{thread_id}` — Get chat history
- `POST /upload` — Upload and index a document
- `POST /chat/stream` — Stream chat responses

## Notes

- The application creates local storage folders such as `uploads/`, `data/`, and `chroma_db/` when it runs.
- Conversation and memory data are stored in SQLite files under `data/`.
- The agent uses tools intelligently, so it may perform web search or document retrieval depending on the query.

## Troubleshooting

If you see an error related to missing API keys:

- confirm your `.env` file exists
- verify `GOOGLE_API_KEY` and `TAVILY_API_KEY` are set correctly
- restart the app after changing environment variables

If documents are not being retrieved:

- make sure the upload completed successfully
- check that the file type is supported
- verify the document has readable text content
