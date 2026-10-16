
# 🎥 Video Agent AI

An AI-powered video assistant that transforms video content into searchable, understandable, and useful information. It processes video audio, generates transcripts and summaries, and uses Retrieval-Augmented Generation (RAG) to help users retrieve relevant information from the content.

## ✨ Features

- **Video Audio Extraction** — Extracts audio from supported YouTube videos or local media files.
- **Speech Transcription** — Converts audio into text for further processing.
- **AI-Powered Summarization** — Generates concise summaries of video content.
- **Vector Database** — Splits transcripts into chunks, creates embeddings, and stores them for semantic search.
- **Retrieval-Augmented Generation (RAG)** — Retrieves relevant transcript sections to answer questions about video content.
- **Language Selection** — Supports English and Hinglish modes, depending on the configured application workflow.
- **Modular Architecture** — Separates transcription, summarization, extraction, vector storage, and retrieval into dedicated modules.

## 🛠️ Tech Stack

- **Python** — Core programming language
- **LangChain** — LLM application development and document processing
- **Sarvam AI** — AI-powered speech and language processing
- **Mistral AI** — Large language model capabilities
- **ChromaDB** — Vector database for semantic retrieval
- **Hugging Face Sentence Transformers** — Text embeddings using `all-MiniLM-L6-v2`
- **Recursive Character Text Splitter** — Splits transcripts into manageable chunks
- **yt-dlp** — YouTube media downloading, if configured in the extraction workflow
- **FFmpeg** — Audio and video processing, if required by the extraction workflow

## 📁 Project Structure

```text
video-agent-ai/
├── core/
│   ├── extractor.py       # Audio/media extraction
│   ├── rag_engine.py      # Retrieval and question answering
│   ├── summarizer.py      # Transcript summarization
│   ├── transcriber.py     # Speech-to-text processing
│   └── vector_store.py    # Embeddings and ChromaDB
├── utils/                 # Helper utilities
├── downloads/             # Downloaded media (local only)
├── vector_db/             # Generated vector database (local only)
├── app.py                 # Application entry point / interface
├── main.py                # Main execution script
├── test.py                # Testing script
├── requirements.txt       # Python dependencies
├── .env.example           # Example environment configuration
├── .gitignore
└── README.md
```

*Note: The `utils/` directory may contain additional modules. The `downloads/` and `vector_db/` directories are local runtime directories and may be excluded from Git.*

## 🚀 Getting Started

### 1. Prerequisites

Make sure you have installed:

- Python 3.10 or later (Python 3.12 is suitable for this project)
- Git
- FFmpeg, if required by your media-processing dependencies
- Sarvam AI API key, if required by your configuration
- Mistral AI API key, if required by your configuration
- A working internet connection for YouTube downloads and model downloads

### 2. Clone the Repository

```bash
git clone https://github.com/aadityaa1221/video-agent-ai.git
cd video-agent-ai
```

### 3. Create a Virtual Environment

**macOS / Linux**

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 4. Install Dependencies

```bash
pip install -r requirements.txt
```

If your project uses `uv`, you can alternatively install dependencies with your existing `pyproject.toml` configuration, if one is present.

### 5. Configure Environment Variables

Create a `.env` file in the project root:

```bash
touch .env
```

Add the environment variables required by your application. For example, if your code reads Sarvam AI and Mistral AI API keys from these variables, add:

```env
SARVAM_API_KEY=your_sarvam_api_key_here
MISTRAL_API_KEY=your_mistral_api_key_here
```

Get your API keys from:

- [Sarvam AI Dashboard](https://dashboard.sarvam.ai/)
- [Mistral AI Console](https://console.mistral.ai/)

**Important:** The environment variable names above are examples. Use the exact names expected by your application. Never commit your real `.env` file or publish API keys on GitHub. Keep `.env` in `.gitignore`.

### 6. Run the Application

Run the main video-processing workflow:

```bash
python main.py
```

If you use `uv`:

```bash
uv run python main.py
```

If `app.py` provides a Streamlit interface, launch it with:

```bash
streamlit run app.py
```

Use the launch command that matches your application's actual implementation.

When prompted, provide a supported YouTube URL or a local media file path, then select a language if requested.

## 🧠 How It Works

The project follows a modular AI processing pipeline:

1. **Input:** Accepts a YouTube video URL or supported local media file.
2. **Extraction:** Extracts the audio track from the source media.
3. **Transcription:** Converts the extracted audio into text.
4. **Summarization:** Generates a concise overview of the transcript.
5. **Chunking:** Splits the transcript into smaller, overlapping text chunks.
6. **Embedding:** Converts each chunk into a numerical vector using a sentence-transformer model.
7. **Storage:** Stores the vectors in ChromaDB for semantic retrieval.
8. **Question Answering:** Retrieves relevant chunks and uses a language model to generate context-aware answers.

### RAG Pipeline

```text
Video URL / Local File
         |
         v
   Audio Extraction
         |
         v
    Transcription
         |
         v
  Transcript Summary
         |
         v
   Text Chunking
         |
         v
   Text Embeddings
         |
         v
     ChromaDB
         |
         v
  Relevant Retrieval
         |
         v
   LLM-Generated Answer
```

## 🧪 Testing

Run the project's test script:

```bash
python test.py
```

For projects using `pytest`, you can also run:

```bash
pytest
```

The available tests depend on the current implementation.

## ⚙️ Configuration

The vector-store implementation uses the following configuration, as specified in the project code:

| Setting | Value |
|---|---|
| Vector database | ChromaDB |
| Collection | `meeting_transcript` |
| Embedding model | `all-MiniLM-L6-v2` |
| Chunk size | 500 characters |
| Chunk overlap | 50 characters |
| Embedding device | CPU |

These settings can be adjusted in `core/vector_store.py`.

## 🔐 Security

- Store API keys and credentials in environment variables.
- Never commit `.env`, access tokens, or other secrets.
- Keep virtual environments and generated media out of version control.
- Review downloaded content and generated database files before publishing the repository.

## 🛣️ Future Improvements

- Add timestamps and source references to answers.
- Support multiple videos in a single knowledge base.
- Improve multilingual transcription and summarization.
- Add a polished interactive chat interface.
- Add automated tests for transcription, retrieval, and summarization.
- Support additional media formats and configurable language models.

## 🤝 Contributing

Contributions, suggestions, and bug reports are welcome.

1. Fork the repository.
2. Create a feature branch.
3. Commit your changes.
4. Open a pull request describing your improvements.
