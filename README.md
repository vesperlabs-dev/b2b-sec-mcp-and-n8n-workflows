# Vesper Labs — SEC EDGAR MCP Server & B2B Signal Automation Suite

![Vesper Labs Banner](./assets/banner.png)

Deterministic, sub-second **Model Context Protocol (MCP)** tools and **n8n / Make / Clay** data pipelines for **SEC EDGAR financial disclosures**, **Multi-ATS hiring intent signals**, **Shopify tech-stack intelligence**, **SaaS competitor churn reviews**, and **live DNS MX-verified contact enrichment**.

---

## 🔌 Quickstart: Connect Claude Desktop, Cursor, or Windsurf to Live SEC EDGAR (`/mcp`)

Our **Standby Streamable HTTP MCP Server** (`2025-03-26`) connects directly to official US SEC EDGAR (`data.sec.gov`) and live DNS infrastructure with zero local Python/Docker setup.

Add [`mcp/claude_desktop_config.json`](./mcp/claude_desktop_config.json) (or `.cursor/mcp.json`):

```json
{
  "mcpServers": {
    "vesper-sec-edgar-b2b": {
      "url": "https://vesper26--sec-edgar-filings-mcp-server.apify.actor/mcp",
      "headers": {
        "Authorization": "Bearer <YOUR_APIFY_API_TOKEN>"
      }
    }
  }
}
```

### Exposed MCP Tools
| Tool Name | What It Returns | Latency |
| :--- | :--- | :--- |
| `get_sec_company_filings` | Live `10-K`, `10-Q`, `8-K`, `Form 4` insider transactions, `13F-HR`, and `S-1` filings + direct `sec.gov/Archives` document URLs | ~250ms |
| `get_sec_xbrl_financials` | Latest audited USD `Revenue`, `Net Income`, `Operating Income`, `Cash`, `Total Assets`, `Total Liabilities`, and `R&D` from SEC XBRL `CompanyFacts` | ~300ms |
| `verify_company_domain_dns` | Real-time DNS `MX` & `SPF` mail-provider fingerprinting (`Google Workspace`, `Microsoft 365`, `Proofpoint`, `Mimecast`) | ~120ms |

---

## 🚀 Live Data Endpoints & Actors (Apify Store)

All five Actors run pure deterministic Node.js (zero LLM hallucination, zero residential proxy bloat) and support **Agentic Payments**:

1. **[SEC EDGAR Filings, Financials & Insider Trades MCP Server](https://apify.com/vesper26/sec-edgar-filings-mcp-server)** — Batch SEC filing extractor + live `/mcp` server (`$1.50 / 1k items`).
2. **[B2B Verified Contact & Decision-Maker Email Enricher](https://apify.com/vesper26/b2b-verified-contact-scraper)** — Cloudflare `data-cfemail` decoding, `/team` & JSON-LD leadership extraction, live MX/SPF verification, and executive email permutations (`$2.00 / 1k domains`).
3. **[Multi-ATS Career Site Jobs & B2B Hiring Signals](https://apify.com/vesper26/ats-hiring-signal-scraper)** — Direct Greenhouse, Ashby, and Lever job feeds with normalized USD compensation and B2B budget tags (`$0.80 / 1k jobs`).
4. **[SaaS & Shopify App Reviews + B2B Churn Signal Scraper](https://apify.com/vesper26/saas-reviews-churn-signal-scraper)** — Extracts 1–3★ Shopify & Apple App Store reviews with merchant store names, tenure, and churn reason tags (`$1.20 / 1k reviews`).
5. **[Shopify Store Products, Pricing, Stock & Tech-Stack Scraper](https://apify.com/vesper26/shopify-store-intelligence-scraper)** — Detects `myshopify.com` domain, active theme, installed marketing apps/pixels (`Klaviyo`, `Gorgias`, `Recharge`), and live variant stock (`$0.90 / 1k items`).

---

## ⚡ Free Ready-to-Import `n8n` Workflow Blueprints

All three production n8n pipelines are included **free** right in [`examples/`](./examples/) — just import into n8n and plug in your Apify API token (`HTTP Header Auth` → `Authorization: Bearer <YOUR_APIFY_API_TOKEN>`):

1. **[Shopify Competitor Churn → Tech Stack & Verified Contacts](./examples/01-shopify-competitor-churn-to-verified-contacts.json)** *(21 nodes · also live on [n8n.io/workflows/22650](https://n8n.io/workflows/22650))* — Daily scan of 1–2★ competitor Shopify App Store reviews (`vesper26/saas-reviews-churn-signal-scraper`), parallel Shopify tech-stack fingerprinting (`vesper26/shopify-store-intelligence-scraper`) + DNS MX-verified executive enrichment (`vesper26/b2b-verified-contact-scraper`), 0–100 intent scoring, Slack alerts, and Google Sheets CRM upsert.
2. **[Multi-ATS Hiring Buying Signals → Executive Outreach CRM](./examples/02-ats-hiring-intent-to-executive-emails.json)** *(16 nodes)* — Scans Greenhouse, Ashby, and Lever job feeds (`vesper26/ats-hiring-signal-scraper`) for high-budget B2B signals (`$180k+` roles, security/AI/GTM spend), deduplicates jobs, enriches MX-verified C-suite/VP emails (`vesper26/b2b-verified-contact-scraper`), alerts Slack, and upserts to Google Sheets.
3. **[SEC EDGAR Form 4 Insider Trades, 8-K & 10-K Executive Monitor](./examples/sec-edgar-insider-alert-starter.json)** *(14 nodes)* — Polls `vesper26/sec-edgar-filings-mcp-server` every 6 hours for your ticker watchlist, deduplicates accession numbers, routes urgent `Form 4` / `8-K` disclosures + audited XBRL `$B`/`$M` metrics to Slack, and archives every filing to Google Sheets.

---

## ⚖️ Acceptable Use & Compliance
All tools operate strictly as ephemeral, user-directed utilities querying publicly accessible web metadata, public DNS records, and public-domain U.S. SEC EDGAR disclosures. Vesper Labs maintains zero centralized databases of personal information. End users act as independent Data Controllers responsible for GDPR, UK GDPR, CCPA, and CAN-SPAM compliance, and SEC data is provided strictly for informational research (not investment advice).
