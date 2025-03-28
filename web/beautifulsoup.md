# BeautifulSoup Cheat Sheet

## Installation

```bash
pip install beautifulsoup4 lxml
```

## Basic Usage

```python
from bs4 import BeautifulSoup

html = "<html><body><h1>Hello</h1></body></html>"
soup = BeautifulSoup(html, "lxml")
```

## Load from File

```python
with open("page.html") as f:
    soup = BeautifulSoup(f, "lxml")
```

## Load from URL

```python
import requests
from bs4 import BeautifulSoup

url = "https://example.com"
res = requests.get(url)
soup = BeautifulSoup(res.text, "lxml")
```

## Accessing Tags

```python
soup.title              # <title> tag
soup.title.name         # "title"
soup.title.string       # "Hello"
soup.h1.text            # "Hello"
```

## Finding Elements

```python
soup.find("h1")                         # First <h1>
soup.find_all("a")                     # All <a> tags
soup.find(id="main")                   # By ID
soup.find(class_="button")             # By class
soup.find_all("div", class_="box")     # Tag + class
```

## CSS Selectors

```python
soup.select("div.box")                 # <div class="box">
soup.select_one("#main")              # ID selector
soup.select("ul > li")                # Direct children
```

## Tag Attributes

```python
tag = soup.find("a")
tag["href"]                           # Get href
tag.get("href")                       # Same as above
```

## Navigating DOM Tree

```python
tag.parent
tag.children
tag.contents
tag.next_sibling
tag.previous_sibling
```

## Modify HTML

```python
tag = soup.find("p")
tag.string = "Updated text"
```

## Add New Tag

```python
new_tag = soup.new_tag("a", href="https://example.com")
new_tag.string = "Link"
soup.body.append(new_tag)
```

## Remove Element

```python
tag = soup.find("script")
tag.decompose()   # Completely remove from tree
```

## Get Text

```python
text = soup.get_text()
text = soup.get_text(strip=True)
```

## Extract Links

```python
for a in soup.find_all("a", href=True):
    print(a["href"])
```

## Save to File

```python
with open("output.html", "w") as f:
    f.write(str(soup))
```

## Parser Options

```python
# Other parsers
BeautifulSoup(html, "html.parser")     # Built-in
BeautifulSoup(html, "lxml")            # Fast and lenient
BeautifulSoup(html, "html5lib")        # Closest to browser
```
