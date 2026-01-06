# Python RegEx

Regular expressions for pattern matching in strings.

## re Module

```python
import re
```

## Search

```python
import re

text = "The rain in Spain"
match = re.search("Spain", text)

if match:
    print("Match found")
```

## findall()

```python
text = "The rain in Spain"
matches = re.findall("ai", text)
print(matches)  # ['ai', 'ai']
```

## split()

```python
text = "The rain in Spain"
result = re.split("\s", text)
print(result)  # ['The', 'rain', 'in', 'Spain']

# Limit splits
result = re.split("\s", text, 1)
# ['The', 'rain in Spain']
```

## sub()

Replace matches:

```python
text = "The rain in Spain"
result = re.sub("\s", "-", text)
print(result)  # The-rain-in-Spain

# Limit replacements
result = re.sub("\s", "-", text, 2)
# The-rain-in Spain
```

## Match Object

```python
import re

text = "The rain in Spain"
match = re.search(r"\bS\w+", text)

if match:
    print(match.span())   # (12, 17) - position
    print(match.string)   # The rain in Spain
    print(match.group())  # Spain - matched text
```

## Metacharacters

```python
[]   # Set of characters [a-z]
\    # Escape special character
.    # Any character (except newline)
^    # Starts with
$    # Ends with
*    # 0 or more occurrences
+    # 1 or more occurrences
?    # 0 or 1 occurrence
{}   # Exact number {2,4}
|    # Either or
()   # Capture group
```

## Special Sequences

```python
\d  # Digit [0-9]
\D  # Non-digit
\s  # Whitespace
\S  # Non-whitespace
\w  # Word character [a-zA-Z0-9_]
\W  # Non-word character
\b  # Word boundary
\B  # Not word boundary
```

## Examples

```python
import re

# Email validation
email = "user@example.com"
pattern = r'^[a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+\.[a-zA-Z0-9-.]+$'
if re.match(pattern, email):
    print("Valid email")

# Phone number
phone = "123-456-7890"
pattern = r'^\d{3}-\d{3}-\d{4}$'

# Extract numbers
text = "Price: $50, Discount: $10"
numbers = re.findall(r'\d+', text)
print(numbers)  # ['50', '10']

# Replace
text = "Call me at 123-456-7890"
result = re.sub(r'\d', 'X', text)
# Call me at XXX-XXX-XXXX
```

---

**Related:** [[Python Strings]] | [[Python]] | [[Python String Formatting]]
