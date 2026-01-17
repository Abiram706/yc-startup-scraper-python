# 🍊 Async YC Scraper

A robust, high-performance Python scraper designed to extract data for 500+ startups from the [Y Combinator Directory](https://www.ycombinator.com/companies). 

This project demonstrates a **hybrid scraping architecture**: combining browser automation (Playwright) for handling infinite scroll with asynchronous HTTP requests (aiohttp) for rapid data enrichment.

## 🚀 Key Features

* **Hybrid Architecture:** Uses `Playwright` for dynamic navigation and `aiohttp` for high-concurrency fetching.
* **Speed:** Scrapes detailed profiles of 500+ companies in under 2 minutes (approx. 20x faster than sequential scraping).
* **Robust Selectors:** Implements attribute-based selection (`href^="/companies/"`) to bypass YC's randomized CSS class names.
* **Data Enrichment:** Extracts Company Name, Batch, One-liner, Founder Names, and Founder LinkedIn URLs.
* **Clean Output:** Automatically handles missing data and exports to a formatted CSV.

## 🛠️ Tech Stack

* **Python 3.12+**
* **Playwright:** For handling JavaScript-heavy "Infinite Scroll" on the main directory.
* **aiohttp & asyncio:** For concurrent scraping of detail pages (scatter-gather pattern).
* **BeautifulSoup4:** For fast static HTML parsing.
* **Pandas:** For data structuring and CSV export.

## ⚙️ Logic & Architecture

The scraper operates in two distinct phases to maximize efficiency:



1.  **Phase 1 (The Scroll):** A headless browser navigates the directory, triggering the "Load More" JavaScript events until 500 unique links are collected. It uses robust attribute selectors to ignore dynamic CSS obfuscation.
2.  **Phase 2 (The Swarm):** The 500 links are fed into an asynchronous queue. `aiohttp` fetches the HTML for 20 pages simultaneously.
3.  **Phase 3 (The Parse):** `BeautifulSoup` extracts metadata (Founders, Batch, etc.) from the raw HTML, and `Pandas` writes the result to `yc_startups_500.csv`.

## 📦 Installation

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/yourusername/async-yc-scraper.git](https://github.com/yourusername/async-yc-scraper.git)
    cd async-yc-scraper
    ```

2.  **Install dependencies:**
    ```bash
    pip install playwright aiohttp pandas beautifulsoup4
    ```

3.  **Install Playwright browsers:**
    ```bash
    # Important: This installs the headless browser binaries
    playwright install chromium
    # OR if on Windows/PowerShell:
    python -m playwright install chromium
    ```

## 🏃 Usage

Run the main script:

```bash
python yc_scraper_v2.py
