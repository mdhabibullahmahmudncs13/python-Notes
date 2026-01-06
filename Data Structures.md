# Data Structures

Python's built-in data structures for storing and organizing data.

## Topics

- [[Python Lists]] - Ordered, mutable collections
- [[Python Tuples]] - Ordered, immutable collections
- [[Python Sets]] - Unordered, unique elements
- [[Python Dictionaries]] - Key-value pairs
- [[Python Arrays]] - Homogeneous data storage
- [[Python Range]] - Sequence of numbers

## Comparison

| Structure | Ordered | Mutable | Duplicates | Syntax |
|-----------|---------|---------|------------|--------|
| List | Yes | Yes | Yes | `[]` |
| Tuple | Yes | No | Yes | `()` |
| Set | No | Yes | No | `{}` |
| Dictionary | Yes* | Yes | No (keys) | `{key:value}` |
| Array | Yes | Yes | Yes | `array()` |

*Dictionaries maintain insertion order (Python 3.7+)

## Choosing the Right Structure

- **List**: When you need an ordered, changeable collection
- **Tuple**: When you need an ordered, unchangeable collection
- **Set**: When you need unique elements and don't care about order
- **Dictionary**: When you need key-value pairs for fast lookups
- **Array**: When you need efficient numerical operations

---

**Related:** [[Python]] | [[Python Data Types]] | [[Python Iterators]]

**See Also:** [[Data Structures in Python|A First Course on Data Structures in Python]] - Complete textbook covering data structures, algorithms, and analysis
