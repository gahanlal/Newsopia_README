# 🌐 NEWSOPIA — AI-Powered News Intelligence Platform

<div align="center">

![Newsopia](https://img.shields.io/badge/NEWSOPIA-News%20Intelligence-667eea?style=for-the-badge&logo=newspaper&logoColor=white)

[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=flat-square&logo=python&logoColor=white)](https://python.org)
[![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?style=flat-square&logo=streamlit&logoColor=white)](https://streamlit.io)
[![LangGraph](https://img.shields.io/badge/LangGraph-00A67E?style=flat-square&logo=chainlink&logoColor=white)](https://langchain.com)
[![OpenAI](https://img.shields.io/badge/OpenAI-GPT--4o-412991?style=flat-square&logo=openai&logoColor=white)](https://openai.com)

**A 12-agent AI system that reads, understands, cross-verifies, and explains the news — so you don't have to.**

</div>

---

## 🧠 What Is Newsopia?

Newsopia is not another news aggregator. It is an **autonomous multi-agent intelligence system** that:

- Scrapes news from multiple search engines and RSS feeds **in parallel**
- Understands what the user is really asking through **deep intent analysis**
- Routes complex queries to **specialized domain agents** (financial, geopolitical, social) that run simultaneously
- **Cross-references claims** across Google, Bing, and DuckDuckGo with title-similarity verification and credibility scoring against a database of **120+ trusted global outlets**
- Synthesizes multi-perspective analyses into a **single, actionable response**
- Supports **General and Personal chat modes** — Personal mode tailors every answer to the user's interests, location, and custom prompts
- Delivers everything through a polished **conversational UI** with chat history, streaming responses, and smart caching

The result: a user asks a plain-English question and receives a comprehensive, source-cited, personalized intelligence briefing — not a list of links.

---

## 🏗️ System Architecture — How the Agents Work Together

Newsopia's core is a **LangGraph state machine** — a directed acyclic graph where each node is a specialized AI agent. Every user query flows through this pipeline, and the graph dynamically decides which agents activate based on the query's intent.

### The 12-Agent Pipeline

```
┌──────────────────────────────────────────────────────────────────────┐
│                         USER QUERY                                   │
└──────────────────┬───────────────────────────────────────────────────┘
                   │
                   ▼
         ┌─────────────────┐
    ①    │  Intent Router   │  Zero-latency regex for trivial queries,
         │                  │  LLM structured output for complex ones.
         │  Decides: WHAT   │  Classifies intent, urgency, complexity.
         │  agents activate │  Determines which specialist agents are needed.
         └────────┬─────────┘
                  │
          ┌───────┴───── casual/help? ──── ⑩ QA Agent (direct answer)
          │
          ▼
    ②  ┌─────────────────┐
       │ Query Analyzer   │  Extracts keywords, entities, time filters,
       │                  │  categories, and financial/global/social flags.
       └────────┬─────────┘
                │
                ▼
    ③  ┌─────────────────┐
       │Search Optimizer  │  Generates engine-specific query variants
       │                  │  (Google syntax vs Bing vs DDG).
       │                  │  Fast-paths simple queries; LLM for complex ones.
       └────────┬─────────┘
                │
                ▼
    ④  ┌─────────────────┐
       │  Web Scraper     │  Hits Google News, Bing News, DuckDuckGo
       │  (3 engines      │  IN PARALLEL. Supports native-language search,
       │   in parallel)   │  50/50 bilingual mode, and RSS fallback.
       └────────┬─────────┘
                │
                ▼
    ⑤  ┌─────────────────┐
       │Content Processor │  No LLM — pure speed. Deduplicates articles,
       │  (rule-based)    │  classifies categories, analyzes sentiment,
       │                  │  extracts keywords, and scores by relevance
       │                  │  + freshness (breaking news floats to top).
       └────────┬─────────┘
                │
                ▼
    ⑥  ┌─────────────────┐
       │  AI Summarizer   │  Parallel article summaries (up to 8 workers).
       │  (parallel LLM)  │  Generates structured insights with JSON output.
       └────────┬─────────┘
                │
        ┌───────┴────────────────────────────────────────┐
        │         INTELLIGENT ROUTING DECISION            │
        │  Based on Intent Router's agent activation:     │
        ├─────────────────┬──────────────┬───────────────┤
        │   Single Agent  │  Multi-Agent │   General QA   │
        │   (financial,   │  (2-3 agents │   (no domain   │
        │   global, OR    │   IN PARALLEL│    specialist)  │
        │   social)       │   + synthesis│               │
        └───────┬─────────┴──────┬───────┴───────┬───────┘
                │                │               │
                ▼                ▼               ▼
    ⑦  ┌──────────────┐ ┌──────────────┐ ┌──────────────┐
       │  Financial    │ │   Global     │ │   Social     │
       │  Impact Agent │ │ Impact Agent │ │ Impact Agent │
       │              │ │              │ │              │
       │ • Live stock │ │ • Geopolitics│ │ • Public     │
       │   data (3    │ │ • Diplomacy  │ │   opinion    │
       │   API chain) │ │ • Sanctions  │ │ • Cultural   │
       │ • Sector     │ │ • Conflict   │ │   impact     │
       │   analysis   │ │   mapping    │ │ • Social     │
       │ • Risk/      │ │ • Alliance   │ │   movements  │
       │   opportunity│ │   analysis   │ │ • Human      │
       │              │ │              │ │   stories    │
       └──────┬───────┘ └──────┬───────┘ └──────┬───────┘
              │                │                 │
              └────────────────┼─────────────────┘
                               │
                    ┌──────────▼──────────┐
    ⑧              │     Synthesis       │  For multi-agent queries:
                   │   (LLM unification) │  Merges all perspectives into
                   │                     │  one actionable briefing.
                   └──────────┬──────────┘
                              │
                              ▼
    ⑨          ┌──────────────────────┐
               │  Response Aggregator  │  Structures the final output:
               │                      │  answer, articles, citations,
               │                      │  analytics, impact summaries.
               └──────────┬───────────┘
                          │
                          ▼
    ⑩          ┌──────────────────────┐
               │      QA Agent        │  Handles follow-up questions,
               │                      │  casual chat, and help requests.
               │                      │  Source-cited, language-aware.
               └──────────┬───────────┘
                          │
                          ▼
               ┌──────────────────────┐
               │     FINAL RESPONSE   │  Answer + articles + analytics
               │     (cached 2 min)   │  delivered to the user.
               └──────────────────────┘
```

### Supporting Agents (outside the main pipeline)

| Agent | Role |
|-------|------|
| **Query Enhancer** | Pre-processes vague queries before they enter the pipeline. Detects ambiguity, enriches context, and injects personal-mode instructions. |
| **Fake News Detector** | Multi-signal credibility engine: source reputation (120+ trusted outlets), 3-engine parallel cross-referencing with title-similarity scoring, linguistic pattern analysis, structural checks, and GPT-powered claim verification. Produces a 0–100 credibility score with verdict. |

---

## ⚡ Performance Architecture

| Optimization | Impact |
|-------------|--------|
| **Single-pass pipeline** | Eliminated the old double-call pattern (search + re-answer). ~40-60% faster. |
| **Parallel agent execution** | Financial + Global + Social agents run simultaneously with individual 20s timeouts. ~3× faster than sequential. |
| **Parallel web scraping** | 3 search engines queried simultaneously. |
| **Dynamic summarizer scaling** | Worker pool scales from 4→8 based on article count. |
| **Response caching** | MD5-hashed cache with 2-min TTL and normalized query keys. Near-identical queries ("Apple stock today" vs "today apple stock") hit the same cache. |
| **Freshness-aware ranking** | Breaking/recent queries boost newer articles. Decay function: articles from 1h ago score 1.0, 24h → 0.5, 72h → 0.2. |
| **Fast-path routing** | Regex instant-match for greetings/help. Simple queries skip LLM in QueryAnalyzer and SearchOptimizer. |
| **Graceful error recovery** | Every agent node is wrapped in try/except — one failing agent doesn't crash the pipeline. Multi-analysis tracks failed agents and proceeds with available results. |
| **Streaming output** | `stream_chat_search()` yields tokens progressively for real-time UI feedback. |

---

## 🔍 Fact-Checking & Credibility Engine

Every article can be analyzed by the **Fake News Detector**, which runs 5 independent signals:

| Signal | Weight | Method |
|--------|--------|--------|
| **Source Credibility** | 25% | Article domain checked against 120+ trusted outlets and known-unreliable database |
| **Cross-Reference** | 25% | Parallel search across Google, Bing, and DuckDuckGo with title-similarity scoring |
| **AI Verification** | 20% | GPT-powered analysis of logical consistency, factual claims, bias indicators |
| **Linguistic Analysis** | 20% | Clickbait patterns, emotional manipulation, ALL-CAPS ratio, factual language detection |
| **Article Structure** | 10% | Author attribution, publication date, content depth, about-page existence |

The weighted score produces a verdict: **Likely Credible**, **Needs Verification**, **Likely Misleading**, or **Likely False**.

Cross-referencing is the strongest differentiator — rather than relying on a single search engine, Newsopia searches 3 engines in parallel, deduplicates by domain, and uses `SequenceMatcher` to verify that other sources are actually reporting the **same story** (not just mentioning similar words).

---

## 🎯 Key Product Features

### 💬 Dual Chat Modes
- **General Mode** — Objective, balanced analysis
- **Personal Mode** — Every answer is tailored to the user's saved interests, location, and custom prompts (e.g., "Always tell me how this affects India's IT sector")

### 🌍 Multilingual Intelligence
- Search in English + native language simultaneously (50/50 bilingual mode)
- UI translations on-demand
- All agents respond in the user's preferred language

### 📊 Real-Time Analytics
- Sentiment distribution across articles
- Source diversity charts
- Trending topics extraction
- Category breakdown

### 🔐 Authentication & Guest Access
- Full auth flow with OTP verification
- Persistent sessions with cookie-based recovery
- Guest mode with configurable daily quotas

### 💾 Collections & Alerts
- Save articles to custom collections
- Topic-based alerts (instant, daily, weekly)
- JSON export

---

## 🧰 Tech Stack

| Layer | Technology |
|-------|-----------|
| **Orchestration** | LangGraph (directed state graph) |
| **LLM** | OpenAI GPT-4o-mini (temp=0 for deterministic output) |
| **Frontend** | Streamlit with custom CSS (glassmorphism dark theme) |
| **Database** | Supabase (PostgreSQL + Row-Level Security) |
| **Financial Data** | yfinance → Polygon.io → Twelve Data (3-tier fallback) |
| **Web Scraping** | BeautifulSoup + requests (parallel, multi-engine) |
| **Caching** | In-memory with MD5 keys + normalized queries |
| **Deployment** | Streamlit Cloud / any Python host |

---

## 🚀 Getting Started

### Prerequisites
- Python 3.10+
- OpenAI API key

### Quick Start

```bash
# Clone and setup
git clone https://github.com/gahanlal/Newsopia.git
cd Newsopia
python -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Configure
# Add your OpenAI API key to config.yaml or set OPENAI_API_KEY env variable

# Run
streamlit run app.py
```

Open `http://localhost:8501` in your browser.

---

## 📈 Why Newsopia Is Different

| Traditional Aggregator | Newsopia |
|----------------------|----------|
| Shows links | Delivers **synthesized intelligence** |
| Single search engine | **3 engines in parallel** with dedup |
| No verification | **5-signal credibility analysis** with 120+ trusted sources |
| One-size-fits-all | **Personal mode** tailored to your interests & location |
| Text only | **Live stock data**, sector analysis, risk assessment |
| Sequential processing | **Parallel multi-agent pipeline** with graceful degradation |
| Static results | **Streaming responses** with smart caching |

---

## 📝 License

This project is proprietary. All rights reserved.

---

<div align="center">

**Built with 🧠 by the Newsopia team**

*12 AI agents. 3 search engines. 120+ trusted sources. One intelligent answer.*

</div>
