# Dynamic Programming

← [[09 - Recursion]] | [[Data Structures in Python]] | Next: [[11 - Binary Search]] →

## What is Dynamic Programming?

**Dynamic Programming (DP):** Optimization technique for solving problems by:
1. Breaking into **overlapping subproblems**
2. **Storing** solutions to avoid recomputation
3. **Building up** solution from smaller problems

> [!important]
> Dynamic Programming = [[09 - Recursion|Recursion]] + **Memoization** (or **Tabulation**)

**When to use:**
- Problem has overlapping subproblems
- Problem has optimal substructure
- Naive recursion too slow

## The Problem with Naive Recursion

### Fibonacci (Naive)

```python
def fib(n):
    if n <= 1:
        return n
    return fib(n - 1) + fib(n - 2)
```

**Problem:** Massive redundant computation!

```
fib(5)
├─ fib(4)
│  ├─ fib(3)
│  │  ├─ fib(2)
│  │  │  ├─ fib(1) → 1
│  │  │  └─ fib(0) → 0
│  │  └─ fib(1) → 1
│  └─ fib(2)           # Recomputed!
│     ├─ fib(1) → 1
│     └─ fib(0) → 0
└─ fib(3)              # Recomputed!
   ├─ fib(2)           # Recomputed!
   │  ├─ fib(1) → 1
   │  └─ fib(0) → 0
   └─ fib(1) → 1
```

**Running time:** $O(2^n)$ - exponential! 😱

