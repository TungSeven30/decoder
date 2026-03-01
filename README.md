# Decoder.

> *Because your partner won't stop talking about the internet.*

A weekly briefing site that translates the tech/finance/politics drama you live in real-time into plain English for your spouse. You track X minute-by-minute. Krystal doesn't. This bridges the gap.

---

## The Problem

You're terminally online — following every DeepSeek drop, every Musk meltdown, every $100B funding round as it happens. Krystal is a normal human being who has clients and children and a life.

The result: you reference "the xAI/SpaceX merger" and get a blank stare. You mention "NVIDIA's forward PE" and she's already tuned out. Not because she doesn't care — she just doesn't have 14 browser tabs open at all times.

**Decoder.** is the fix. A clean, searchable briefing updated weekly that explains:
- The week's biggest stories in plain English (no jargon)
- A running glossary of terms you keep using
- Context that makes the reference actually land

---

## What It Is

A single-page static website with:
- **"This Week's Drama"** — 10–15 expandable story cards, each with a one-liner + full plain-English explanation
- **Glossary** — 15–20 terms defined for a smart non-technical reader
- **Search** — filter both sections instantly
- **Dark mode** — because of course

---

## Vision: Making It Real

### Architecture

```
Alfred (OpenClaw)
    │
    ├── Monitors: X/Twitter (@0xHuman feed + curated lists)
    ├── Monitors: news feeds (TechCrunch, Bloomberg, The Verge, FT)
    │
    └── Weekly (Friday 6PM CST) → generates new edition
            │
            ├── Picks top 10-15 stories of the week
            ├── Writes plain-English summaries (Krystal-optimized)
            ├── Updates glossary with new terms
            ├── Injects into HTML template
            └── Deploys → Cloudflare Pages
```

### Content Pipeline

**Step 1 — Collection**
Alfred uses `xurl` to pull posts from curated X lists (AI, finance, tech drama) + scrapes key newsletters and news aggregators. Ranks by signal (retweets, quote tweets, engagement velocity).

**Step 2 — Selection**
Filter to stories that: (a) went noticeably viral, (b) are genuinely confusing without context, (c) Tùng actually referenced or would reference at dinner. 10–15 per week.

**Step 3 — Generation**
For each story, Alfred generates:
- One punchy sentence: what happened, who's involved, why it matters
- Full explanation (2–3 paragraphs): Written like explaining to a smart friend who doesn't follow tech Twitter. Conversational, no condescension, occasional humor.

New jargon from the week → new glossary cards.

**Step 4 — Inject & Deploy**
Python script injects content into HTML template → push to GitHub → Cloudflare Pages auto-deploys.

---

## File Structure

```
decoder/
├── index.html          ← The site (self-contained, no build step)
├── template.html       ← Base HTML for injection (no story content)
├── README.md
├── scripts/
│   ├── collect.py      ← Fetch stories from X, news, Reddit
│   ├── generate.py     ← Claude API → plain-English content
│   └── inject.py       ← Write generated content into template
└── data/
    ├── stories.json    ← Current week's stories (raw)
    ├── glossary.json   ← Running glossary (append-only)
    └── archive/        ← Previous weeks
```

---

## Content Principles

**Write for Krystal, not for CT.**
- She's a CPA. Smart, not technical. Not stupid — just not online.
- Explain every acronym the first time, every time.
- Use real-world analogies ("like if Pepsi rented Coca-Cola's bottling plant")
- Be a little funny. She'll appreciate it.
- Keep it punchy. No 1,000-word explainers.

**Story selection filter:**
- Would you actually say this at dinner? → Include
- Only CT-core would care? → Skip
- Generated genuine "wait, what?" moments? → Include
- Already stale? → Skip

**Tone:** Warm, friendly, slightly exasperated. A good friend in tech translating for their partner.

---

## Categories

| Tag | Covers |
|---|---|
| AI / Government | Policy, regulation, military AI |
| AI / Finance | Funding, valuations, M&A |
| AI / Culture | Viral AI moments, pop culture |
| Tech / Finance | Layoffs, earnings, company moves |
| Big Tech | Google, Meta, Apple, Amazon |
| Semiconductors | Chips, NVIDIA, TSMC, ASML |
| Finance / Markets | Stocks, macro, rates |
| Tech / Legal | Lawsuits, antitrust, regulation |
| Creator Economy | YouTubers + influencers doing business things |

---

## Deployment

**Target:** Cloudflare Pages (free, instant deploys from GitHub)
**Domain idea:** `decoder.tnguyen.ai` or `wtfdidisay.com`
**Cadence:** Weekly (Friday) + hot-drop when something truly insane happens mid-week

---

## Status

- [x] Design complete
- [x] Mock content live (Feb 27, 2026 edition)
- [ ] `collect.py` — story scraping pipeline
- [ ] `generate.py` — Claude content generation
- [ ] `inject.py` — HTML template injection
- [ ] GitHub repo + Cloudflare Pages deploy
- [ ] First automated edition

---

*Built by Alfred for Tùng × Krystal.*
