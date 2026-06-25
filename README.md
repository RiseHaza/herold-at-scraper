[Herold At Scraper](https://apify.com/santamaria-automations/herold-at-scraper?fpr=data)

# Herold.at Scraper

Scrape business listings from [herold.at](https://www.herold.at), Austria's Yellow Pages with 360K+ businesses.

## Features

- **Phone + email on SERP** — Direct `tel:` and `mailto:` links, no detail page needed
- **~30 results per page** with automatic pagination
- **Austrian address parsing** — 4-digit postal codes + city names
- **Optional detail pages** — Website URLs, opening hours, geo coordinates, company details
- **Qwik JSON extraction** — Structured data from herold.at's Qwik framework (rating, industries, founding year, keywords)
- **Social media links** — Facebook, Instagram, LinkedIn, Xing, YouTube via vCard + HTML parsing
- **HTTP-only** — Low memory (~128MB), fast execution
- **Pay-per-result** pricing via Apify billing events

## Use with AI Agents (MCP)

Connect this actor to any MCP-compatible AI client — Claude Desktop, Claude.ai, Cursor, VS Code, LangChain, LlamaIndex, or custom agents.

**Apify MCP server URL:**

```
https://mcp.apify.com?tools=santamaria-automations/herold-at-scraper
```

**Example prompt once connected:**

> "Use `herold-at-scraper` to scrape company data from herold at. Return results as a table."

Clients that support dynamic tool discovery (Claude.ai, VS Code) will receive the full input schema automatically via `add-actor`.

## Input

| Field | Type | Default | Description |
| --- | --- | --- | --- |
| `keyword` | string | required | Business type (e.g., "Elektriker", "Restaurant") |
| `location` | string | optional | City/region (e.g., "Wien", "Salzburg"). Empty = all Austria |
| `maxResults` | number | 100 | Maximum results to scrape |
| `includeDetails` | boolean | false | Fetch detail pages for website/hours/geo |
| `proxyConfiguration` | object | Apify proxy | Proxy settings |

## Output Fields

### From SERP (always available)

- `name` — Business name
- `phone` — Phone number (directly from SERP!)
- `email` — Email address (directly from SERP!)
- `address` — Full address
- `city`, `postal_code` — Address components
- `category` — Business category
- `detail_url` — Link to detail page
- `logo_url` — Business logo image URL (from SERP listing)

### From Detail Page (when `includeDetails=true`)

- `website` — Business website URL
- `opening_hours` — Business hours
- `description` — Business description (from Qwik JSON or meta tags)
- `latitude`, `longitude` — Geo coordinates
- `logo_url` — Business logo image URL (higher quality from Qwik JSON)
- `social_links` — Social media profiles as `{ facebook: "url", instagram: "url", ... }`
- `branches` — Comma-separated industry names (primary + secondary industries)
- `rating_score` — Average rating (0-5 scale)
- `rating_count` — Number of reviews
- `founding_year` — Company founding year
- `company_register_id` — Austrian company register number (Firmenbuchnummer)
- `ksv_url` — KSV1870 credit check link
- `keywords` — Comma-separated business keywords

## Pricing Events

| Event | Price |
| --- | --- |
| `directory-start` | $0.05 |
| `directory-serp-result` | $0.003 |
| `directory-detail-result` | $0.005 |

## Enrichment add-ons

After the scrape completes, this actor can automatically trigger AI-powered extraction on every website found in the results. Each add-on runs as a separate actor and produces its own dataset.

### Contact extraction

Extracts team member names, email addresses, phone numbers, positions, and departments from company websites. Powered by the [Website Contact Extractor](https://apify.com/santamaria-automations/website-contact-extractor).

Enable it by setting `enableContactExtraction: true` and providing at least one LLM API key. The sub-actor run ID is stored in the key-value store as `CONTACT_EXTRACTOR_RUN_ID`.

### Job listing extraction

Extracts open positions, job titles, locations, departments, and career page URLs from company websites. Powered by the [Website Job Extractor](https://apify.com/santamaria-automations/website-job-extractor).

Enable it by setting `enableJobExtraction: true` and providing at least one LLM API key. The sub-actor run ID is stored in the key-value store as `JOB_EXTRACTOR_RUN_ID`.

### Browser fallback

Some company websites are built with JavaScript frameworks (React, Vue, Angular) that require a full browser to render. When `enableBrowserFallback` is set to `true`, the contact/job extractors will automatically re-scrape these sites with Playwright. This catches ~25% more sites but increases cost and runtime. Only applies when contact or job extraction is enabled.

### LLM API keys

Both add-ons use LLMs to extract structured data. Provide one or more API keys. When multiple keys are provided, the system uses them in priority order with automatic fallback:

1. **Gemini** (recommended) -- Best quality-to-cost ratio. Free tier includes 1M tokens/min. Get a key at [Google AI Studio](https://aistudio.google.com/app/apikey).
2. **Groq** (optional) -- Ultra-fast inference. Get a key at [Groq Console](https://console.groq.com/keys).
3. **OpenRouter** (optional) -- Access to 100+ models. Get a key at [OpenRouter](https://openrouter.ai/keys).

One key is sufficient. With multiple keys, if the primary provider hits a rate limit, the system falls back to the next available provider automatically.

## Related Actors

**DACH Business Directories**

- [FirmenABC.at Scraper](https://apify.com/santamaria-automations/firmenabc-at-scraper) -- Austrian business directory
- [Gelbe Seiten Scraper](https://apify.com/santamaria-automations/gelbeseiten-de-scraper) -- German Yellow Pages
- [wlw.de Scraper](https://apify.com/santamaria-automations/wlw-de-scraper) -- German B2B supplier directory
- [Das Oertliche Scraper](https://apify.com/santamaria-automations/dasoertliche-de-scraper) -- German phone directory
- [search.ch Scraper](https://apify.com/santamaria-automations/search-ch-scraper) -- Swiss business directory
- [Europages Scraper](https://apify.com/santamaria-automations/europages-scraper) -- 30+ European countries

**Swiss Company Data**

- [Zefix.ch Scraper](https://apify.com/santamaria-automations/zefix-ch-scraper) -- Official Swiss commercial register
- [Moneyhouse.ch Scraper](https://apify.com/santamaria-automations/moneyhouse-ch-scraper) -- Swiss company registry

**Enrich your leads**

- [Website Email & Phone Scraper](https://apify.com/santamaria-automations/website-email-scraper) -- Extract emails and phones from company websites
- [Website Contact Extractor](https://apify.com/santamaria-automations/website-contact-extractor) -- Extract team members and decision-makers
- [Google Maps Scraper](https://apify.com/santamaria-automations/google-maps-scraper) -- Find businesses by location
- [Trustpilot Reviews Scraper](https://apify.com/santamaria-automations/trustpilot-scraper) -- Get company reviews and ratings

## Support

Found a bug or have a feature request? [Open an issue](https://console.apify.com/actors/vaFLVihPSgf3tdbKs/issues).