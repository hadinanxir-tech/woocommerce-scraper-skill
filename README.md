# WooCommerce Product Scraper Skill

A reusable skill for pulling a store's public product catalog into a CSV file using only a store URL.

This project is designed for public WooCommerce stores and best-effort scraping. Many WooCommerce stores require API authentication or a login to expose all product data, so the script tries public API endpoints and public HTML pages first, then exports results as CSV.

## Features

- Accepts a WooCommerce storefront URL
- Tries public WooCommerce JSON endpoints
- Falls back to product pages and HTML parsing
- Exports all discovered products to CSV
- Avoids requiring API keys when the storefront exposes public data

## Important note

This tool is intended for public data only. If the store restricts access or requires WooCommerce API credentials, the script will not be able to list all products without proper authentication.

## Project structure

- `scraper.py` — main scraper entry point
- `skill_definition.json` — machine-readable skill definition for AI usage
- `requirements.txt` — Python dependencies
- `README.md` — usage docs

## Setup

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## Usage

```bash
python scraper.py https://example.com --output products.csv
```

Optional flags:

```bash
python scraper.py https://example.com \
  --output products.csv \
  --max-pages 10 \
  --verbose
```

## Output columns

The CSV includes rows like:

- `id`
- `name`
- `slug`
- `url`
- `price`
- `regular_price`
- `sale_price`
- `stock_status`
- `sku`
- `categories`
- `image_url`
- `short_description`
- `description`

## Example

```bash
python scraper.py https://store.example.com --output products.csv
```

This will create a file named `products.csv` in the current directory.

## Notes

- Public WooCommerce API endpoints may return JSON only if the site allows unauthenticated access.
- Product pages often include product metadata inside HTML and JSON-LD scripts.
- Some stores render products via JS; in that case, a browser automation stack may be needed.

## License

MIT
