# 🌐 NEWSOPIA — AI-Powered News Intelligence Platform

<div align="center">

![Newsopia](https://img.shields.io/badge/NEWSOPIA-News%20Intelligence-667eea?style=for-the-badge&logo=newspaper&logoColor=white)

[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=flat-square&logo=python&logoColor=white)](https://python.org)
[![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?style=flat-square&logo=streamlit&logoColor=white)](https://streamlit.io)
[![LangGraph](https://img.shields.io/badge/LangGraph-00A67E?style=flat-square&logo=chainlink&logoColor=white)](https://langchain.com)
[![OpenAI](https://img.shields.io/badge/OpenAI-GPT--4o-412991?style=flat-square&logo=openai&logoColor=white)](https://openai.com)

**A 17-agent AI system that reads, understands, cross-verifies, and explains the news — so you don't have to.**

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

## 📈 Evolution: From Simple Foundation to Intelligent Knowledge Graph

Newsopia's architecture evolved through deliberate phases, each building on the previous:

### Phase 1: Foundation
Started with a basic multi-agent system: search aggregator → article processor → QA agent. Single language, no specialization.

### Phase 2: Domain Specialist Agents
Added specialized agents that could reason within specific domains:
- **Financial Impact Agent** — Live stock data, sector analysis, market risk assessment
- **Social Impact Agent** — Public sentiment, cultural impact, social movements

Each agent could now provide deep domain expertise, but queries had to be manually routed to the right agent.

### Phase 3: Multilingual News Article Pulling
Implemented parallel multilingual search and content fetching:
- Search in English + user's native language simultaneously (50/50 bilingual mode)
- Fetch articles in both languages
- UI dynamically switches to user's preferred language for articles and responses
- Result: Global news coverage without language barriers

### Phase 4: Credibility & Verification Layer
Added fact-checking and source verification:
- **120+ Trusted Outlets Database**: Cross-reference articles against verified sources
- **5-Signal Credibility Engine**: Source reputation, cross-referencing, AI verification, linguistic analysis, article structure
- **Fake News Detector**: Multi-signal analysis producing 0-100 credibility score with verdict

### Phase 5: Full 17-Agent Pipeline
Expanded from 3 domain agents to a complete intelligent pipeline:
- **Query Analysis & Routing** — Intent detection, category classification, complexity assessment
- **Search Optimization** — Engine-specific query variants for Google, Bing, DuckDuckGo
- **Content Processing & Fetching** — Full article extraction, deduplication, relevance scoring
- **AI Summarization** — Parallel summaries with structured insights
- **3 Specialized Domain Agents** — Financial, Global, Social impact analysis
- **Synthesis Engine** — Unifies multi-agent perspectives
- **5 Enrichment Agents** — Fact-checking, trend analysis, sentiment mapping, regional impact, bias detection
- **Response Aggregation** — Structures final output
- **QA Agent** — Handles follow-ups and casual chat

System now automatically routes complex queries to the right agents and synthesizes their perspectives.

### Phase 6: Multi-Domain Knowledge Graph (Current)
Introduced a sophisticated knowledge graph engine connecting 11 domains with 44 weighted causal edges:

**The 11 Domains**: War, Finance, Energy, Geopolitics, Social, Tech, Health, Trade, Environment, Food, Economy

**How It Works:**
1. **Detects primary domain(s)** from your query using keyword matching and entity recognition
2. **Traverses the knowledge graph** to find 1-2 hop neighbors across related domains (e.g., War → Energy → Finance → Markets)
3. **Identifies blind spots** — domains connected to your query but not covered by scraped articles
4. **Extracts cross-article entities** — recognizes when the same actors/organizations appear across multiple articles
5. **Synthesizes cross-domain intelligence** — generates a brief explaining causal chains and interconnected impacts

**Example:** Query: "What's happening with the war in Ukraine?"
- **Before Phase 6:** Shows articles about military operations and casualties
- **With Knowledge Graph:** Automatically maps War → Energy (oil sanctions) → Finance (markets) → Trade (grain exports) → Food (prices) — connecting the dots the articles don't explicitly mention. Flags blind spots: "Trade domain is 40% covered, Food domain is 20% covered."

**The 44-Edge Ontology:** War DISRUPTS Energy (weight: 9), Energy INFLUENCES Finance (weight: 9), Trade AFFECTS Food (weight: 8), Geopolitics DRIVES Tech (weight: 7) — each with causal descriptions so the LLM reasons about **why** domains are connected, not just **that** they are.

---

## 🏗️ System Architecture — How the Agents Work Together

Newsopia's core is a **LangGraph state machine** — a directed acyclic graph where each node is a specialized AI agent. Every user query flows through this pipeline, and the graph dynamically decides which agents activate based on the query's intent.

### The 17-Agent Pipeline

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
       │Content Processor │  Deduplicates articles, classifies categories,
       │  (rule-based)    │  analyzes sentiment, extracts keywords, scores
       │  + full content  │  by relevance + freshness. Fetches FULL ARTICLE
       │    fetching      │  CONTENT for top 8 articles in parallel (critical
       │                  │  for answer quality). Rule-based, no LLM.
       └────────┬─────────┘
                │
                ▼
    ⑥  ┌─────────────────┐
       │  AI Summarizer   │  Parallel article summaries (up to 8 workers).
       │  (parallel LLM)  │  Generates structured insights with JSON output.
       └────────┬─────────┘
                │
                ▼
    ⑦  ┌─────────────────┐
       │ Knowledge Graph  │  Multi-domain ontology engine: detects primary
       │    Engine       │  domains from query, traverses 1-2 hops across
       │  (11 domains,   │  44 causal edges, identifies blind spots, extracts
       │   44 edges)     │  cross-article entities, synthesizes cross-domain
       │                 │  intelligence brief. Output: domain mapping,
       │                 │  causal chains, blind spots, coverage scores.
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
    ⑧  ┌──────────────┐ ┌──────────────┐ ┌──────────────┐
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
    ⑨              │     Synthesis       │  For multi-agent queries:
                   │   (LLM unification) │  Merges all perspectives into
                   │                     │  one actionable briefing.
                   └──────────┬──────────┘
                              │
                              ▼
        ┌─────────────────────────────────────────────┐
        │        ⑩  ENRICHMENT LAYER (parallel)       │
        │     5 agents run simultaneously (15s cap)   │
        ├─────────┬─────────┬─────────┬───────┬───────┤
        │  Fact   │ Trend   │Sentiment│Region │Source │
        │  Check  │ Context │  Map    │Impact │ Bias  │
        │         │         │         │       │       │
        │ Cross-  │Historic │ Mood    │Geo    │Framing│
        │ ref     │parallels│ gauge   │impact │& lean │
        │ claims  │& traject│ 0-100   │mapping│detect │
        └────┬────┴────┬────┴────┬────┴───┬───┴───┬───┘
             └─────────┴─────────┴────────┴───────┘
                              │
                              ▼
    ⑪          ┌──────────────────────┐
               │  Response Aggregator  │  Structures the final output:
               │                      │  answer, articles, citations,
               │                      │  analytics, enrichment data.
               └──────────┬───────────┘
                          │
                          ▼
    ⑫          ┌──────────────────────┐
               │      QA Agent        │  Handles follow-up questions, casual chat,
               │    (GPT-4o based)    │  and help. ANSWER-FIRST approach: directly
               │                      │  addresses the question before providing
               │                      │  supporting details. Full article content
               │                      │  fed directly (not just snippets). Language
               │                      │  & source-aware with smart caching.
               └──────────┬───────────┘
                          │
                          ▼
               ┌──────────────────────┐
               │     FINAL RESPONSE   │  Answer + articles + analytics
               │     (cached 2 min)   │  + enrichment insights.
               └──────────────────────┘
```

### Enrichment Agents (run in parallel after synthesis)

| Agent | Purpose | Key Output |
|-------|---------|------------|
| **Fact Check Agent** | Cross-references claims across sources, detects contradictions | Confidence score (0–100), verification labels (✅ High / ⚠️ Partial / ❌ Conflicting) |
| **Trend Context Agent** | Historical parallels, trajectory analysis | Escalating / Stable / De-escalating trajectory, timeline, pattern detection |
| **Sentiment Aggregation Agent** | Cross-source mood gauge, emotion breakdown | Sentiment score (0–100), divergence detection between sources |
| **Regional Impact Agent** | Geographic impact mapping, epicenter detection | Affected regions, personalized local impact based on user location |
| **Source Bias Agent** | Framing analysis, political leaning detection (30+ known sources) | Bias spectrum, loaded language detection, media literacy tips |

> All enrichment agents have **smart gating** — they only activate when relevant signals are detected (e.g., Trend Context requires trend keywords, Source Bias needs 2+ distinct sources). Each has a **rule-based fallback** that works without API keys.

### Supporting Agents (outside the main pipeline)

| Agent | Role |
|-------|------|
| **Query Enhancer** | Pre-processes vague queries before they enter the pipeline. Detects ambiguity, enriches context, and injects personal-mode instructions. |
| **Fake News Detector** | Multi-signal credibility engine: source reputation (120+ trusted outlets), 3-engine parallel cross-referencing with title-similarity scoring, linguistic pattern analysis, structural checks, and GPT-powered claim verification. Produces a 0–100 credibility score with verdict. |

---

## ⚡ Performance Optimizations

| Optimization | Impact |
|-------------|--------|
| **Single-pass pipeline** | Eliminated the old double-call pattern (search + re-answer). ~40-60% faster. |
| **Full article content fetching** | Top 8 articles get full text extracted in parallel before QA. Transforms "why" answer quality. Non-blocking — failures silently skip. |
| **Parallel agent execution** | Financial + Global + Social agents run simultaneously with individual 20s timeouts. ~3× faster than sequential. |
| **Parallel enrichment layer** | 5 enrichment agents (Fact Check, Trend, Sentiment, Regional, Bias) run in parallel via ThreadPoolExecutor with 15s timeout. Non-blocking — failures are silently skipped. |
| **Parallel web scraping** | 3 search engines queried simultaneously. |
| **Dynamic summarizer scaling** | Worker pool scales from 4→8 based on article count. |
| **Response caching** | MD5-hashed cache with 2-min TTL and normalized query keys. Near-identical queries ("Apple stock today" vs "today apple stock") hit the same cache. |
| **Freshness-aware ranking** | Breaking/recent queries boost newer articles. Decay function: articles from 1h ago score 1.0, 24h → 0.5, 72h → 0.2. |
| **Fast-path routing** | Regex instant-match for greetings/help. Simple queries skip LLM in QueryAnalyzer and SearchOptimizer. |
| **Graceful error recovery** | Every agent node is wrapped in try/except — one failing agent doesn't crash the pipeline. Multi-analysis tracks failed agents and proceeds with available results. |
| **Streaming output** | `stream_chat_search()` yields tokens progressively for real-time UI feedback. |
| **GPT-4o for answers** | QA agent uses GPT-4o (not mini) for final answer generation — better reasoning over rich article content. All other agents use gpt-4o-mini for cost efficiency. |

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
- **General Mode** — Objective, balanced analysis of news without personal context
- **Personal Mode** — Every answer is deeply tailored to YOU:
  - **Interests**: News angles aligned with your saved topics
  - **Location**: Geographic impact specific to your city/country (local prices, policies, job market)
  - **Occupation**: Career-specific implications (e.g., how tech news affects software engineers vs. doctors)
  - **Bio/Background**: Personalized context from your profile
  - **Custom Prompts**: Special instructions you set (e.g., "Always tell me how this affects India's IT sector")
  
  *Example: An AI engineer in Singapore asking about AI regulation in General Mode gets objective policy analysis. In Personal Mode, the same query includes: job market impact in Singapore, visa implications for foreign AI talent, local regulatory timeline, and specific actions they should take.*

### 💻 Multi-Tab Interface
- **Chat**: Converse with all 17 agents; ask follow-up questions, get instant citations
- **Local News**: Location-based news for your city/country with quick topic buttons
- **Collections**: Save & organize articles into custom collections (Favorites, Reading List, etc.)
- **Search History**: Browse and replay past searches
- **Settings**: Customize all preferences, language, interests, and custom prompts
- **Profile**: Manage your personal information for better personalization
- **Admin Panel** (for admins): User management, analytics, system monitoring

### 🎯 User Preferences & Customization
- **Profile Management**: Full name, occupation, bio, phone, gender, date of birth, website, social links
- **Interests & Topics**: Save unlimited custom topics and have news filtered to your preferences
- **Custom News Prompts**: Define special instructions (e.g., "Focus on India's perspective", "Include climate implications")
- **UI Theme**: Dark/light mode toggle
- **Results Per Page**: Customize how many articles appear per query
- **Smart Caching**: 2-minute response cache with query normalization (similar queries share results)
- **Search History**: Automatic tracking of all your searches
- **Saved Collections**: Organize articles into custom collections (Favorites, Reading List, etc.)

### 🌍 Multilingual Intelligence
- Search in English + native language simultaneously (50/50 bilingual mode)
- UI translations on-demand
- All agents respond in the user's preferred language
- Auto-translate toggle for news content

### 📊 Real-Time Analytics
- Sentiment distribution across articles
- Source diversity charts
- Trending topics extraction
- Category breakdown
- Article credibility scores displayed with each result
- Daily usage insights and search trends

### 🔐 Authentication & Guest Access
- Full auth flow with OTP verification
- Persistent sessions with cookie-based recovery
- Guest mode with configurable daily quotas
- Row-Level Security (RLS) enforced on all user data
- Password hashing with PBKDF2 + per-user salt

### 💾 Collections & Alerts
- Save articles to custom collections
- Topic-based alerts (instant, daily, weekly)
- JSON export of articles and collections

---

## 🧰 Tech Stack

| Layer | Technology |
|-------|-----------|
| **Orchestration** | LangGraph (directed state graph) |
| **LLM** | OpenAI: GPT-4o for QA agent (answer generation), GPT-4o-mini for all other agents (cost efficiency) |
| **Frontend** | Streamlit with custom CSS (glassmorphism dark theme) |
| **Database** | Supabase (PostgreSQL + Row-Level Security) |
| **Financial Data** | yfinance → Finnhub → FMP → Twelve Data → Polygon.io (5-tier fallback chain) |
| **Enrichment** | 5 parallel agents: Fact Check, Trend Context, Sentiment, Regional Impact, Source Bias |
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
| No context beyond headlines | **5 enrichment agents** add trend analysis, sentiment maps, regional impact, bias detection |

---

## 📝 License

This project is proprietary. All rights reserved.

---

<div align="center">

**Developed by Gahan Kumar Lal**

*17 AI agents. 5 search engines. 120+ trusted sources. One intelligent answer.*

</div>
