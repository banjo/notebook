# Web Scraping with Requests and Beautiful Soup 4

## Getting started
Install tools:
```bash
pip install beautifulsoup4
pip install requests
pip install lxml
```

Import the tools:
```python
from bs4 import BeautifulSoup
import requests
```

## Get the page
### Get the page with requests
```python
result = requests.get("www.google.se")
```

### See status and headers:
```python
result.status_code
```
```python
result.headers
```

### Save for later use:
```python
content = result.content
```
### Make soup out of content:
```python
soup = BeautifulSoup(soup, features="lxml")
```

### EXTRA:
Prettify the soup:
```python
print(soup.prettify())
```

## Scrape with BS4

### Use select
Returns a list or a single element
```python
samples = soup.select("div > div:nth-child(4) > div:nth-child(4)")
```

### Use find_all
Return all elements with an a tag
```python
samples = soup.find_all("a")
```

Return all elements with a specific ID
```python
samples = soup.find_all(id="specific_id")
```

Return all elements with a "a" tag with a specific CSS class:
```python
samples = soup.find_all("a", class_="specific_css_class")
```

Search for any attribute within an a tag
```python
samples = soup.find_all("a", attrs={"class": "specific_css_class"})
```

### Use find
Works same as find_all, but returns a single element
```python
samples = soup.find("title")
```


## Get values

### Get inner text
```python
sample = element.get_text()
```

### Get href (or other attributes)
```python
sample = element.get("href")
```
