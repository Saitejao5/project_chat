# 🎓 ScholarBot — AI Research & Education Assistant

> **NeoStats AI Engineer Case Study**

An intelligent chatbot that helps students, researchers, and educators understand complex academic content, explore research papers, and get answers from uploaded study materials — powered by RAG and live web search.

🔗 **Live Demo:** [your-app.streamlit.app](https://your-app.streamlit.app)  
🐙 **GitHub:** [github.com/Saitejao5/project_chat](https://github.com/Saitejao5/project_chat)

---

## ✨ Features

| Feature | Details |
|---|---|
| **📄 RAG Integration** | Upload PDF, DOCX, TXT → auto-chunked → embedded with `all-MiniLM-L6-v2` → FAISS vector search |
| **🌐 Live Web Search** | Serper.dev (Google Search) + Tavily fallback — real-time answers |
| **⚡ Response Modes** | **Concise** (2–4 sentences) or **Detailed** (structured, with headings & citations) |
| **🤖 OpenRouter LLM** | Access 6+ free models (Qwen3, Llama 3.3, Mistral, Gemma) via a single API key |
| **📎 Source Citations** | Every answer shows exactly which document chunk or URL was used |
| **🎨 Dark UI** | Custom-styled Streamlit with professional dark theme |

---

## 📁 Project Structure
```
project/
├── config/
│   └── config.py          ← All API keys, settings, system prompt
├── models/
│   ├── llm.py             ← OpenRouter LLM calls (streaming + retry logic)
│   └── embeddings.py      ← sentence-transformers wrapper (all-MiniLM-L6-v2)
├── utils/
│   ├── rag.py             ← Document ingestion, chunking, FAISS store, retrieval
│   ├── web_search.py      ← Serper + Tavily search integration
│   └── chat.py            ← Prompt building, history trimming
├── app.py                 ← Main Streamlit UI
├── requirements.txt
├── .env.example
└── .gitignore
```

---

## 🚀 Local Setup
```bash
# 1. Clone the repo
git clone https://github.com/Saitejao5/project_chat
cd project_chat

# 2. Install dependencies
pip install -r requirements.txt

# 3. Set up API keys
cp .env.example .env
# Open .env and fill in your keys

# 4. Run
streamlit run app.py
```

---

## 🔑 API Keys

| Variable | Where to get | Required? |
|---|---|---|
| `OPENROUTER_API_KEY` | [openrouter.ai](https://openrouter.ai) | ✅ Yes — main LLM provider |
| `SERPER_API_KEY` | [serper.dev](https://serper.dev) | ⚡ Optional (2500 free queries/month) |
| `TAVILY_API_KEY` | [tavily.com](https://tavily.com) | ⚡ Optional (web search fallback) |

**Minimum to run:** Only `OPENROUTER_API_KEY` is required. Web search falls back to DuckDuckGo if no search keys are set.

Your `.env` file should look like:
```env
OPENROUTER_API_KEY=sk-or-your-key-here
SERPER_API_KEY=your-serper-key      # optional
TAVILY_API_KEY=your-tavily-key      # optional
```

---

## ☁️ Deploy to Streamlit Cloud

1. Push this repo to GitHub
2. Go to [streamlit.io/cloud](https://streamlit.io/cloud) → **New app**
3. Set **Main file path** to `app.py`
4. Add your API keys under **Settings → Secrets**:
```toml
OPENROUTER_API_KEY = "sk-or-your-key-here"
SERPER_API_KEY     = "your-serper-key"
TAVILY_API_KEY     = "your-tavily-key"
```

5. Click **Deploy** — done!

---

## 🧠 How It Works
```
User Question
     │
     ├──► RAG Retrieval (if docs uploaded)
     │       └─ all-MiniLM-L6-v2 embeddings → FAISS cosine search → top-K chunks
     │
     ├──► Web Search (if enabled)
     │       └─ Serper API → Tavily fallback → top-5 results
     │
     └──► OpenRouter LLM (Qwen3 / Llama / Mistral)
             └─ System prompt + context + history → streamed response
```

---

## 📝 Use Case

ScholarBot solves a real problem: academic content is dense, time-consuming to parse, and hard to search. By combining RAG (for uploaded materials) and live web search (for current information), ScholarBot lets anyone:

- 📄 Get instant summaries of uploaded research papers
- ❓ Ask specific questions about textbook chapters
- 🌐 Explore topics with cited, up-to-date web results
- ⚡ Switch between quick answers (Concise) and deep dives (Detailed)

---

## 🛠 Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Streamlit (dark custom theme) |
| LLM Provider | OpenRouter API (OpenAI-compatible) |
| Embeddings | sentence-transformers `all-MiniLM-L6-v2` |
| Vector Search | FAISS (in-memory) |
| Web Search | Serper.dev + Tavily |
| PDF Parsing | PyMuPDF / pypdf |
| Language | Python 3.11+ |

---

*Built for the NeoStats AI Engineer Case Study · 2026*
