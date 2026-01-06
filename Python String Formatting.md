# Python String Formatting

Various ways to format strings in Python.

## f-strings (Python 3.6+)

```python
name = "Alice"
age = 25

# Basic
message = f"My name is {name} and I'm {age}"

# Expressions
print(f"Next year I'll be {age + 1}")

# Format specifiers
pi = 3.14159
print(f"Pi: {pi:.2f}")  # Pi: 3.14

# Padding
num = 5
print(f"{num:05}")  # 00005
```

## format() Method

```python
# Positional
print("My name is {} and I'm {}".format("Alice", 25))

# Index
print("My name is {0} and I'm {1}".format("Alice", 25))

# Named
print("My name is {name} and I'm {age}".format(name="Alice", age=25))

# Format specifiers
print("Pi: {:.2f}".format(3.14159))  # Pi: 3.14
```

## % Operator (Old Style)

```python
name = "Alice"
age = 25

print("My name is %s and I'm %d" % (name, age))

# Format specifiers
print("Pi: %.2f" % 3.14159)  # Pi: 3.14
```

## Format Specifiers

```python
# Numbers
print(f"{42:05}")     # 00042 (zero padding)
print(f"{42:5}")      # "   42" (space padding)
print(f"{3.14:.2f}")  # 3.14 (2 decimals)
print(f"{1234:,}")    # 1,234 (thousands separator)

# Alignment
print(f"{'left':<10}|")   # "left      |"
print(f"{'center':^10}|") # "  center  |"
print(f"{'right':>10}|")  # "     right|"

# Percentage
print(f"{0.85:.1%}")  # 85.0%

# Scientific notation
print(f"{1234:.2e}")  # 1.23e+03
```

## String Templates

```python
from string import Template

template = Template("My name is $name and I'm $age")
result = template.substitute(name="Alice", age=25)
print(result)
```

## Common Patterns

```python
# Currency
price = 19.99
print(f"${price:.2f}")  # $19.99

# Dates
from datetime import datetime
now = datetime.now()
print(f"{now:%Y-%m-%d %H:%M:%S}")

# Binary, hex, octal
num = 255
print(f"{num:b}")   # 11111111 (binary)
print(f"{num:x}")   # ff (hex)
print(f"{num:o}")   # 377 (octal)

# Padding with specific character
print(f"{42:*^10}")  # ****42****
```

---

**Related:** [[Python Strings]] | [[Python]] | [[Python Dates]]
