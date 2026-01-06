# Sorting

← [[11 - Binary Search]] | [[Data Structures in Python]] | Next: [[13 - Sorting with Divide and Conquer]] →

## The Sorting Problem

**Given:** List of comparable items
**Goal:** Rearrange into non-decreasing order

**Why sort?**
- Enables [[11 - Binary Search|binary search]] - $O(\log n)$ lookup
- Makes data easier to understand
- Simplifies other algorithms
- Required by many algorithms

## Sorting in Python

### Built-in Sorting

```python
# Sort in place (modifies list)
L = [3, 1, 4, 1, 5, 9, 2, 6]
L.sort()
print(L)  # [1, 1, 2, 3, 4, 5, 6, 9]

# Return new sorted list (original unchanged)
L = [3, 1, 4, 1, 5, 9, 2, 6]
L2 = sorted(L)
print(L2)  # [1, 1, 2, 3, 4, 5, 6, 9]
print(L)   # [3, 1, 4, 1, 5, 9, 2, 6] - unchanged
```

### Custom Sorting

**By key:**
```python
words = ["banana", "pie", "Washington", "book"]
words.sort(key=len)
print(words)  # ['pie', 'book', 'banana', 'Washington']

# Sort by last letter
words.sort(key=lambda word: word[-1])
print(words)  # ['banana', 'pie', 'book', 'Washington']
```

**Reverse order:**
```python
L = [3, 1, 4, 1, 5]
L.sort(reverse=True)
print(L)  # [5, 4, 3, 1, 1]
```

**Multiple criteria:**
```python
# Sort by length, then alphabetically
words.sort(key=lambda word: (len(word), word))
```

> [!note]
> Python's built-in sort is **Timsort** - $O(n \log n)$ time, very efficient!

