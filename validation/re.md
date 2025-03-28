# Python `re` (Regular Expressions) Cheat Sheet

## Importing

```python
import re
```

## Basic Functions

```python
re.match(pattern, string)       # match from start
re.search(pattern, string)      # match anywhere
re.findall(pattern, string)     # return all matches
re.finditer(pattern, string)    # return match objects
re.sub(pattern, repl, string)   # replace pattern
```

## Match Object

```python
m = re.search(r"\d+", "Item 42")
m.group()       # "42"
m.start()       # index of match
m.end()         # index after match
```

## Raw Strings

```python
pattern = r"\d+"  # use raw strings for regex
```

## Common Patterns

| Pattern | Description               | Example Match   |
|---------|---------------------------|-----------------|
| `.`     | Any character except `\n` | `a`, `1`, `#`   |
| `^`     | Start of string           | `^hello`        |
| `$`     | End of string             | `world$`        |
| `*`     | 0 or more                 | `a*` matches `aaa`, `a`, `` |
| `+`     | 1 or more                 | `a+` matches `a`, `aa` |
| `?`     | 0 or 1                    | `colou?r`       |
| `{n}`   | Exactly n                 | `\d{3}`         |
| `{n,}`  | n or more                 | `\d{2,}`        |
| `{n,m}` | Between n and m           | `\d{2,4}`       |
| `[]`    | Character class           | `[aeiou]`       |
| `[^]`   | Negated class             | `[^0-9]`        |
| `|`     | Or                        | `cat|dog`       |
| `()`    | Group                     | `(abc)+`        |
| `\d`    | Digit                     | `0-9`           |
| `\D`    | Non-digit                 |                 |
| `\w`    | Word character            | `a-zA-Z0-9_`    |
| `\W`    | Non-word character        |                 |
| `\s`    | Whitespace                | space, tab, \n  |
| `\S`    | Non-whitespace            |                 |

## Flags

```python
re.IGNORECASE or re.I    # case-insensitive
re.MULTILINE or re.M     # ^ and $ match each line
re.DOTALL or re.S        # . matches newline too
```

## Example Patterns

```python
email = r"\b[\w.-]+@[\w.-]+\.\w+\b"
phone = r"\(?\d{3}\)?[-.\s]?\d{3}[-.\s]?\d{4}"
url = r"https?://[\w./-]+"
ipv4 = r"\b(?:\d{1,3}\.){3}\d{1,3}\b"
date = r"\d{4}-\d{2}-\d{2}"
time = r"\d{2}:\d{2}(:\d{2})?"
username = r"^[a-zA-Z0-9_]{3,20}$"
```

## Substitution Example

```python
text = "My phone is 123-456-7890"
cleaned = re.sub(r"\D", "", text)
# Result: "1234567890"
```

## Greedy vs Non-Greedy

```python
greedy = re.search(r"<.*>", "<tag>value</tag>")       # matches entire string
non_greedy = re.search(r"<.*?>", "<tag>value</tag>")  # matches "<tag>"
```