Related: [[09 - Recursion#Fibonacci Numbers (Naive)]]

## Memoization

**Memoization:** Store results of function calls, reuse when same inputs occur

### Fibonacci with Memoization

```python
def fib_memo(n, memo=None):
    if memo is None:
        memo = {}
    
    if n in memo:            # Check if already computed
        return memo[n]
    
    if n <= 1:               # Base case
        return n
    
    # Compute and store result
    memo[n] = fib_memo(n - 1, memo) + fib_memo(n - 2, memo)
    return memo[n]

print(fib_memo(100))         # Fast! No problem.
```

**Running time:** $O(n)$ - each fib(i) computed once!

**Space:** $O(n)$ for memo dictionary + $O(n)$ recursion depth

### Using @lru_cache Decorator

Python provides built-in memoization:

```python
from functools import lru_cache

@lru_cache(maxsize=None)
def fib_cache(n):
    if n <= 1:
        return n
    return fib_cache(n - 1) + fib_cache(n - 2)

print(fib_cache(100))        # Equally fast!
```

> [!tip]
> `@lru_cache` is the pythonic way to memoize!

## Tabulation (Bottom-Up DP)

**Tabulation:** Build solution iteratively from smallest subproblems up

### Fibonacci with Tabulation

```python
def fib_tab(n):
    if n <= 1:
        return n
    
    # Create table for all values up to n
    table = [0] * (n + 1)
    table[1] = 1
    
    # Fill table bottom-up
    for i in range(2, n + 1):
        table[i] = table[i - 1] + table[i - 2]
    
    return table[n]

print(fib_tab(100))
```

**Running time:** $O(n)$
**Space:** $O(n)$ for table (no recursion overhead!)

### Space-Optimized Fibonacci

Only need last two values:

```python
def fib_optimized(n):
    if n <= 1:
        return n
    
    prev2, prev1 = 0, 1
    
    for i in range(2, n + 1):
        current = prev1 + prev2
        prev2, prev1 = prev1, current
    
    return prev1

print(fib_optimized(100))
```

**Running time:** $O(n)$
**Space:** $O(1)$ - optimal! 🎉

## Longest Increasing Subsequence (LIS)

**Problem:** Find length of longest increasing subsequence in array

**Example:** `[10, 9, 2, 5, 3, 7, 101, 18]`
- LIS: `[2, 3, 7, 101]` → length 4

### Recursive Solution with Memoization

```python
def lis(arr):
    n = len(arr)
    memo = {}
    
    def lis_ending_at(i):
        """Length of LIS ending at index i."""
        if i in memo:
            return memo[i]
        
        max_length = 1  # At minimum, the element itself
        
        for j in range(i):
            if arr[j] < arr[i]:
                max_length = max(max_length, 1 + lis_ending_at(j))
        
        memo[i] = max_length
        return max_length
    
    # Try all possible ending positions
    return max(lis_ending_at(i) for i in range(n))

arr = [10, 9, 2, 5, 3, 7, 101, 18]
print(lis(arr))  # 4
```

**Running time:** $O(n^2)$

### Tabulation Version

```python
def lis_tab(arr):
    n = len(arr)
    if n == 0:
        return 0
    
    # table[i] = length of LIS ending at index i
    table = [1] * n
    
    for i in range(1, n):
        for j in range(i):
            if arr[j] < arr[i]:
                table[i] = max(table[i], table[j] + 1)
    
    return max(table)

arr = [10, 9, 2, 5, 3, 7, 101, 18]
print(lis_tab(arr))  # 4
```

**Running time:** $O(n^2)$
**Space:** $O(n)$

## Edit Distance (Levenshtein Distance)

**Problem:** Minimum number of operations to transform string A into string B

**Operations:** Insert, delete, replace character

**Example:** 
- `"kitten"` → `"sitting"` requires 3 operations
- kitten → sitten (replace k with s)
- sitten → sittin (replace e with i)
- sittin → sitting (insert g)

### Recursive Solution

```python
def edit_distance(s1, s2, i=None, j=None, memo=None):
    if i is None:
        i = len(s1) - 1
    if j is None:
        j = len(s2) - 1
    if memo is None:
        memo = {}
    
    if (i, j) in memo:
        return memo[(i, j)]
    
    # Base cases
    if i == -1:
        return j + 1  # Insert all of s2
    if j == -1:
        return i + 1  # Delete all of s1
    
    # If characters match, no operation needed
    if s1[i] == s2[j]:
        result = edit_distance(s1, s2, i - 1, j - 1, memo)
    else:
        # Try all three operations, take minimum
        insert = 1 + edit_distance(s1, s2, i, j - 1, memo)
        delete = 1 + edit_distance(s1, s2, i - 1, j, memo)
        replace = 1 + edit_distance(s1, s2, i - 1, j - 1, memo)
        result = min(insert, delete, replace)
    
    memo[(i, j)] = result
    return result

print(edit_distance("kitten", "sitting"))  # 3
```

### Tabulation Version

```python
def edit_distance_tab(s1, s2):
    m, n = len(s1), len(s2)
    
    # Create table
    table = [[0] * (n + 1) for _ in range(m + 1)]
    
    # Base cases
    for i in range(m + 1):
        table[i][0] = i
    for j in range(n + 1):
        table[0][j] = j
    
    # Fill table
    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if s1[i - 1] == s2[j - 1]:
                table[i][j] = table[i - 1][j - 1]
            else:
                table[i][j] = 1 + min(
                    table[i][j - 1],      # Insert
                    table[i - 1][j],      # Delete
                    table[i - 1][j - 1]   # Replace
                )
    
    return table[m][n]

print(edit_distance_tab("kitten", "sitting"))  # 3
```

**Running time:** $O(mn)$ where $m = |s1|, n = |s2|$
**Space:** $O(mn)$

## Knapsack Problem

**Problem:** Given items with weights and values, and a knapsack capacity, maximize total value.

**0/1 Knapsack:** Each item can be taken at most once

### Example

```
Items: [(weight, value)]
[(2, 6), (2, 10), (3, 12)]
Capacity: 5

Answer: Take items 2 and 3 → value = 22
```

### Recursive Solution

```python
def knapsack(items, capacity, i=None, memo=None):
    if i is None:
        i = len(items) - 1
    if memo is None:
        memo = {}
    
    if (i, capacity) in memo:
        return memo[(i, capacity)]
    
    # Base case
    if i < 0 or capacity == 0:
        return 0
    
    weight, value = items[i]
    
    # Can't take this item
    if weight > capacity:
        result = knapsack(items, capacity, i - 1, memo)
    else:
        # Max of: take it or leave it
        take = value + knapsack(items, capacity - weight, i - 1, memo)
        leave = knapsack(items, capacity, i - 1, memo)
        result = max(take, leave)
    
    memo[(i, capacity)] = result
    return result

items = [(2, 6), (2, 10), (3, 12)]
print(knapsack(items, 5))  # 22
```

**Running time:** $O(n \cdot W)$ where $n$ = number of items, $W$ = capacity

## Comparison: Memoization vs Tabulation

| Aspect | Memoization (Top-Down) | Tabulation (Bottom-Up) |
|--------|----------------------|------------------------|
| Approach | Recursive | Iterative |
| Computation | Only needed subproblems | All subproblems |
| Code | Often more intuitive | Can be more efficient |
| Space | Recursion stack + memo | Just table |
| Ease | Easier to write | Requires planning order |

## DP Problem Characteristics

### Optimal Substructure

Optimal solution contains optimal solutions to subproblems

**Example:** Shortest path from A to C through B uses shortest path from A to B

### Overlapping Subproblems

Same subproblems solved multiple times in naive recursion

**Example:** `fib(5)` calls `fib(3)` twice

> [!important]
> Both properties must be present to use dynamic programming!

## DP Strategy

1. **Define subproblems:** What are the smaller problems?
2. **Find recurrence:** How do subproblems relate?
3. **Identify base cases:** When can we stop recursing?
4. **Determine order:** (For tabulation) What order to compute?
5. **Optimize space:** Can we use less memory?

## Related Topics

- [[09 - Recursion]] - Foundation for DP
- [[05 - Running Time Analysis]] - Analyzing DP algorithms
- [[11 - Binary Search]] - Another divide and conquer technique
- [[13 - Sorting with Divide and Conquer]] - Related optimization
- [[15 - Mappings and Hash Tables]] - Memoization uses dictionaries

---

*Dynamic programming transforms exponential problems into polynomial ones by remembering what we've already computed.*
