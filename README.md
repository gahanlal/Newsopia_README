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
- **Cross-references claims** across Google, Bing, DuckDuckGo, NewsData.io, and GNews.io with title-similarity verification and credibility scoring against a database of **120+ trusted global outlets**
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
Added Signal Analysis and source verification:
- **120+ Trusted Outlets Database**: Cross-reference articles against verified sources
- **5-Signal Credibility Engine**: Source reputation, cross-referencing, AI verification, linguistic analysis, article structure
- **Signal Analysis**: Multi-signal credibility scoring with a single unified output

### Phase 5: Full 17-Agent Pipeline
Expanded from 3 domain agents to a complete intelligent pipeline:
- **LLM-Only Intent Router** — Pure LLM classification using Pydantic structured output (`IntentAnalysis` model). No regex, no keyword rules — the LLM decides intent (casual/question/analysis/comparison/follow_up/etc.) and which specialist agents to activate. Uses `gpt-4o-mini` with `with_structured_output()` for guaranteed schema compliance.
- **Search Optimization** — Engine-specific query variants for Google, Bing, DuckDuckGo, NewsData.io, GNews.io
- **Content Processing & Fetching** — Full article extraction, deduplication, relevance scoring
- **AI Summarization** — Parallel summaries with structured insights
- **3 Specialized Domain Agents** — Financial (with live stock data from 5 APIs), Global (geopolitical analysis), Social (public sentiment) — all run in parallel
- **Synthesis Engine** — Unifies multi-agent perspectives via LLM
- **5 Enrichment Agents** — Signal Analysis, trend analysis, sentiment mapping, regional impact, bias detection
- **Response Aggregation** — Structures final output
- **QA Agent** — Handles follow-ups and casual chat with full article content

System now automatically routes complex queries to the right agents and synthesizes their perspectives.

### Phase 6: Multi-Domain Knowledge Graph (Current)
Introduced a sophisticated knowledge graph engine connecting 11 domains with 44 weighted causal edges:

**The 11 Domains**: War, Finance, Energy, Geopolitics, Social, Tech, Health, Trade, Environment, Food, Economy

**How It Works:**
1. **Detects primary domain(s)** from your query using keyword matching and entity recognition
2. **Dynamic edge weight boosting** — When two domains co-appear in the same article, the edge between them gets boosted (+2 per co-occurrence, capped at +6). Recent articles (< 24h) get a 2× multiplier, making the graph responsive to breaking news.
3. **BFS traversal** to find 1-2 hop neighbors across related domains (e.g., War → Energy → Finance → Markets) using dynamically weighted edges
4. **Geographic entity layer** — Scans articles for 30 countries/regions (US, China, India, EU, Middle East, etc.) with demonyms, currencies, and capitals. Maps which countries appear alongside which domains.
5. **Blind-spot detection & autonomous search** — Identifies connected domains with zero article coverage, generates targeted search queries, and dispatches the web scraper to fill gaps automatically. Example: if War → Food has no articles, it searches "[query] food famine hunger" across Google, Bing, DDG, NewsData.io, and GNews.io.
6. **Cross-article entity extraction** — Regex-based NER (multi-word proper nouns, acronyms, known domain entities) with union-find clustering to group related articles
7. **LLM synthesis** — For complex graphs (3+ domains or blind spots), generates a Cross-Domain Intelligence Brief via GPT-4o-mini. Simple graphs use a deterministic rule-based synthesis to save API calls.

**Example:** Query: "How is the US-Iran conflict affecting defense stocks and oil futures?"
- **Domain detection:** War & Conflict (primary) → Finance & Markets, Energy, Geopolitics, Trade, Social (connected via BFS)
- **Dynamic weights:** War→Finance edge boosted from 8 to 14 because 6 articles mention both military action and market impact
- **Geographic layer:** Iran (12 mentions), US (15 mentions), Israel (8 mentions), Saudi Arabia (5 mentions)
- **Blind spots found:** Environment & Climate, Social & Domestic → autonomous search dispatched for both
- **Result:** 29 entities linked, 5 article clusters, 4 causal chains identified, 10 new articles added from blind-spot search

**The 44-Edge Ontology:** War DISRUPTS Energy (weight: 9), Energy INFLUENCES Finance (weight: 9), Trade AFFECTS Food (weight: 8), Geopolitics DRIVES Tech (weight: 7) — each with causal descriptions so the LLM reasons about **why** domains are connected, not just **that** they are.

### Phase 7: Sector-Aware Financial Intelligence (Current)
The Financial Impact Agent now understands **sector-level queries** — not just individual company names or tickers:

- **SECTOR_TICKER_MAP** (~60 entries) maps sector keywords to representative tickers:
  - "defense stocks" → LMT, RTX, NOC
  - "oil futures" → CL=F, XOM, CVX
  - "tech stocks" → AAPL, MSFT, NVDA
  - "banking stocks" → JPM, BAC, GS
  - "crypto" → BTC-USD, ETH-USD
  - And 55+ more sectors covering pharma, airlines, EVs, semiconductors, REITs, etc.

