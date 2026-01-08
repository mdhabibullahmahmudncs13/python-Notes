# Python Data Types

Data types specify the type of data that a variable can store.

## Built-in Data Types

| Category | Data Types |
|----------|-----------|
| Text | `str` |
| Numeric | `int`, `float`, `complex` |
| Sequence | `list`, `tuple`, `range` |
| Mapping | `dict` |
| Set | `set`, `frozenset` |
| Boolean | `bool` |
| Binary | `bytes`, `bytearray`, `memoryview` |
| None | `NoneType` |

## Getting Data Type

Use `type()` function:

```python
x = 5
print(type(x))  # <class 'int'>

y = "Hello"
print(type(y))  # <class 'str'>
```

## Setting Data Types

```python
# Text
x = "Hello World"                    # str

# Numeric
x = 20                               # int
x = 20.5                             # float
x = 1j                               # complex

# Sequence
x = ["apple", "banana", "cherry"]    # list
x = ("apple", "banana", "cherry")    # tuple
x = range(6)                         # range

# Mapping
x = {"name": "John", "age": 36}      # dict

# Set
x = {"apple", "banana", "cherry"}    # set
x = frozenset({"apple", "banana"})   # frozenset  (see [[Python Frozenset]])

# Boolean
x = True                             # bool

# Binary
x = b"Hello"                         # bytes
x = bytearray(5)                     # bytearray
x = memoryview(bytes(5))             # memoryview

# None
x = None                             # NoneType
```

## Type Conversion

See [[Python Casting]] for converting between data types.

## Detailed Topics

- [[Python Strings]] - Text data
- [[Python Numbers]] - Numeric data
- [[Python Booleans]] - True/False values
- [[Python Lists]] - Ordered, mutable sequences
- [[Python Tuples]] - Ordered, immutable sequences
- [[Python Sets]] - Unordered, unique elements
- [[Python Dictionaries]] - Key-value pairs
- [[Python None]] - Null value

## Checking Data Types

```python
x = 200
print(isinstance(x, int))  # True

y = "Hello"
print(isinstance(y, str))  # True
```

---

**Related:** [[Python Variables]] | [[Python Casting]] | [[Python Numbers]] | [[Python Strings]]
