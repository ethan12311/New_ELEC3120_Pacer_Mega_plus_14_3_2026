
# ELEC3120 Network Learning Hub

An AI-powered Computer Networks tutoring web application for university students. Ask questions, upload network diagrams for analysis, and submit PDF documents — all answered by a large language model tuned for networking education.

---

## Features

- **AI Chat** — Ask anything about Computer Networks (TCP/IP, OSI model, routing protocols, subnetting, DNS, HTTP/S, switching, network security, and more)
- **Image Analysis** — Upload network topology diagrams or screenshots; the AI identifies components, explains the architecture, and answers questions about what it sees
- **PDF Analysis** — Upload lecture notes, textbook chapters, or past papers for the AI to summarise, explain, and answer questions about
- **Quiz Mode** — Built-in multiple-choice quizzes with instant feedback
- **Conversation History** — Sessions persist within a run; optionally connect Supabase for permanent storage
- **Response Caching** — Repeated questions are served from cache to save API credits

---

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Flask 3.0 (Python), rendered HTML/CSS/JS |
| Backend API | FastAPI 0.109 + Uvicorn |
| AI Provider | OpenRouter (Qwen 2.5 VL 72B by default) |
| PDF Extraction | pdfplumber + PyPDF2 |
| Database (optional) | Supabase via PostgREST |

---

## Project Structure

```
.
├── main.py              # FastAPI backend — all AI and session endpoints
├── quiz_app_ai.py       # Flask frontend — UI, quiz logic, chat interface
├── ai_services.py       # OpenRouter API integration, response caching
├── pdf_processor.py     # PDF text extraction and chunking
├── concept_analyzer.py  # Tracks student weak areas, generates targeted quizzes
├── database.py          # Supabase integration (optional, falls back to memory)
├── config.py            # All configuration loaded from environment variables
├── requirements.txt     # Python dependencies
└── start.sh             # Startup script — launches both backend and frontend
```

---

## Getting Started

### Prerequisites

- Python 3.12+
- An [OpenRouter](https://openrouter.ai) API key (free tier available)

### Installation

```bash
git clone https://github.com/your-username/network-learning-hub.git
cd network-learning-hub

pip install -r requirements.txt
```

### Configuration

Create a `.env` file in the project root:

```env
# Required
OPENROUTER_API_KEY=sk-or-...

# Optional — Supabase for persistent conversation storage
SUPABASE_URL=https://your-project.supabase.co
SUPABASE_KEY=your-anon-key

# Optional — tuning
DEBUG=false
ENABLE_CACHE=true
CACHE_TTL=300
MAX_IMAGE_SIZE_MB=10
MAX_PDF_SIZE_MB=20
MAX_PDF_PAGES=50
```

### Run

```bash
bash start.sh
```

This starts:
- **FastAPI backend** on `http://localhost:8000`
- **Flask frontend** on `http://localhost:5000`

Open your browser at `http://localhost:5000`.

---

## API Reference

The FastAPI backend exposes these endpoints (docs at `/docs`):

| Method | Endpoint | Description |
|---|---|---|
| GET | `/health` | Status, provider config, and feature flags |
| POST | `/chat` | Text chat with session continuity |
| POST | `/chat/with-image` | Chat with an attached image (multipart) |
| POST | `/chat/with-pdf` | Chat with an attached PDF (multipart) |
| POST | `/pdf/validate` | Validate a PDF and return metadata without AI analysis |
| GET | `/session/{session_id}` | Retrieve conversation history |
| DELETE | `/session/{session_id}` | Clear a session |
| GET | `/conversations` | List all conversations |

---

## AI Models

The default model is `qwen/qwen2.5-vl-72b-instruct` via OpenRouter, which supports both text and image (VLM) inputs. You can override the model in your `.env`:

```env
OPENROUTER_MODEL=qwen/qwen2.5-vl-72b-instruct
VLM_MODEL=qwen/qwen2.5-vl-72b-instruct
```

Any model available on OpenRouter can be used. Vision features require a VLM-capable model.

---

## Database (Optional)

By default, conversation history is stored in memory and lost on restart. To enable persistent storage, provide Supabase credentials in your `.env`. You will need to create two tables in your Supabase project:

**`conversations`**
| Column | Type |
|---|---|
| session_id | text (primary key) |
| title | text |
| created_at | timestamptz |
| updated_at | timestamptz |

**`messages`**
| Column | Type |
|---|---|
| id | uuid (primary key) |
| session_id | text (foreign key) |
| role | text |
| content | text |
| created_at | timestamptz |

---

## Networking Topics Covered

- TCP/IP protocol suite
- OSI model (all 7 layers)
- Routing protocols — OSPF, BGP, RIP, EIGRP
- Subnetting and CIDR
- DNS resolution
- HTTP/1.1, HTTP/2, HTTPS, TLS
- Switching and VLANs
- Network security fundamentals
- Network topology and diagram reading

---
- https://new-elec-3120-pacer-megaplus-1432026--ethanethan4.replit.app/
- the website will be expired till : 4/13/2026 :(
 
- i made a reflection about this project as well
- you can go to reflection.md to have a look
## License

MIT