Related: [[13 - Sorting with Divide and Conquer#Merge Sort]] for similar algorithm

## Simple Sorting Algorithms

### Selection Sort

**Idea:** Repeatedly find minimum and move to front

```python
def selection_sort(L):
    n = len(L)
    for i in range(n):
        # Find index of minimum in L[i:]
        min_index = i
        for j in range(i + 1, n):
            if L[j] < L[min_index]:
                min_index = j
        
        # Swap minimum to position i
        L[i], L[min_index] = L[min_index], L[i]

L = [64, 25, 12, 22, 11]
selection_sort(L)
print(L)  # [11, 12, 22, 25, 64]
```

**Visualization:**
```
[64, 25, 12, 22, 11]  # Find min (11), swap with 64
[11, 25, 12, 22, 64]  # Find min in rest (12), swap with 25
[11, 12, 25, 22, 64]  # Find min (22), swap with 25
[11, 12, 22, 25, 64]  # Find min (25), already in place
[11, 12, 22, 25, 64]  # Done
```

**Analysis:**
- Comparisons: $n + (n-1) + (n-2) + \cdots + 1 = \frac{n(n+1)}{2}$
- **Running time:** $O(n^2)$
- **Space:** $O(1)$ - sorts in place

### Insertion Sort

**Idea:** Build sorted portion one element at a time

```python
def insertion_sort(L):
    n = len(L)
    for i in range(1, n):
        # Insert L[i] into sorted portion L[0:i]
        key = L[i]
        j = i - 1
        
        # Shift elements right to make room
        while j >= 0 and L[j] > key:
            L[j + 1] = L[j]
            j -= 1
        
        # Insert key
        L[j + 1] = key

L = [64, 25, 12, 22, 11]
insertion_sort(L)
print(L)  # [11, 12, 22, 25, 64]
```

**Visualization:**
```
[64, 25, 12, 22, 11]  # 25 < 64, insert before
[25, 64, 12, 22, 11]  # 12 < 25, insert at start
[12, 25, 64, 22, 11]  # 22 between 12 and 25
[12, 22, 25, 64, 11]  # 11 at start
[11, 12, 22, 25, 64]  # Done
```

**Analysis:**
- **Best case:** $O(n)$ - already sorted
- **Average/Worst case:** $O(n^2)$
- **Space:** $O(1)$ - sorts in place

> [!tip]
> Insertion sort is efficient for **small** or **nearly sorted** lists!

### Bubble Sort

**Idea:** Repeatedly swap adjacent elements if out of order

```python
def bubble_sort(L):
    n = len(L)
    for i in range(n):
        swapped = False
        for j in range(n - 1 - i):
            if L[j] > L[j + 1]:
                L[j], L[j + 1] = L[j + 1], L[j]
                swapped = True
        
        # If no swaps, list is sorted
        if not swapped:
            break

L = [64, 25, 12, 22, 11]
bubble_sort(L)
print(L)  # [11, 12, 22, 25, 64]
```

**Analysis:**
- **Best case:** $O(n)$ - with early termination
- **Average/Worst case:** $O(n^2)$
- **Space:** $O(1)$

> [!warning]
> Bubble sort is mainly of historical interest - rarely used in practice!

## Comparison of Simple Sorts

| Algorithm | Best | Average | Worst | Space | Stable |
|-----------|------|---------|-------|-------|--------|
| Selection Sort | $O(n^2)$ | $O(n^2)$ | $O(n^2)$ | $O(1)$ | No |
| Insertion Sort | $O(n)$ | $O(n^2)$ | $O(n^2)$ | $O(1)$ | Yes |
| Bubble Sort | $O(n)$ | $O(n^2)$ | $O(n^2)$ | $O(1)$ | Yes |

**Stability:** A stable sort preserves the relative order of equal elements

```python
# Example of stability
data = [(1, 'a'), (2, 'b'), (1, 'c')]
# Stable sort by first element:
# Result: [(1, 'a'), (1, 'c'), (2, 'b')]  # 'a' still before 'c'
```

## Why Study Simple Sorts?

1. **Educational** - understand sorting principles
2. **Small datasets** - competitive for n < 50
3. **Nearly sorted** - insertion sort is $O(n)$
4. **Building blocks** - used in advanced algorithms
5. **Space constrained** - $O(1)$ space

## Better Sorting Algorithms

For larger datasets, need faster algorithms:

### Overview

| Algorithm | Time | Space | Notes |
|-----------|------|-------|-------|
| [[13 - Sorting with Divide and Conquer#Merge Sort\|Merge Sort]] | $O(n \log n)$ | $O(n)$ | Stable, predictable |
| [[13 - Sorting with Divide and Conquer#Quicksort\|Quicksort]] | $O(n \log n)$ avg | $O(\log n)$ | Fast in practice |
| Heapsort | $O(n \log n)$ | $O(1)$ | Uses [[16 - Trees#Heaps\|heap]] |
| Timsort | $O(n \log n)$ | $O(n)$ | Python's default |

See [[13 - Sorting with Divide and Conquer]] for details.

## Counting Sort (Non-Comparison)

**When applicable:** Small range of integers

```python
def counting_sort(L, max_val):
    """Sort list of integers in range [0, max_val]."""
    n = len(L)
    
    # Count occurrences
    count = [0] * (max_val + 1)
    for num in L:
        count[num] += 1
    
    # Reconstruct sorted list
    index = 0
    for num in range(max_val + 1):
        for _ in range(count[num]):
            L[index] = num
            index += 1

L = [4, 2, 2, 8, 3, 3, 1]
counting_sort(L, 8)
print(L)  # [1, 2, 2, 3, 3, 4, 8]
```

**Running time:** $O(n + k)$ where $k$ = range of values

> [!important]
> Faster than $O(n \log n)$ **when** $k = O(n)$!

**Limitation:** Only works for integers in known range

## Radix Sort

**Idea:** Sort by individual digits/characters

```python
def radix_sort(L):
    """Sort list of non-negative integers."""
    if not L:
        return
    
    # Find maximum to determine number of digits
    max_val = max(L)
    exp = 1
    
    while max_val // exp > 0:
        # Counting sort on current digit
        counting_sort_by_digit(L, exp)
        exp *= 10

def counting_sort_by_digit(L, exp):
    n = len(L)
    output = [0] * n
    count = [0] * 10
    
    # Count occurrences of digits
    for num in L:
        digit = (num // exp) % 10
        count[digit] += 1
    
    # Cumulative count
    for i in range(1, 10):
        count[i] += count[i - 1]
    
    # Build output
    for i in range(n - 1, -1, -1):
        digit = (L[i] // exp) % 10
        output[count[digit] - 1] = L[i]
        count[digit] -= 1
    
    # Copy back
    for i in range(n):
        L[i] = output[i]

L = [170, 45, 75, 90, 802, 24, 2, 66]
radix_sort(L)
print(L)  # [2, 24, 45, 66, 75, 90, 170, 802]
```

**Running time:** $O(d \cdot n)$ where $d$ = number of digits

## Lower Bound for Comparison Sorts

> [!important]
> **Theorem:** Any comparison-based sorting algorithm requires $\Omega(n \log n)$ comparisons in the worst case.

**Why?**
- Decision tree has $n!$ leaves (all possible orderings)
- Tree height ≥ $\log_2(n!)$ ≈ $n \log n$

**Implication:** Merge sort and quicksort are **optimal** for comparison-based sorting!

Related: [[05 - Running Time Analysis#Big-O Notation]]

## Choosing a Sorting Algorithm

**Small data (n < 50):**
- Insertion sort - simple, fast for small n

**General purpose:**
- Python's `sort()`/`sorted()` (Timsort)
- [[13 - Sorting with Divide and Conquer#Merge Sort|Merge sort]] - predictable $O(n \log n)$

**Need $O(1)$ space:**
- Heapsort
- [[13 - Sorting with Divide and Conquer#Quicksort|Quicksort]] - often fastest in practice

**Integers in small range:**
- Counting sort or radix sort

**Mostly sorted:**
- Insertion sort - $O(n)$ if nearly sorted
- Timsort - optimized for partially sorted data

**Need stability:**
- [[13 - Sorting with Divide and Conquer#Merge Sort|Merge sort]]
- Timsort
- Insertion sort

## Related Topics

- [[11 - Binary Search]] - Requires sorted data
- [[13 - Sorting with Divide and Conquer]] - Advanced algorithms
- [[14 - Selection]] - Finding kth smallest without full sort
- [[05 - Running Time Analysis]] - Analyzing sort performance
- [[16 - Trees#Heaps]] - Heapsort data structure

---

*Sorting is fundamental - choose the right algorithm for your data and constraints.*
