# Python Frozenset

A frozenset is an immutable version of a set. Once created, elements cannot be added or removed.

## Creating Frozensets

```python
# From a list
frozen = frozenset([1, 2, 3, 4])

# From a set
normal_set = {1, 2, 3}
frozen = frozenset(normal_set)

# From a string
frozen = frozenset("hello")  # frozenset({'h', 'e', 'l', 'o'})

# Empty frozenset
empty = frozenset()

# Duplicates are removed
frozen = frozenset([1, 2, 2, 3, 3, 3])  # frozenset({1, 2, 3})
```

## Key Differences from Set

| Feature | Set | Frozenset |
|---------|-----|-----------|
| Mutable | ✅ Yes | ❌ No |
| Can add/remove | ✅ Yes | ❌ No |
| Hashable | ❌ No | ✅ Yes |
| Can be dict key | ❌ No | ✅ Yes |
| Can be set element | ❌ No | ✅ Yes |

## Why Use Frozensets?

### 1. As Dictionary Keys

```python
# Frozensets can be dictionary keys
locations = {
    frozenset(['New York', 'USA']): "East Coast",
    frozenset(['London', 'UK']): "Europe",
    frozenset(['Tokyo', 'Japan']): "Asia"
}

# Sets cannot be keys (unhashable)
# This would cause an error:
# bad_dict = { {'a', 'b'}: "value" }  # TypeError
```

### 2. As Set Elements

```python
# Frozensets can be elements of sets
set_of_sets = {
    frozenset([1, 2]),
    frozenset([3, 4]),
    frozenset([5, 6])
}

# Create set of frozensets from list of lists
data = [[1, 2], [3, 4], [5, 6]]
result = {frozenset(item) for item in data}
```

### 3. Immutable Data Structures

```python
# When you want to ensure data doesn't change
def process_data(numbers):
    # Convert to frozenset to prevent modification
    safe_numbers = frozenset(numbers)
    # safe_numbers.add(10)  # AttributeError
    return safe_numbers

# Useful for constants
VALID_COLORS = frozenset(['red', 'green', 'blue'])
```

## Set Operations

Frozensets support all the same operations as regular sets:

```python
frozen1 = frozenset([1, 2, 3])
frozen2 = frozenset([3, 4, 5])

# Union
union = frozen1 | frozen2  # frozenset({1, 2, 3, 4, 5})

# Intersection
intersection = frozen1 & frozen2  # frozenset({3})

# Difference
difference = frozen1 - frozen2  # frozenset({1, 2})

# Symmetric difference
sym_diff = frozen1 ^ frozen2  # frozenset({1, 2, 4, 5})

# Subset/superset
is_subset = frozen1 <= frozen2  # False
is_superset = frozen1 >= frozen2  # False
```

## Methods

Frozensets have the same query methods as sets, but no modification methods:

```python
frozen = frozenset([1, 2, 3, 4, 5])

# Available methods
len(frozen)                    # 5
3 in frozen                    # True
frozen.issubset({1, 2, 3, 4, 5, 6})     # True
frozen.issuperset({1, 2})      # True
frozen.isdisjoint({6, 7, 8})   # True
frozen.union({6, 7})           # frozenset({1, 2, 3, 4, 5, 6, 7})
frozen.intersection({3, 4, 5}) # frozenset({3, 4, 5})
frozen.difference({4, 5, 6})   # frozenset({1, 2, 3})
frozen.symmetric_difference({4, 5, 6})  # frozenset({1, 2, 3, 6})
frozen.copy()                  # Creates a copy

# NOT available (would modify)
# frozen.add(6)        # AttributeError
# frozen.remove(3)     # AttributeError
# frozen.discard(3)    # AttributeError
# frozen.pop()         # AttributeError
# frozen.clear()       # AttributeError
```

## Converting Between Set and Frozenset

```python
# Set to frozenset
normal_set = {1, 2, 3}
frozen = frozenset(normal_set)

# Frozenset to set
frozen = frozenset([1, 2, 3])
normal_set = set(frozen)

# Now you can modify it
normal_set.add(4)
```

## Practical Examples

### Graph Edges (Undirected)

```python
# Use frozensets for undirected graph edges
# Order doesn't matter: {A, B} == {B, A}

edges = {
    frozenset(['A', 'B']),
    frozenset(['B', 'C']),
    frozenset(['C', 'D']),
    frozenset(['A', 'D'])
}

# Add edge (no duplicates)
edges.add(frozenset(['B', 'A']))  # Same as ['A', 'B']
print(len(edges))  # Still 4

# Check if edge exists
has_edge = frozenset(['A', 'B']) in edges  # True
```

### Caching Results

```python
# Use frozenset as cache key
cache = {}

def expensive_operation(items):
    # Convert to frozenset for hashable key
    key = frozenset(items)
    
    if key not in cache:
        # Perform expensive computation
        result = sum(items) * len(items)
        cache[key] = result
    
    return cache[key]

# These will use the same cache entry
print(expensive_operation([1, 2, 3]))  # Computes
print(expensive_operation([3, 2, 1]))  # Uses cache
print(expensive_operation([2, 1, 3]))  # Uses cache
```

### Grouping by Set Membership

```python
# Group items by their characteristics
from collections import defaultdict

people = [
    {"name": "Alice", "skills": {"Python", "SQL"}},
    {"name": "Bob", "skills": {"Python", "Java"}},
    {"name": "Carol", "skills": {"SQL", "Java"}}
]

# Group by skill combination
groups = defaultdict(list)
for person in people:
    skill_set = frozenset(person["skills"])
    groups[skill_set].append(person["name"])

# Result: Each unique skill combination is a key
# {frozenset({'Python', 'SQL'}): ['Alice'], ...}
```

## Performance

- Frozensets have the same O(1) average time complexity for lookups as sets
- They use hash tables internally, just like sets
- Memory usage is similar to regular sets
- Since they're immutable, they can be optimized by Python

## When to Choose Frozenset vs Set

**Use frozenset when:**
- You need a hashable collection (dict key or set element)
- Data should not be modified after creation
- Working with mathematical sets that represent fixed collections
- Caching with collection-based keys

**Use set when:**
- You need to add/remove elements
- Data changes over time
- Don't need it as a dict key or set element

---

**Related:** [[Python Sets]] | [[Python Data Types]] | [[Python Dictionaries]] | [[Data Structures]]
