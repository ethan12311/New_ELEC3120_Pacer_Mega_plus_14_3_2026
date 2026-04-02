# ELEC3120 Network Learning Hub - FYP Work Log

---

## Meeting Minutes — 2 April 2026

### Objective

Replace all hardcoded knowledge-base content in the Network Learning Hub backend with real lecture material from three ELEC3120 course PDFs (Congestion Control, Advanced Congestion Control, Queue Management), so the AI tutor can answer questions and generate quizzes grounded in actual course content rather than generic placeholder text.

---

### What Was Updated

#### 1. `quiz_app_ai.py` — Knowledge Base, QA Patterns & Quiz Bank

| Section | Before | After |
|---|---|---|
| `knowledge_base` | 5 generic protocol entries (TCP, UDP, HTTP, HTTPS, DNS) | 15 topic-specific entries covering Congestion Control, TCP Reno, CUBIC, BBR, BDP, Fair Queueing, Token Bucket, Network Calculus, and more |
| `qa_patterns` (local fallback) | 4 regex patterns | 22 regex patterns with answers drawn from lecture slides |
| `QUIZ_QUESTIONS` | 2 questions across 2 categories | **38 questions across 11 categories**: congestion-control-basics, tcp-reno, congestion-fairness, mathis-equation, tcp-cubic, advanced-cc, rtt-fairness, queue-management, wfq, token-bucket, network-calculus |

All Flask routes and the full HTML/JS frontend template were left untouched.

#### 2. `concept_analyzer.py` — Concept Taxonomy Expansion

| Metric | Before | After |
|---|---|---|
| Tracked concepts | 8 (tcp, udp, osi, routing, subnetting, dns, http, switching) | **24** (original 8 retained + 16 new from PDFs) |
| Follow-up suggestions | 8 | **24** (one per concept) |

New concepts added: `congestion_control`, `bdp`, `tcp_reno`, `duplicate_ack`, `tcp_cubic`, `bbr`, `bufferbloat`, `mathis_equation`, `fairness`, `rtt_unfairness`, `fair_queueing`, `wfq`, `token_bucket`, `water_filling`, `network_calculus`, `aimd_vs_others`.

#### 3. `config.py` — AI System Prompt (NETWORKING_CONTEXT)

The AI system prompt grew from roughly 740 characters to over 9,200 characters. It now instructs the AI tutor to cover all ten major topic areas from the three lectures:

1. Congestion Control Fundamentals (BDP, pipe model, congestion collapse of 1986)
2. TCP Reno (slow start, AIMD, CWND, ssthresh, fast recovery, sawtooth)
3. AIMD Properties (Chiu & Jain four axioms, MIMD/AIAD comparison)
4. TCP Performance (Mathis equation, average throughput, high-bandwidth problem)
5. TCP CUBIC (cubic growth function, 20 %/40 % window reduction)
6. Advanced CC — BBR (STARTUP, DRAIN, PROBE_BW, PROBE_RTT phases)
7. Fairness (Jain's Fairness Index, RTT unfairness)
8. Queue Management (Max-Min Fairness, Water Filling, work-conserving)
9. Fair Queueing (bit-by-bit round-robin, WFQ with weights)
10. Traffic Shaping (Token Bucket, Network Calculus, arrival/service curves)

Only `NETWORKING_CONTEXT` was modified; all other config settings, API keys, VLM/PDF contexts, and helper functions remain identical.

---

### Source Material

Three lecture-slide PDFs from Prof. Zili Meng, ELEC 3120 (Fall 2024):

| File | Pages | Topics |
|---|---|---|
| `07-Congestion_Control (1).pdf` | 80 | BDP, TCP Reno, AIMD, CWND, duplicate ACKs, Chiu-Jain fairness, Mathis equation, TCP CUBIC |
| `08-AdvancedCC (1).pdf` | 60 | CUBIC recap, bufferbloat, BBR, Jain's Fairness Index, RTT unfairness |
| `09-Queue (3).pdf` | 83 | Max-Min Fairness, Water Filling, Fair Queueing, WFQ, Token Bucket, Network Calculus |

---

### Files Modified

```
download/
  quiz_app_ai.py        # Knowledge base + QA patterns + 38 quiz questions
  concept_analyzer.py   # 24 concept taxonomy entries with follow-ups
  config.py             # Enriched NETWORKING_CONTEXT system prompt
  README.md             # This file
```

### What Was NOT Changed

- `ai_services.py`, `database.py`, `main.py`, `pdf_processor.py` — no modifications needed
- All Flask API routes and FastAPI endpoints — untouched
- Frontend HTML/JS template inside `quiz_app_ai.py` — untouched
- Environment / `.env` configuration — untouched

---

### Verification

All three updated files pass Python `ast.parse()` syntax checks. No runtime dependencies were added.
