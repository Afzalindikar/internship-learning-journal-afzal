#  Week 4 – Session 1  
## APIs, Geocoding, and Data Extraction

---

# 1. Extracting Backend APIs Using Browser Tools

## Concept
Many modern websites load data using **hidden APIs** instead of static HTML.  
Instead of scraping the page, we can directly call these APIs.

## How to Find the API
1. Open **Developer Tools** → `F12`
2. Go to **Network Tab**
3. Trigger an action (search, click, scroll)
4. Inspect the **Request URL**

## API URL Structure

```
https://host/path?key=value&key2=value2
```

### Components
- **Host** → Server address  
- **Path** → API endpoint  
- **Query Parameters** → filters or inputs  

### Example

```
https://api.example.com/search?q=machine%20learning
```

## Fetching API Data with Python

```python
import requests

url = "API_URL"
response = requests.get(url)
data = response.json()
```

## Handling Broken / Wrapped JSON

Sometimes APIs return **invalid JSON**.

Steps:
1. Locate JSON start using `.find()`
2. Slice the valid portion
3. Parse using `json.loads()`

---

# 2️ Geocoding with Geopy (Nominatim)

## Concept
Geocoding converts:

```
Address ↔ Coordinates
```

Library used:

```
geopy
```

## Setup

```python
from geopy.geocoders import Nominatim

geo = Nominatim(user_agent="myapp")
```

 `user_agent` must be **lowercase and contain no spaces**

---

## Forward Geocoding

**Address → Coordinates**

```python
location = geo.geocode("IIT Madras")

print(location.latitude)
print(location.longitude)
```

---

## Reverse Geocoding

**Coordinates → Address**

```python
geo.reverse((13.0827, 80.2707))
```

---

## Batch Geocoding with Pandas

```python
import pandas as pd

df["location"] = df["address"].apply(geo.geocode)
```

---

## Handling Missing Values

Invalid address returns:

```
None
```

Example:

```python
lat = loc.latitude if loc else None
```

---

## Rate Limiting

Nominatim allows:

```
1 request per second
```

Solution:

```python
from geopy.extra.rate_limiter import RateLimiter

geocode = RateLimiter(geo.geocode, min_delay_seconds=1)
```

---

# 3️ Wikipedia Python Package

## Install

```bash
pip install wikipedia
```

---

## Search Topics

```python
import wikipedia

wikipedia.search("Artificial Intelligence")
```

---

## Get Summary

```python
wikipedia.summary("Python", sentences=2)
```

---

## Page Information

```python
page = wikipedia.page("Python")

page.title
page.url
page.images
page.references
```

---

# 4️ Scraping IMDb Using Browser JavaScript

Open **Developer Tools → Console**

## Select Movie Elements

```javascript
$$(".ipc-metadata-list-summary-item")
```

## Extract Data

```javascript
copy(
$$(".ipc-metadata-list-summary-item").map(item => [
item.querySelector(".ipc-title__text")?.textContent,
item.querySelector(".ipc-title-link-wrapper")?.href
])
)
```

---

## Functions Used

| Function | Purpose |
|--------|--------|
| `$$()` | querySelectorAll shortcut |
| `map()` | transform elements |
| `?.` | optional chaining |
| `copy()` | copy output to clipboard |

Convert result → **CSV / Excel**

---

# 5️ Web Scraping Dynamic Sites with Playwright

## Problem

`requests` cannot load **JavaScript rendered content**

## Solution

Use **Playwright**

### Install

```bash
pip install playwright
```

---

## Example

```python
from playwright.sync_api import sync_playwright

with sync_playwright() as p:
    browser = p.firefox.launch()
    page = browser.new_page()

    page.goto("https://example.com")
    html = page.content()
```

---

## Convert Tables to DataFrame

```python
import pandas as pd

df = pd.read_html(html)[0]
```

---

## Useful Playwright Features

### Screenshot

```python
page.screenshot(path="page.png")
```

### Wait

```python
page.wait_for_timeout(5000)
```

### Click

```python
page.click("button")
```

### Fill Forms

```python
page.fill("#username","user")
```

---

# 6️ Scraping PDFs and Extracting Tables

## Libraries Used

- **BeautifulSoup** → find PDF links  
- **Requests** → download PDFs  
- **Tabula** → extract tables  

---

## Download PDFs

```python
import requests
from bs4 import BeautifulSoup

response = requests.get(url)
soup = BeautifulSoup(response.text,"html.parser")

for link in soup.select("a[href$='.pdf']"):
    pdf = requests.get(link["href"])
```

---

## Extract Tables from PDF

```python
import tabula

tabula.convert_into(
    "file.pdf",
    "table.csv",
    output_format="csv",
    pages=18
)
```

---

# 7️ Converting Documents to Markdown (MarkItDown)

Microsoft tool to convert files → **Markdown**

## Supported Formats

- PDF
- Word
- PowerPoint
- Excel
- HTML
- JSON
- Images (OCR)

---

## Install

```bash
pip install markitdown
```

---

## Convert PDF

```python
from markitdown import MarkItDown

md = MarkItDown()
result = md.convert("file.pdf")

print(result.text_content)
```

---

# 8️ LLM-Based Website Scraping

LLMs can extract **structured data from messy webpages**

## Workflow

```
Fetch Webpage
      ↓
Convert HTML → Text
      ↓
Send to LLM
      ↓
Extract Structured Data
```

Example prompt:

```python
prompt = "Extract important data from this page"
```

Output → **JSON / CSV**

---

# 9️ Chrome Remote Debugging for Scraping

Used when a website requires **login session**

---

## Step 1: Launch Chrome in Debug Mode

```
chrome.exe --remote-debugging-port=9222
```

## Step 2

Login manually in the browser

## Step 3: Connect Using Playwright

```python
browser = p.chromium.connect_over_cdp("http://localhost:9222")
```

---

# 10 Scheduled Scraping with GitHub Actions

Run scrapers **automatically on schedule**

Example:

```yaml
on:
  schedule:
    - cron: "0 0 * * *"
```

Runs **daily at midnight (UTC)**

---

## Workflow Steps

1. Checkout repository
2. Run scraping script
3. Commit new data
4. Push updates

---

# 11 Open Data Processing Pipeline

Standard pipeline:

```
Fetch → Parse → Aggregate
```

## Fetch
Download raw data

## Parse
Convert data into structured format

## Aggregate
Combine datasets for analysis

---


