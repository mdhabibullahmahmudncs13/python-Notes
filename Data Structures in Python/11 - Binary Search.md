# Binary Search

← [[10 - Dynamic Programming]] | [[Data Structures in Python]] | Next: [[12 - Sorting]] →

## The Search Problem

**Given:** 
- A sorted list `L`
- A target value `target`

**Find:** Whether `target` is in `L`

> [!important]
> Binary search **requires** a sorted list!

## Linear Search (Naive)

```python
def linear_search(L, target):
    for item in L:
        if item == target:
            return True
    return False
```

**Running time:** $O(n)$ - must check each element in worst case

## Binary Search Algorithm

**Idea:** Repeatedly divide search space in half

**Strategy:**
1. Look at middle element
2. If it's the target, done!
3. If target is smaller, search left half
4. If target is larger, search right half
5. Repeat until found or search space empty

### Recursive Implementation

```python
def binary_search(L, target, left=0, right=None):
    if right is None:
        right = len(L) - 1
    
    # Base case: search space is empty
    if left > right:
        return False
    
    # Find middle
    mid = (left + right) // 2
    
    # Check middle element
    if L[mid] == target:
        return True
    elif L[mid] < target:
        # Search right half
        return binary_search(L, target, mid + 1, right)
    else:
        # Search left half
        return binary_search(L, target, left, mid - 1)

# Example
L = [1, 3, 5, 7, 9, 11, 13, 15, 17, 19]
print(binary_search(L, 7))    # True
print(binary_search(L, 8))    # False
```

