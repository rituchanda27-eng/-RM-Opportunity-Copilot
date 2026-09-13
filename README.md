# RM Opportunity Copilot

An n8n AI agent that scores a wealth manager's client book daily, flags which clients to call today and why, and auto-generates a polished PDF briefing with AI-written talking points.

## The Problem

Relationship Managers (RMs) at wealth management firms often manage dozens of high-net-worth clients with no systematic way to know who to prioritize calling on a given day. Opportunities like idle cash from maturing FDs, dangerous portfolio concentration, or underperformance vs. benchmark often go unnoticed until it's too late.

## The Approach

Rather than a generic AI chatbot, this agent targets a real, specific workflow problem:

1. **Deterministic scoring** — Every client is scored using five real signals: portfolio concentration risk, FD maturity timing, underperformance vs. benchmark, unused PMS/AIF eligibility, and relationship staleness. This logic is transparent and explainable, not a black-box AI guess.
2. **Selective AI use** — Only the top 5 highest-scoring clients get an AI-generated call script (via Groq's free-tier LLM API). This keeps token usage minimal and shows deliberate judgment about *where* AI adds value versus where plain logic is sufficient.
3. **Structured, decision-ready output** — Each client gets a priority tag (🔴 Urgent / 🟡 Monitor / 🟢 Stable), Indian-currency-formatted AUM, and a one-line daily summary — turning raw scores into something an RM can act on immediately.
4. **Real deliverable** — The workflow ends by rendering a clean, styled PDF report, not just a JSON blob.

## What's in this repo

- `rm_opportunity_copilot.json` — The full importable n8n workflow
- `mock_clients.csv` — Synthetic dataset of 20 sample HNI client portfolios used for testing
- `daily_rm_briefing.pdf` — Sample output: a generated daily briefing PDF

## How to run it

1. Import `rm_opportunity_copilot.json` into your own n8n instance (cloud or self-hosted)
2. Get a free API key from [Groq](https://console.groq.com) for the talking-points generation step
3. Get a free API key from [PDFMunk](https://pdfmunk.com) for PDF export
4. Add both keys as credentials in the corresponding nodes
5. Click "Execute Workflow" — the mock client data is already built into the workflow, no external file needed

## Why this design

Most people building for this space default to a client-facing chatbot. This project instead targets the advisor-facing side of the platform — the less obvious, more operationally valuable problem — and prioritizes a working, explainable prototype over a slide deck.
