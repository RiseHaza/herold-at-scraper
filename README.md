[Herold At Scraper](https://apify.com/fatihtahta/herold-at-scraper?fpr=data)

### **Slug:** `fatihtahta/herold-at-scraper`

## 1. Overview

Herold.At Scraper collects structured business details from Herold.at, Austria’s trusted yellow pages and local search directory. Use it to pull listings with contact information, ratings, descriptions, services, images, and location data so you can move straight to analysis instead of manual copy-paste. The actor is built for reliable automation, helping you save hours of repetitive work while keeping results consistent run after run.

## 2. Why Use This Actor

- **Market researchers & analysts:** Monitor local categories, compare competitors, and benchmark coverage across Austria.
- **Developers & data teams:** Feed clean business records into internal tools, dashboards, or enrichment pipelines.
- **Growth & sales teams:** Build targeted lead lists with phones, emails (when present), and location context for outreach.
- **Content & directory managers:** Refresh business directories or catalogs with up-to-date listings, services, and visuals.
- **Product & operations:** Track regional presence, ratings, and descriptions to inform expansion or quality checks.

Typical use cases include lead generation, market insights, location intelligence, directory building, and trend tracking—all without manual browsing.

## 3. Input Parameters

| Parameter | Type | Description | Default |
| --- | --- | --- | --- |
| `startUrls` | Array of strings | One or more Herold.at search, category, or individual listing URLs to scrape. | – |
| `queries` | Array of strings | Business type or search terms to run on Herold.at. | – |
| `location` | Array of strings | Optional city or region filters. Leave empty for nationwide coverage. | – |
| `limit` | Integer | Maximum listings to save per input. | `50000` |
| `proxyConfiguration` | Object | Connection settings for stable runs (defaults to Apify Residential proxy). | `{ "useApifyProxy": true, "apifyProxyGroups": ["RESIDENTIAL"] }` |

## 4. Example Input

```
{
  "startUrls": ["https://www.herold.at/gelbe-seiten/wien--2-leopoldstadt/restaurant/"],
  "queries": ["restaurant"],
  "location": ["Wien"],
  "limit": 200,
  "proxyConfiguration": {
    "useApifyProxy": true,
    "apifyProxyGroups": ["RESIDENTIAL"]
  }
}
```

## 5. Example Output

Each dataset item represents one business listing with key contact and profile fields.

```
{
  "title": "Gast: sarah.janisch",
  "detailUrl": "https://www.herold.at/gelbe-seiten/wien/MGPKb/gasthaus-moeslinger/",
  "snippet": "Genießen Sie österreichische Kulinarik im Restaurant im Stuwerviertel, direkt neben dem Wiener Prater in 1020 Wien. Der 1. Wiener AMA GenussWirt!",
  "phone": "+43 1 7280195",
  "email": "kontakt@gasthausmoeslinger.at",
  "website": "https://www.herold.at/firmeneintrag/?utm_source=herold_at&utm_medium=pre_header&utm_campaign=firmeneintrag_form",
  "verified": false,
  "position": 1,
  "ratingValue": 3,
  "ratingCount": 3,
  "sourceUrl": "https://www.herold.at/gelbe-seiten/wien--2-leopoldstadt/restaurant/",
  "addressText": "Stuwerstraße 14 1020 Wien Wien 2 (Leopoldstadt) Wien",
  "streetAddress": "Stuwerstraße 14",
  "postalCode": "1020",
  "addressRegion": "Wien",
  "addressCountry": "AT",
  "services": [
    "Gastronomie",
    "Vegetarische Küche",
    "Brunch",
    "Mittagsmenü",
    "Verkauf regionaler Schmankerl"
  ],
  "description": "Gasthaus Möslinger in 1020 Wien - Restaurant ✓ geprüfte Bewertungen, Telefonnummer, Öffnungszeiten, Adresse und mehr auf herold.at .",
  "branchCode": "MGPKb",
  "logoUrl": "https://a.mktgcdn.com/p/L8sNkojpNijLl6eBp9WA8N8fN4lhN5P4taYW8Df092I/600x600.jpg",
  "imageUrls": [
    "https://a.mktgcdn.com/p/3Qn-N4B3O0MxUwKbTlIJGSM1PT6XY-NRJC4AtJkXIEM/814x600.jpg",
    "https://a.mktgcdn.com/p/91i6_drF8snpSRZfOT6mchTN0bWX_b41UWYP7ISxx1Y/900x600.jpg",
    "https://a.mktgcdn.com/p/DdI67DDMBpSuDJJS5_nN7CpS_tQf0RbiR-OM-mEwxEU/900x600.jpg",
    "https://a.mktgcdn.com/p/Jdox5sm6-vAb_JyNoxwdDAeKedOvJKsppPETpoAjrpY/693x441.jpg",
    "https://a.mktgcdn.com/p/_maVNHeZOTetoIfqm5F7yEjnJTLRzL3lOMcjwcDKvcg/900x409.jpg",
    "https://a.mktgcdn.com/p/hdsMUEeIR5-hIiXl7YWcg2sBZGMF1N1_HnnssI-5PDQ/292x300.jpg",
    "https://a.mktgcdn.com/p/jm--EHOVYPav4EvFk3THl1B8PB0ba0WBQhnvXbKmYDg/900x600.jpg",
    "https://www.herold.at/FS/picture/9/1/2/5916219.jpg"
  ]
}
```

**Field highlights:** titles and URLs identify each listing; snippet, description, and services summarize the offering; phone, email, and website enable outreach; rating fields show on-site feedback; address data localizes each business; media URLs capture logos and gallery images.

## 6. Notes & Limitations

Use this actor responsibly. Always respect Herold.at’s terms of service and any applicable laws when collecting or using data. Ensure you have a valid basis for storing and processing business or personal information.

## 7. Support

Questions or custom needs? Open an issue on the **Issues** tab of the actor page in Apify Console and it will be resolved around the clock.

Happy Scraping,

- Fatih