Related: [[09 - Recursion#Binary Search (Recursive)]]

### Iterative Implementation

```python
def binary_search_iter(L, target):
    left, right = 0, len(L) - 1
    
    while left <= right:
        mid = (left + right) // 2
        
        if L[mid] == target:
            return True
        elif L[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    
    return False

# Example
L = [1, 3, 5, 7, 9, 11, 13, 15, 17, 19]
print(binary_search_iter(L, 7))    # True
print(binary_search_iter(L, 8))    # False
```

> [!tip]
> Iterative version avoids recursion overhead - slightly faster in practice

## Visualization

Searching for 7 in `[1, 3, 5, 7, 9, 11, 13, 15, 17, 19]`:

```
Step 1: [1, 3, 5, 7, 9, |11|, 13, 15, 17, 19]
        7 < 11, search left half

Step 2: [1, 3, |5|, 7, 9]
        7 > 5, search right half

Step 3: [7, |9|]
        7 < 9, search left half

Step 4: [|7|]
        Found!
```

## Running Time Analysis

**Question:** How many times can we divide $n$ by 2 before reaching 1?

**Answer:** $\log_2 n$ times

**Example:** $n = 1024 = 2^{10}$
- After 1 division: 512
- After 2 divisions: 256
- After 10 divisions: 1

> [!important]
> **Running time:** $O(\log n)$

This is **much faster** than linear search!

| List Size | Linear Search | Binary Search |
|-----------|---------------|---------------|
| 100 | 100 | 7 |
| 1,000 | 1,000 | 10 |
| 1,000,000 | 1,000,000 | 20 |
| 1,000,000,000 | 1,000,000,000 | 30 |

Related: [[05 - Running Time Analysis#Common Growth Rates]]

## Finding the Index

Modify to return index instead of boolean:

```python
def binary_search_index(L, target):
    left, right = 0, len(L) - 1
    
    while left <= right:
        mid = (left + right) // 2
        
        if L[mid] == target:
            return mid        # Return index
        elif L[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    
    return -1                # Not found

L = [1, 3, 5, 7, 9, 11, 13]
print(binary_search_index(L, 7))    # 3
print(binary_search_index(L, 8))    # -1
```

## Finding Insertion Point

Where should we insert `target` to keep list sorted?

```python
def binary_search_insert(L, target):
    left, right = 0, len(L)
    
    while left < right:
        mid = (left + right) // 2
        
        if L[mid] < target:
            left = mid + 1
        else:
            right = mid
    
    return left

L = [1, 3, 5, 7, 9, 11, 13]
print(binary_search_insert(L, 6))    # 3 (between 5 and 7)
print(binary_search_insert(L, 0))    # 0 (before 1)
print(binary_search_insert(L, 20))   # 7 (after 13)
```

> [!note]
> Python's `bisect` module provides this functionality!

```python
import bisect

L = [1, 3, 5, 7, 9, 11, 13]
print(bisect.bisect_left(L, 6))     # 3
print(bisect.bisect_right(L, 7))    # 4
```

## The Ordered List ADT

An **ordered list** maintains elements in sorted order.

### Operations

| Operation | Description | Time with Binary Search |
|-----------|-------------|-------------------------|
| `add(item)` | Insert item in sorted position | $O(n)$ |
| `remove(item)` | Remove item | $O(n)$ |
| `contains(item)` | Check if item present | $O(\log n)$ |
| `get(index)` | Get item at index | $O(1)$ |

> [!warning]
> Even with binary search, insertion is $O(n)$ because we must shift elements!

### Implementation

```python
import bisect

class OrderedList:
    def __init__(self):
        self._L = []
    
    def add(self, item):
        index = bisect.bisect_left(self._L, item)
        self._L.insert(index, item)    # O(n) - must shift
    
    def remove(self, item):
        index = bisect.bisect_left(self._L, item)
        if index < len(self._L) and self._L[index] == item:
            self._L.pop(index)         # O(n) - must shift
        else:
            raise ValueError(f"{item} not in list")
    
    def __contains__(self, item):
        index = bisect.bisect_left(self._L, item)
        return index < len(self._L) and self._L[index] == item
    
    def __getitem__(self, index):
        return self._L[index]
    
    def __len__(self):
        return len(self._L)
```

## Binary Search Variations

### First Occurrence

Find index of first occurrence of target:

```python
def binary_search_first(L, target):
    left, right = 0, len(L)
    
    while left < right:
        mid = (left + right) // 2
        
        if L[mid] < target:
            left = mid + 1
        else:
            right = mid
    
    if left < len(L) and L[mid] == target:
        return left
    return -1

L = [1, 3, 5, 5, 5, 7, 9]
print(binary_search_first(L, 5))    # 2
```

### Last Occurrence

Find index of last occurrence:

```python
def binary_search_last(L, target):
    left, right = 0, len(L)
    
    while left < right:
        mid = (left + right) // 2
        
        if L[mid] <= target:
            left = mid + 1
        else:
            right = mid
    
    if left > 0 and L[left - 1] == target:
        return left - 1
    return -1

L = [1, 3, 5, 5, 5, 7, 9]
print(binary_search_last(L, 5))     # 4
```

## Common Pitfalls

### Integer Overflow

```python
# Bad: Can overflow for large left + right
mid = (left + right) // 2

# Better:
mid = left + (right - left) // 2
```

> [!note]
> Not an issue in Python (arbitrary precision integers), but important in other languages!

### Off-by-One Errors

Be careful with:
- Loop condition: `left <= right` vs `left < right`
- Update: `mid + 1` vs `mid`, `mid - 1` vs `mid`
- Initial right: `len(L)` vs `len(L) - 1`

> [!tip]
> Test edge cases:
> - Empty list
> - Single element
> - Target at beginning/end
> - Target not present

## When to Use Binary Search

**Use when:**
- Data is sorted
- Need fast lookups ($O(\log n)$)
- Random access available (arrays, not linked lists)

**Don't use when:**
- Data not sorted (cost of sorting may outweigh benefit)
- Frequent insertions/deletions
- Small datasets (linear search simpler)

## Applications

- **Spell checkers** - dictionary lookup
- **Databases** - indexed searches
- **Version control** - finding when bug was introduced (git bisect)
- **Mathematical algorithms** - finding roots, optimization
- **Game AI** - decision making

## Related Topics

- [[12 - Sorting]] - Must sort before binary searching
- [[05 - Running Time Analysis#Logarithmic]] - Why $O(\log n)$ is fast
- [[09 - Recursion]] - Recursive implementation
- [[16 - Trees#Binary Search Trees]] - Data structure optimized for searching

---

*Binary search: dividing and conquering in $O(\log n)$ time.*
