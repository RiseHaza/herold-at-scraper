[Herold At Scraper](https://apify.com/lexis-solutions/herold-at-scraper?fpr=data)

# Herold.at Business Directory Scraper

![banner](https://images.apifyusercontent.com/_bITXCyEH3HwcPmmXUrQ3vkAzk1n1X4pHDOout1zLRw/w:1800/cb:1/aHR0cHM6Ly9sZXhpcy1zb2x1dGlvbnMtYXBpZnkuZnJhMS5jZG4uZGlnaXRhbG9jZWFuc3BhY2VzLmNvbS9iYW5uZXJzL2hlcm9sZGF0LWF0LnBuZw.webp)

## 🔎 What does Herold.at Business Directory Scraper do

Our Herold.at Business Directory Scraper allows you to easily **extract business information from Austria's leading business directory**. The actor automatically crawls through Herold.at and extracts detailed business information based on your search criteria.

## 🧾 What data can the scraper extract

The scraper extracts comprehensive business information including:

- Business name and description
- Contact information (phone, email)
- Physical address
- Business category
- Opening hours
- Website URL (if available)
- Company logo URL
- Additional business details

## 💼 Use Cases

- **Lead Generation**: Build targeted lists of Austrian businesses for sales and marketing
- **Market Research**: Analyze business presence and distribution across Austrian regions
- **Competitive Analysis**: Track competitors and understand market positioning
- **Business Networking**: Find potential business partners or suppliers
- **Local SEO**: Gather business data for local SEO and directory submissions
- **Data Enrichment**: Enhance existing business databases with verified information

## 📖 How to use the Herold.at Scraper

1. [Create](https://console.apify.com/sign-up) a free Apify account
2. Open Herold.at Business Directory Scraper
3. Choose your input method:

- Enter search keywords (e.g., "restaurants wien")
- Provide specific URLs to scrape
4. Set the maximum number of results (optional)
5. Configure proxy settings if needed
6. Click "Start" and wait for the results
7. Download your data in JSON, XML, CSV, Excel, or HTML format

## 📥 Input Examples

The actor accepts two types of input:

Using `startUrls`:

```
{
  "startUrls": [
    { "url": "https://www.herold.at/gelbe-seiten/installateurnotdienst" } 
  ],
  "maxItems": 50,
  "proxyConfiguration": {
    "useApifyProxy": true,
    "groups": ["RESIDENTIAL"]
  }
}
```

Using `keyword`:

```
{
  "keyword": "installateurnotdienst",
  "maxItems": 50,
  "proxyConfiguration": {
    "useApifyProxy": true,
    "groups": ["RESIDENTIAL"]
  }
}
```

## 📤 Output Example

```
{
    "companyDetailUrl": "https://www.herold.at/gelbe-seiten/wien/Rg2ZK/b-gas-installateur-und-notdienst-vaillant-junkers-baxi-service/",
    "companyName": "B-GAS - Installateur & Notdienst + Vaillant, Junkers, Baxi Service",
    "companyDescription": "Ihr Spezialist von B-GAS Installateur, für Heizung, Sanitär, Wasserschäden und Abflussproblemen.24 Stunden für Wien, Niederösterreich u.-Burgenland.",
    "companyAddress": "1220 Wien",
    "companyPhone": "+43 1 2028556",
    "companyEmail": "office@b-gas.at",
    "companyWebsite": "https://www.installateur-bgas.at",
    "companyLogoUrl": "https://a.mktgcdn.com/p/6-lbjcGiS76vKEphcE1cmC4j_ytoxjSYWjlo9J4sBbk/600x600.jpg"
}
```

## ⚡️ Why use the Herold.at Scraper

- **Fast & Efficient**: Automatically handles pagination and data extraction
- **Easy to Use**: No coding knowledge required
- **Reliable**: Well-maintained and regularly updated
- **Flexible Output**: Multiple export formats available
- **API Integration**: Can be integrated with your existing systems

## 🔗 Integrations

Connect the scraper with various services through [Apify's integrations](https://apify.com/integrations):

- Make (Integromat)
- Zapier
- Slack
- Google Sheets
- Webhooks
- And [many more](https://docs.apify.com/integrations)

## 📝 Note on Scraping

This scraper extracts publicly available data from Herold.at. Please ensure your use of the data complies with Herold.at's terms of service and applicable laws and regulations. The data is provided for informational purposes only and may not be completely accurate or up-to-date.

---

## Need to scrape other business and marketplace websites

- Business & Real Estate 🏢

- [Redfin Scraper](https://apify.com/lexis-solutions/redfin-scraper)
- [Hemnet.se Scraper](https://apify.com/lexis-solutions/hemnet-se-scraper)
- Marketplace & E-commerce 🛒

- [Alibaba Scraper](https://apify.com/lexis-solutions/alibaba-scraper)
- [Wayfair Scraper](https://apify.com/lexis-solutions/wayfair-scraper)
- [Otto Scraper](https://apify.com/lexis-solutions/otto-scraper)

👀 Need help or custom features?

Lexis Solutions is a [certified Apify Partner](https://apify.com/partners/find). Contact us for support and customization options:

- [Email](mailto:scraping@lexis.solutions)
- [LinkedIn](https://www.linkedin.com/company/lexis-solutions)