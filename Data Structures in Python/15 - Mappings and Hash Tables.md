# Mappings and Hash Tables

← [[14 - Selection]] | [[Data Structures in Python]] | Next: [[16 - Trees]] →

## The Mapping ADT

**Mapping** (also called **dictionary**, **map**, **associative array**):
- Stores **key-value** pairs
- Fast lookup by key
- Keys must be unique

### Operations

| Operation | Description | Returns |
|-----------|-------------|---------|
| `put(key, value)` | Add/update key-value pair | None |
| `get(key)` | Retrieve value for key | value |
| `remove(key)` | Delete key-value pair | None |
| `contains(key)` | Check if key exists | bool |
| `len()` | Number of pairs | int |

> [!important]
> Goal: All operations in $O(1)$ time!

Related: [[02 - Basic Python#Dictionaries (dict)]] for Python dict basics

## Naive Implementations

### List of Tuples

```python
class ListMapping:
    def __init__(self):
        self._items = []
    
    def put(self, key, value):
        for i, (k, v) in enumerate(self._items):
            if k == key:
                self._items[i] = (key, value)
                return
        self._items.append((key, value))
    
    def get(self, key):
        for k, v in self._items:
            if k == key:
                return v
        raise KeyError(key)
    
    def __contains__(self, key):
        return any(k == key for k, v in self._items)
```

**Problem:** All operations $O(n)$ - must scan list!

### Sorted List with Binary Search

```python
import bisect

class SortedListMapping:
    def __init__(self):
        self._items = []  # [(key, value), ...]
    
    def put(self, key, value):
        i = bisect.bisect_left([k for k, v in self._items], key)
        if i < len(self._items) and self._items[i][0] == key:
            self._items[i] = (key, value)
        else:
            self._items.insert(i, (key, value))
    
    def get(self, key):
        i = bisect.bisect_left([k for k, v in self._items], key)
        if i < len(self._items) and self._items[i][0] == key:
            return self._items[i][1]
        raise KeyError(key)
```

**Better:** `get` is $O(\log n)$
**Still slow:** `put` is $O(n)$ due to insertion

Related: [[11 - Binary Search]]

## Hash Tables

**Big idea:** Use a **hash function** to compute index from key!

### Hash Function

**Hash function** $h$: Maps keys to integers (indices)

**Requirements:**
1. **Deterministic:** Same key → same hash
2. **Uniform:** Distribute keys evenly
3. **Fast:** $O(1)$ to compute

**Example:**
```python
def simple_hash(key, table_size):
    """Simple hash for strings."""
    total = 0
    for char in key:
        total += ord(char)
    return total % table_size

print(simple_hash("cat", 10))  # 4
print(simple_hash("dog", 10))  # 4  # Collision!
```

### Python's hash() Function

```python
print(hash("hello"))     # -692164404
print(hash(42))          # 42
print(hash((1, 2, 3)))   # 529344067

# Unhashable (mutable):
# hash([1, 2, 3])        # TypeError!
```

> [!important]
> Only **immutable** types are hashable (can be hashed)

## Handling Collisions

**Collision:** Two different keys hash to same index

**Two main approaches:**
1. **Chaining** - store multiple items at same index
2. **Open addressing** - find another index

### Chaining

**Idea:** Each table slot contains a list (chain) of items

```python
class ChainedHashTable:
    def __init__(self, size=10):
        self._size = size
        self._table = [[] for _ in range(size)]
        self._length = 0
    
    def _hash(self, key):
        return hash(key) % self._size
    
    def put(self, key, value):
        index = self._hash(key)
        
        # Check if key already exists
        for i, (k, v) in enumerate(self._table[index]):
            if k == key:
                self._table[index][i] = (key, value)
                return
        
        # Add new key-value pair
        self._table[index].append((key, value))
        self._length += 1
    
    def get(self, key):
        index = self._hash(key)
        
        for k, v in self._table[index]:
            if k == key:
                return v
        raise KeyError(key)
    
    def __contains__(self, key):
        index = self._hash(key)
        return any(k == key for k, v in self._table[index])
    
    def __len__(self):
        return self._length

# Example
ht = ChainedHashTable()
ht.put("apple", 5)
ht.put("banana", 7)
ht.put("cherry", 3)
print(ht.get("banana"))  # 7
```

**Visualization:**
```
Table (size=5):
0: []
1: [("banana", 7)]
2: [("apple", 5), ("cherry", 3)]  ← chain (collision)
3: []
4: []
```

**Running time:**
- **Average:** $O(1)$ if table size ≈ number of items
- **Worst:** $O(n)$ if all keys hash to same index

### Load Factor

**Load factor** $\alpha = n / m$ where:
- $n$ = number of items
- $m$ = table size

> [!important]
> Keep $\alpha < 0.75$ for good performance!

### Resizing (Rehashing)

When table gets too full, **resize**:

```python
def _resize(self):
    """Double table size and rehash all items."""
    old_table = self._table
    self._size *= 2
    self._table = [[] for _ in range(self._size)]
    self._length = 0
    
    # Rehash all items
    for chain in old_table:
        for key, value in chain:
            self.put(key, value)
```

**Cost:** $O(n)$ to rehash all items

**Amortized cost:** $O(1)$ per operation!
- Most operations don't trigger resize
- Occasional expensive resize averaged over many cheap operations

Related: [[05 - Running Time Analysis#Asymptotic Analysis]]

### Complete Implementation with Resizing

```python
class HashTable:
    def __init__(self, size=10):
        self._size = size
        self._table = [[] for _ in range(size)]
        self._length = 0
    
    def _hash(self, key):
        return hash(key) % self._size
    
    def put(self, key, value):
        # Resize if load factor > 0.75
        if self._length / self._size > 0.75:
            self._resize()
        
        index = self._hash(key)
        
        for i, (k, v) in enumerate(self._table[index]):
            if k == key:
                self._table[index][i] = (key, value)
                return
        
        self._table[index].append((key, value))
        self._length += 1
    
    def get(self, key):
        index = self._hash(key)
        for k, v in self._table[index]:
            if k == key:
                return v
        raise KeyError(key)
    
    def remove(self, key):
        index = self._hash(key)
        for i, (k, v) in enumerate(self._table[index]):
            if k == key:
                del self._table[index][i]
                self._length -= 1
                return
        raise KeyError(key)
    
    def __contains__(self, key):
        index = self._hash(key)
        return any(k == key for k, v in self._table[index])
    
    def __len__(self):
        return self._length
    
    def _resize(self):
        old_table = self._table
        self._size *= 2
        self._table = [[] for _ in range(self._size)]
        self._length = 0
        
        for chain in old_table:
            for key, value in chain:
                self.put(key, value)
```

## Open Addressing

**Idea:** Store all items directly in table, probe for next empty slot

### Linear Probing

If slot $h(k)$ is full, try $h(k) + 1, h(k) + 2, \ldots$

```python
class LinearProbingHashTable:
    def __init__(self, size=10):
        self._size = size
        self._table = [None] * size
        self._length = 0
    
    def _hash(self, key):
        return hash(key) % self._size
    
    def put(self, key, value):
        if self._length / self._size > 0.5:
            self._resize()
        
        index = self._hash(key)
        
        # Probe for empty slot or matching key
        while self._table[index] is not None:
            k, v = self._table[index]
            if k == key:
                self._table[index] = (key, value)
                return
            index = (index + 1) % self._size
        
        self._table[index] = (key, value)
        self._length += 1
    
    def get(self, key):
        index = self._hash(key)
        
        while self._table[index] is not None:
            k, v = self._table[index]
            if k == key:
                return v
            index = (index + 1) % self._size
        
        raise KeyError(key)
```

**Problem:** **Clustering** - items bunch together, slowing down searches

### Quadratic Probing

Try $h(k), h(k) + 1^2, h(k) + 2^2, h(k) + 3^2, \ldots$

**Better:** Reduces clustering

### Double Hashing

Use second hash function to determine probe step:
Try $h_1(k), h_1(k) + h_2(k), h_1(k) + 2h_2(k), \ldots$

**Best:** Minimizes clustering

## Comparison: Chaining vs Open Addressing

| Aspect | Chaining | Open Addressing |
|--------|----------|-----------------|
| **Collisions** | List per slot | Probe for next slot |
| **Load factor** | Can exceed 1 | Must stay < 1 |
| **Memory** | Extra for lists | More table space |
| **Deletion** | Easy | Complex (need markers) |
| **Cache** | Poor | Better |
| **When** | Simple, flexible | Space-critical |

## Sets

**Set:** Mapping with keys but no values

```python
class HashSet:
    def __init__(self):
        self._map = HashTable()
    
    def add(self, item):
        self._map.put(item, None)
    
    def remove(self, item):
        self._map.remove(item)
    
    def __contains__(self, item):
        return item in self._map
    
    def __len__(self):
        return len(self._map)
```

> [!note]
> Python's `set` is implemented as a hash table!

Related: [[02 - Basic Python#Sets (set)]]

## Factoring Out A Superclass

**Pattern:** Create base class for shared functionality

```python
class Mapping:
    """Abstract base class for mappings."""
    
    def __getitem__(self, key):
        return self.get(key)
    
    def __setitem__(self, key, value):
        self.put(key, value)
    
    def __delitem__(self, key):
        self.remove(key)
    
    def __contains__(self, key):
        try:
            self.get(key)
            return True
        except KeyError:
            return False

class ListMapping(Mapping):
    # Implement get, put, remove
    pass

class HashTable(Mapping):
    # Implement get, put, remove
    pass
```

**Benefits:**
- Shared code in one place
- Consistent interface
- [[03 - Object-Oriented Programming#Duck Typing|Duck typing]] works

Related: [[03 - Object-Oriented Programming#Inheritance]]

## Applications

**Hash tables used for:**
- Python dictionaries and sets
- Database indexing
- Caches (memoization in [[10 - Dynamic Programming]])
- Symbol tables in compilers
- Routers (IP address lookup)
- Spell checkers

## Performance Summary

| Operation | Average | Worst | With good hash |
|-----------|---------|-------|----------------|
| `put` | $O(1)$ | $O(n)$ | $O(1)$ amortized |
| `get` | $O(1)$ | $O(n)$ | $O(1)$ |
| `remove` | $O(1)$ | $O(n)$ | $O(1)$ |
| `contains` | $O(1)$ | $O(n)$ | $O(1)$ |

> [!important]
> Hash tables provide $O(1)$ average-case for all operations!
> This is why Python dicts are so fast!

## Hash Table Design Principles

1. **Choose good hash function** - uniform distribution
2. **Keep load factor reasonable** - resize when needed
3. **Handle collisions well** - chaining or probing
4. **Use immutable keys** - prevent hash changes

## Related Topics

- [[02 - Basic Python#Dictionaries (dict)]] - Using Python dicts
- [[02 - Basic Python#Sets (set)]] - Using Python sets
- [[05 - Running Time Analysis#Dictionary Operations]] - Performance
- [[10 - Dynamic Programming#Memoization]] - Using dicts for caching
- [[03 - Object-Oriented Programming#Inheritance]] - Factoring superclass
- [[16 - Trees#Binary Search Trees]] - Alternative for ordered data

---

*Hash tables: the secret behind Python's blazing-fast dictionaries and sets.*
