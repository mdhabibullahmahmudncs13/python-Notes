# Python Strings

Strings are sequences of characters enclosed in quotes.

## Creating Strings

```python
# Single quotes
x = 'Hello'

# Double quotes
y = "Hello"

# Triple quotes for multi-line
z = '''This is a
multi-line
string'''

# Or with double quotes
z = """This is also a
multi-line
string"""
```

## String Indexing

```python
text = "Hello"
print(text[0])   # H
print(text[1])   # e
print(text[-1])  # o (last character)
print(text[-2])  # l (second from end)
```

## String Slicing

Extract a portion of a string:

```python
text = "Hello, World!"

# [start:end] (end not included)
print(text[0:5])   # Hello
print(text[7:12])  # World

# From start
print(text[:5])    # Hello

# To end
print(text[7:])    # World!

# Negative indexing
print(text[-6:-1]) # World

# Step
print(text[::2])   # Hlo ol!
print(text[::-1])  # !dlroW ,olleH (reverse)
```

## String Length

```python
text = "Hello"
print(len(text))  # 5
```

## Modifying Strings

### Upper/Lower Case
```python
text = "Hello World"

print(text.upper())      # HELLO WORLD
print(text.lower())      # hello world
print(text.capitalize()) # Hello world
print(text.title())      # Hello World
print(text.swapcase())   # hELLO wORLD
```

### Strip
```python
text = "  Hello  "
print(text.strip())   # "Hello"
print(text.lstrip())  # "Hello  "
print(text.rstrip())  # "  Hello"
```

### Replace
```python
text = "Hello World"
print(text.replace("World", "Python"))  # Hello Python
```

### Split
```python
text = "Hello, World, Python"
print(text.split(","))  # ['Hello', ' World', ' Python']
```

## String Concatenation

```python
a = "Hello"
b = "World"

# Using +
c = a + " " + b  # Hello World

# Using join()
words = ["Hello", "World"]
result = " ".join(words)  # Hello World
```

## String Formatting

### f-strings (Python 3.6+)
```python
name = "John"
age = 36
print(f"My name is {name} and I am {age}")
```

### format() method
```python
print("My name is {} and I am {}".format(name, age))
print("My name is {0} and I am {1}".format(name, age))
print("My name is {n} and I am {a}".format(n=name, a=age))
```

### % operator (old style)
```python
print("My name is %s and I am %d" % (name, age))
```

See [[Python String Formatting]] for more details.

## Escape Characters

```python
txt = "We are the so-called \"Vikings\" from the north."
txt = 'It\'s alright.'
txt = "This is a backslash: \\"
txt = "Hello\nWorld"    # New line
txt = "Hello\tWorld"    # Tab
txt = "Hello\rWorld"    # Carriage return
txt = "Hello\bWorld"    # Backspace
```

Common escape characters:
- `\'` - Single quote
- `\"` - Double quote
- `\\` - Backslash
- `\n` - New line
- `\t` - Tab
- `\r` - Carriage return
- `\b` - Backspace

## String Methods

```python
text = "Hello World"

# Case methods
text.upper()
text.lower()
text.capitalize()
text.title()
text.swapcase()

# Search methods
text.find("World")      # Returns index or -1
text.index("World")     # Returns index or raises error
text.count("l")         # Count occurrences
text.startswith("Hello")
text.endswith("World")

# Check methods
text.isalpha()          # All alphabetic
text.isdigit()          # All digits
text.isalnum()          # Alphanumeric
text.isspace()          # All whitespace
text.isupper()
text.islower()

# Modification methods
text.strip()
text.lstrip()
text.rstrip()
text.replace("old", "new")
text.split()
text.join(iterable)

# Format methods
text.center(20)
text.ljust(20)
text.rjust(20)
text.zfill(10)          # Pad with zeros
```

## String Checking

```python
text = "Hello World"

# Check substring
"World" in text         # True
"Python" not in text    # True
```

## Raw Strings

```python
# Ignore escape characters
path = r"C:\Users\name"
print(path)  # C:\Users\name
```

---

**Related:** [[Python Data Types]] | [[Python String Formatting]] | [[Python RegEx]] | [[Python Basics]]
