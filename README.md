[Herold At Scraper](https://apify.com/abotapi/herold-at-scraper?fpr=data)

# Herold.at Scraper, Austrian Yellow Pages Listings

Scrape company listings from **herold.at**, the largest Austrian directory portal, into a clean structured dataset. Pull names, full addresses, GPS coordinates, telephone numbers, emails, websites, ratings, reviews, opening hours, payment methods, and founding dates, for any category in any Austrian city or region.

Use it to build local lead lists, enrich CRM records with verified contacts, monitor competitor coverage by region, or feed a directory aggregator. Two start modes (search-builder and URL-paste) and forward auto-pagination keep large pulls effortless.

## Why This Scraper?

- **Full contact info on every listing without `fetchDetails`**: name, street address, postal code, city, region, telephone, email, website, rating, verified status, logo, branch code (~17 fields). The detail toggle adds GPS, opening hours, payment methods, founding date, reviews, and description (~25 fields total).
- **Two start modes**, pick categories and locations through the input panel, or paste any herold.at SERP URL straight from your browser
- **Multi-search batching**, categories × locations cartesian product in one run
- **Forward auto-pagination**, walks `/seite/N/` until the limit is reached
- **Detail enrichment toggle**, SERP-only happy path is fast and cheap (already includes street address, phone, email, website, rating); turn on `fetchDetails` to add GPS coordinates, opening hours, payment methods, founding date, and reviews
- **Resilient pagination**, picks up the page number from any pasted URL and walks forward
- **Post-fetch filters**, `verifiedOnly`, `ratedOnly`, `minRating` apply client-side without breaking the URL grammar

## Data You Get

> Sample shape, values are illustrative placeholders, not from a live listing.

The "Source" column shows where each field comes from. **SERP** fields are always populated (every run). **Detail** fields require `fetchDetails: true` and add ~30× the request count per page.

| Field | Source | Example | Notes |
| --- | --- | --- | --- |
| `id` | SERP | `"00000"` | 5-char herold.at branch code |
| `url` | SERP | `"https://www.herold.at/gelbe-seiten/wien/00000/sample-company/"` | Detail page URL |
| `name` | SERP | `"Sample Company"` | Company name |
| `category` | SERP | `"restaurant"` | Category slug from input or inferred from URL |
| `regionSlug` | SERP | `"wien"` | Location slug from URL path |
| `position` | SERP | `1` | Position in original SERP |
| `isVerified` | SERP | `true` | "Verifiziert" badge present on SERP card |
| `streetAddress` | SERP | `"Sample Street 1"` | Hidden popover on each card (always present) |
| `postalCode` | SERP | `"1010"` | Visible address line |
| `addressLocality` | SERP | `"Wien"` | City |
| `addressRegion` | SERP | `"Wien"` | Federal state |
| `addressCountry` | SERP | `"AT"` | Always "AT" |
| `telephone` | SERP | `"+43 1 0000000"` | International format, from `tel:` link in popover |
| `email` | SERP | `"contact@example.com"` | From `mailto:` link in popover (when company supplied one) |
| `website` | SERP | `"https://example.com"` | External link in popover (when company supplied one) |
| `logoUrl` | SERP | `"https://images.herold.at/optimize?url=...&width=320"` | Logo image (some categories show an icon instead) |
| `primaryImage` | SERP | `"https://images.herold.at/..."` | First image (logo or hero) |
| `ratingValue` | SERP | `4.8` | Average rating (1-5) |
| `ratingCount` | SERP | `42` | Number of ratings |
| `bestRating` | SERP | `5` | Rating scale max |
| `worstRating` | SERP | `1` | Rating scale min |
| `branchCode` | SERP | `"00000"` | Same as id, exposed for downstream joins |
| `latitude` | Detail | `48.0000` | Geo coordinate |
| `longitude` | Detail | `16.0000` | Geo coordinate |
| `imageCount` | Detail | `1` | Number of detail-page images |
| `foundingDate` | Detail | `"2020"` | When the company was founded |
| `paymentAccepted` | Detail | `["Cash", "Card"]` | Accepted payment methods |
| `openingHours` | Detail | `[{ "day": "Monday", "opens": "09:00", "closes": "18:00" }]` | When the company supplied them |
| `reviewCount` | Detail | `12` | Number of detailed reviews |
| `reviews` | Detail | `[{ "author": "Sample Reviewer", "body": "Sample review text.", "rating": 5, "datePublished": "2026-01-01" }]` | Detailed review list |
| `description` | Detail | `"Sample seller description text appears here when fetchDetails=true."` | Company-supplied description text under the "Beschreibung" heading |
| `breadcrumb` | Detail | `["Home", "Wien", "Restaurant"]` | Category breadcrumb |
| `services` | Detail | `["Gastronomie", "Internationale Küche", "Gastgarten"]` | Tag chips from the Leistungen section (cuisine, amenities, special services) |
| `branchen` | Detail | `[{"name": "Restaurant", "slug": "restaurant"}, {"name": "Bierlokale-Pubs", "slug": "bierlokale-pubs"}]` | Company-specific industry memberships, populated from "Sie finden dieses Unternehmen in den Branchen" |
| `scrapedAt` | runtime | `"2026-01-01T00:00:00.000Z"` | ISO timestamp of when this record was extracted |

## How to Use

### Search mode, single category in Vienna (fast, SERP-only)

```
{
  "mode": "search",
  "categories": ["restaurant"],
  "locations": ["wien"],
  "maxPages": 5,
  "maxListings": 100
}
```

### Search mode, multi-category × multi-location with detail enrichment

```
{
  "mode": "search",
  "categories": ["elektriker", "installateur"],
  "locations": ["wien", "graz", "linz"],
  "fetchDetails": true,
  "maxPages": 3,
  "maxListings": 200
}
```

### Search mode, Austria-wide for a category (no location filter)

```
{
  "mode": "search",
  "categories": ["zahnarzt"],
  "locations": [],
  "maxPages": 10
}
```

### URL mode, paste prepared URLs

```
{
  "mode": "url",
  "urls": [
    "https://www.herold.at/gelbe-seiten/wien/restaurant/",
    "https://www.herold.at/gelbe-seiten/graz/elektriker/"
  ],
  "maxPages": 5,
  "maxListings": 100
}
```

### Search mode with post-filters (verified, rated 4+ stars)

```
{
  "mode": "search",
  "categories": ["frisör"],
  "locations": ["wien"],
  "verifiedOnly": true,
  "ratedOnly": true,
  "minRating": 4,
  "maxListings": 50
}
```

## Input Parameters

| Parameter | Type | Default | Description |
| --- | --- | --- | --- |
| `mode` | enum `search`/`url` | `search` | Pick search-builder or URL-paste mode |
| `categories` | string[] | `["restaurant"]` | Category URL slugs, e.g. `restaurant`, `elektriker`, `zahnarzt` |
| `locations` | string[] | `["wien"]` | Austrian location slugs, e.g. `wien`, `graz`, `linz`. Empty = Austria-wide |
| `verifiedOnly` | boolean | `false` | Keep only "Verifiziert" listings (post-filter) |
| `ratedOnly` | boolean | `false` | Keep only listings with at least one rating (post-filter) |
| `minRating` | integer 1-5 | (none) | Drop listings below this average rating (post-filter) |
| `urls` | string[] | example URL | Full herold.at URLs (URL mode only) |
| `maxPages` | integer | `2` | Max SERP pages to walk per search |
| `maxListings` | integer | `0` | Total cap across all searches; `0` = unlimited |
| `fetchDetails` | boolean | `false` | Also fetch each listing's detail page (full address, phone, email, GPS, hours, reviews). Multiplies request count ~30× per page |
| `proxy` | object | Apify residential AT | Proxy configuration |

## Output Example

> Sample shape, values are illustrative placeholders, not from a live listing.

```
{
  "id": "00000",
  "url": "https://www.herold.at/gelbe-seiten/wien/00000/sample-company/",
  "name": "Sample Company",
  "category": "restaurant",
  "regionSlug": "wien",
  "position": 1,
  "isVerified": true,
  "breadcrumb": ["Home", "Gelbe Seiten", "Restaurant", "Wien"],
  "streetAddress": "Sample Street 1",
  "postalCode": "1010",
  "addressLocality": "Wien",
  "addressRegion": "Wien",
  "addressCountry": "AT",
  "latitude": 48.0000,
  "longitude": 16.0000,
  "telephone": "+43 1 0000000",
  "email": "contact@example.com",
  "website": "https://example.com",
  "logoUrl": "https://images.herold.at/optimize?url=...&width=320",
  "primaryImage": "https://images.herold.at/optimize?url=...&width=320",
  "imageCount": 1,
  "foundingDate": "2020",
  "branchCode": "00000",
  "paymentAccepted": ["Cash", "Card"],
  "openingHours": [
    { "day": "Monday", "opens": "09:00", "closes": "18:00" },
    { "day": "Tuesday", "opens": "09:00", "closes": "18:00" }
  ],
  "ratingValue": 4.8,
  "ratingCount": 42,
  "reviewCount": 12,
  "bestRating": 5,
  "worstRating": 1,
  "reviews": [
    { "author": "Sample Reviewer", "body": "Sample review text.", "rating": 5, "datePublished": "2026-01-01" }
  ],
  "description": "Sample seller description text appears here when fetchDetails=true.",
  "scrapedAt": "2026-01-01T00:00:00.000Z"
}
```

## Plan Requirement

- **Apify Free plan**: works for small runs but does not include residential proxy access, set the proxy field to your own proxy URLs if available.
- **Apify Starter plan and above**: includes Apify residential, set `proxy.apifyProxyGroups: ["RESIDENTIAL"]` and `proxy.apifyProxyCountry: "AT"` for stable Austrian routing. The default input prefill already does this.
- **Datacenter proxies**: usually work but may be rate-limited under load. Residential is recommended for any run with `maxListings > 200`.
- **Memory**: 256 MB default is sufficient for HTTP-only runs (peak ~80 MB).

## Finding category and location slugs

The simplest way to learn valid slugs is to browse herold.at in your browser and copy URL fragments:

- Visit `https://www.herold.at/gelbe-seiten/` and click any category, note the slug after `/gelbe-seiten/` (e.g. `restaurant`, `elektriker`).
- Open a SERP URL like `https://www.herold.at/gelbe-seiten/wien/restaurant/`, the first path segment is the location slug (`wien`).
- Pass `mode=url` and paste the URL directly if you prefer to skip the slug discovery.

## Known limitations

- **Not every city × category combination has a SEO page.** Herold only generates `/<location>/<category>/` URLs where there is enough listing volume. Wien, Salzburg, and Bregenz work for most popular categories; Graz, Linz, Innsbruck, and Klagenfurt usually return 404 even though those cities appear in detail-page addresses. When a combo 404s, the actor logs a warning and moves to the next search. To get coverage for those cities, omit `locations` (Austria-wide search) and post-filter the dataset by `addressLocality` or `regionSlug`.
- **`openedNow` filter is not supported.** Herold's "Jetzt geöffnet" toggle is a client-side JavaScript filter; the URL grammar does not carry it. To get currently-open listings, run with `fetchDetails: true` (which populates `openingHours`) and post-filter the dataset against the current Europe/Vienna time.
- **GPS, opening hours, reviews, payment methods, and founding date require `fetchDetails: true`.** SERP cards already include name, full street address, postal code, city/region, phone, email, website, logo, rating, and verified status, so most use cases work without detail fetching. Turning detail fetch on multiplies request count ~30× per page. Even on detail pages, fields like `description`, `openingHours`, and `website` are populated only when the company supplied them to Herold.