# Python Casting

Type casting is converting a value from one data type to another.

## Constructor Functions

Python has three built-in functions for casting:

- `int()` - Constructs an integer
- `float()` - Constructs a float
- `str()` - Constructs a string

## Integer Casting

```python
# From float (removes decimals)
x = int(2.8)   # 2
y = int(3.9)   # 3

# From string (must be valid integer)
z = int("4")   # 4

# Invalid conversion
# x = int("4.5")  # ValueError
# y = int("Hello") # ValueError
```

## Float Casting

```python
# From integer
x = float(1)     # 1.0

# From string
y = float("3.14") # 3.14
z = float("3")    # 3.0
```

## String Casting

```python
# From integer
x = str(10)      # "10"

# From float
y = str(3.14)    # "3.14"

# From boolean
z = str(True)    # "True"
```

## Boolean Casting

```python
# Numbers: 0 is False, all others are True
bool(0)      # False
bool(1)      # True
bool(-5)     # True

# Strings: Empty string is False
bool("")     # False
bool("abc")  # True

# Collections: Empty collections are False
bool([])     # False
bool([1,2])  # True
bool({})     # False
bool(None)   # False
```

## List, Tuple, Set Casting

```python
# To list
x = list(("apple", "banana", "cherry"))  # From tuple
y = list({"a", "b", "c"})                # From set

# To tuple
x = tuple(["apple", "banana", "cherry"]) # From list
y = tuple({"a", "b", "c"})               # From set

# To set
x = set(["apple", "banana", "cherry"])   # From list
y = set(("apple", "banana", "cherry"))   # From tuple
```

## Dictionary Casting

```python
# From sequence of tuples
x = dict([("name", "John"), ("age", 36)])
# {'name': 'John', 'age': 36}

# Using dict() constructor
y = dict(name="John", age=36)
# {'name': 'John', 'age': 36}
```

## Complex Conversions

```python
# String to list
text = "Hello"
chars = list(text)  # ['H', 'e', 'l', 'l', 'o']

# Number to binary/hex/octal string
num = 255
bin_str = bin(num)   # '0b11111111'
hex_str = hex(num)   # '0xff'
oct_str = oct(num)   # '0o377'

# String to number (different bases)
int("10")       # 10 (decimal)
int("10", 2)    # 2  (binary)
int("10", 8)    # 8  (octal)
int("10", 16)   # 16 (hexadecimal)
```

## Error Handling

```python
try:
    x = int("hello")
except ValueError:
    print("Cannot convert to integer")
```

See [[Python Try Except]] for error handling.

---

**Related:** [[Python Data Types]] | [[Python Numbers]] | [[Python Variables]] | [[Python Try Except]]