- **3-Tier extraction pipeline:**
  1. **Tier 1a:** Direct `$TICKER` pattern matching
  2. **Tier 1b:** Sector keyword matching against SECTOR_TICKER_MAP (before LLM)
  3. **Tier 2:** LLM extraction with structured rules for company names, sectors, and industries
  4. **Tier 3:** Fallback extraction checking both SECTOR_TICKER_MAP and COMPANY_TICKER_MAP (200+ companies)

- **5-API multi-tier data fetching** per symbol:
  1. **yfinance** (primary) — real-time price, fundamentals, technicals
  2. **Finnhub** merge — analyst recommendations, earnings, company news
  3. **FMP** merge — DCF valuation, financial ratios, institutional holders
  4. **Twelve Data** fallback — if yfinance fails
  5. **Polygon.io** fallback — if all above fail

- **Comprehensive stock data cards** include: price action (current, change, 52-week range), performance (1D/5D/1M/3M/6M/1Y), valuation (P/E, P/B, EV/EBITDA, DCF), technicals (SMA 20/50/200, RSI, MACD, Bollinger), fundamentals (revenue, margins, ROE, debt), analyst consensus, upcoming earnings, options activity, and institutional holders.

**Example:** "How is the US-Iran conflict affecting defense stocks?" → Sector match extracts LMT, RTX, NOC → yfinance fetches live prices → Finnhub merges analyst data + 5 news articles per stock → FMP merges DCF valuations → LLM analyzes with entry zones, price targets, and risk assessment.

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
    ①    │  Intent Router   │  Pure LLM classification — no regex/keywords.
         │  (LLM-only)      │  Pydantic structured output (IntentAnalysis).
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
       │  Web Scraper     │  Hits Google, Bing, DDG, NewsData, GNews
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
       │   data (5    │ │ • Diplomacy  │ │   opinion    │
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
| **Signal Analysis Agent** | Cross-references claims across sources, detects contradictions | Confidence score (0–100), verification labels (✅ High / ⚠️ Partial / ❌ Conflicting) |
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
| **Parallel agent execution** | Financial + Global + Social agents run simultaneously with 45s per-agent timeout and 75s global deadline. ~3× faster than sequential. |
| **Parallel enrichment layer** | 5 enrichment agents (Signal Analysis, Trend, Sentiment, Regional, Bias) run in parallel via ThreadPoolExecutor with 15s timeout. Non-blocking — failures are silently skipped. |
| **Parallel web scraping** | 3 search engines queried simultaneously. |
| **Dynamic summarizer scaling** | Worker pool scales from 4→8 based on article count. |
| **Response caching** | MD5-hashed cache with 2-min TTL and normalized query keys. Near-identical queries ("Apple stock today" vs "today apple stock") hit the same cache. |
| **Freshness-aware ranking** | Breaking/recent queries boost newer articles. Decay function: articles from 1h ago score 1.0, 24h → 0.5, 72h → 0.2. |
| **LLM-first routing** | Intent router uses pure LLM classification with Pydantic structured output — no regex rules. Simple queries skip LLM in QueryAnalyzer and SearchOptimizer. |
| **Graceful error recovery** | Every agent node is wrapped in try/except — one failing agent doesn't crash the pipeline. Multi-analysis tracks failed agents and proceeds with available results. |
| **Streaming output** | `stream_chat_search()` yields tokens progressively for real-time UI feedback. |
| **GPT-4o-mini across all agents** | All agents (intent router, financial, global, social, QA) use gpt-4o-mini for cost efficiency. QA agent has max_tokens=2000 for detailed answers. |

---

## 🔍 Signal Analysis & Credibility Engine

Every article can be analyzed by the **Fake News Detector**, which runs 5 independent signals:

| Signal | Weight | Method |
|--------|--------|--------|
| **Source Credibility** | 25% | Article domain checked against 120+ trusted outlets and known-unreliable database |
| **Cross-Reference** | 25% | Parallel search across Google, Bing, DuckDuckGo, NewsData.io, and GNews.io with title-similarity scoring |
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
| **LLM** | OpenAI GPT-4o-mini for all agents (intent routing, financial analysis, QA answers, synthesis). Pydantic structured output for intent classification. |
| **Frontend** | Streamlit with custom CSS (glassmorphism dark theme) |
| **Database** | Supabase (PostgreSQL + Row-Level Security) |
| **Financial Data** | yfinance → Finnhub → FMP → Twelve Data → Polygon.io (5-tier fallback chain) |
| **Enrichment** | 5 parallel agents: Signal Analysis, Trend Context, Sentiment, Regional Impact, Source Bias |
| **Web Scraping** | BeautifulSoup + requests (parallel, multi-engine) |
| **Caching** | In-memory with MD5 keys + normalized queries |
| **Deployment** | Streamlit Cloud / any Python host |

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

*17 AI agents. 5 search engines. 5 financial APIs. 11-domain knowledge graph. 120+ trusted sources. One intelligent answer.*

</div>
