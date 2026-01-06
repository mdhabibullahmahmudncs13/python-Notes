# Selection

← [[13 - Sorting with Divide and Conquer]] | [[Data Structures in Python]] | Next: [[15 - Mappings and Hash Tables]] →

## The Selection Problem

**Given:** 
- List of $n$ comparable elements
- Integer $k$ where $1 \leq k \leq n$

**Find:** The $k$-th smallest element

**Examples:**
- $k=1$: minimum
- $k=n$: maximum
- $k=\lceil n/2 \rceil$: median

> [!important]
> Can we find the $k$-th smallest element **without fully sorting**?

## Naive Approach: Sort First

```python
def select_by_sorting(L, k):
    """Find kth smallest element (k is 1-indexed)."""
    sorted_L = sorted(L)
    return sorted_L[k - 1]

L = [3, 1, 4, 1, 5, 9, 2, 6]
print(select_by_sorting(L, 1))  # 1 (minimum)
print(select_by_sorting(L, 4))  # 3 (4th smallest)
print(select_by_sorting(L, 8))  # 9 (maximum)
```

**Running time:** $O(n \log n)$ - dominated by sorting

**Question:** Can we do better?

Related: [[12 - Sorting]], [[13 - Sorting with Divide and Conquer]]

## Finding Minimum/Maximum

**For minimum or maximum only:**

```python
def find_min(L):
    if not L:
        raise ValueError("Empty list")
    
    min_val = L[0]
    for item in L[1:]:
        if item < min_val:
            min_val = item
    return min_val

# Or use built-in:
print(min(L))
```

**Running time:** $O(n)$ - single pass

> [!tip]
> If you only need min or max, don't sort! Just scan the list.

## Quickselect Algorithm

**Idea:** Use [[13 - Sorting with Divide and Conquer#Quicksort|quicksort]] partitioning, but only recurse on one side!

### How It Works

1. Choose pivot and partition
2. If pivot is at position $k-1$, done!
3. If $k-1 <$ pivot position, recurse left
4. If $k-1 >$ pivot position, recurse right

### Implementation

```python
import random

def quickselect(L, k, left=0, right=None):
    """
    Find kth smallest element (k is 1-indexed).
    Modifies L in place.
    """
    if right is None:
        right = len(L) - 1
    
    if left == right:
        return L[left]
    
    # Random pivot for good expected performance
    pivot_index = random.randint(left, right)
    L[pivot_index], L[right] = L[right], L[pivot_index]
    
    # Partition
    pivot_index = partition(L, left, right)
    
    # Check if we found the kth element
    if k - 1 == pivot_index:
        return L[pivot_index]
    elif k - 1 < pivot_index:
        return quickselect(L, k, left, pivot_index - 1)
    else:
        return quickselect(L, k, pivot_index + 1, right)

def partition(L, left, right):
    """Partition L[left:right+1] around pivot at right."""
    pivot = L[right]
    i = left - 1
    
    for j in range(left, right):
        if L[j] <= pivot:
            i += 1
            L[i], L[j] = L[j], L[i]
    
    L[i + 1], L[right] = L[right], L[i + 1]
    return i + 1

# Example
L = [3, 1, 4, 1, 5, 9, 2, 6]
print(quickselect(L.copy(), 1))  # 1 (minimum)
print(quickselect(L.copy(), 4))  # 3 (4th smallest)
print(quickselect(L.copy(), 5))  # 4 (median)
```

### Visualization

Finding 4th smallest in `[3, 1, 4, 1, 5, 9, 2, 6]`:

```
[3, 1, 4, 1, 5, 9, 2, 6]  pivot=6
    → partition →
[3, 1, 4, 1, 5, 2, 6, 9]  pivot at index 6
                ^
k=4 < 6, so search left: [3, 1, 4, 1, 5, 2]

[3, 1, 4, 1, 5, 2]  pivot=2
    → partition →
[1, 1, 2, 4, 5, 3]  pivot at index 2
      ^
k=4 > 2, so search right: [4, 5, 3]

[4, 5, 3]  pivot=3
    → partition →
[3, 5, 4]  pivot at index 0 (relative)
^          → actual index 3 in original
           
k=4 > 3, search right: [5, 4]

[5, 4]  pivot=4
    → partition →
[4, 5]  pivot at index 0 (relative)
^       → actual index 3 in original

Found! 4th smallest = 3
```

### Analysis

**Best/Average case:** $O(n)$

**Why?**
- First partition: $O(n)$ work on $n$ elements
- Second partition: $O(n/2)$ work on $n/2$ elements (on average)
- Total: $n + n/2 + n/4 + \cdots = 2n = O(n)$

**Worst case:** $O(n^2)$
- If always pick bad pivot (like sorted list)
- Same as quicksort worst case

> [!important]
> **With randomization:** Expected $O(n)$ time!
> **Without sorting:** Much better than $O(n \log n)$!

Related: [[13 - Sorting with Divide and Conquer#Improving Quicksort]]

## Median of Medians (Deterministic)

**Worst-case $O(n)$ algorithm** (more complex):

### Idea

1. Divide elements into groups of 5
2. Find median of each group
3. Recursively find median of medians
4. Use as pivot

```python
def median_of_medians(L, k):
    """Find kth smallest in worst-case O(n) time."""
    if len(L) <= 5:
        return sorted(L)[k - 1]
    
    # Divide into groups of 5
    sublists = [L[i:i+5] for i in range(0, len(L), 5)]
    
    # Find median of each group
    medians = [sorted(sublist)[len(sublist)//2] for sublist in sublists]
    
    # Find median of medians
    pivot = median_of_medians(medians, len(medians)//2 + 1)
    
    # Partition around pivot
    low = [x for x in L if x < pivot]
    high = [x for x in L if x > pivot]
    pivot_count = len(L) - len(low) - len(high)
    
    # Recurse on appropriate partition
    if k <= len(low):
        return median_of_medians(low, k)
    elif k <= len(low) + pivot_count:
        return pivot
    else:
        return median_of_medians(high, k - len(low) - pivot_count)

L = [3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5]
print(median_of_medians(L, 6))  # 4
```

**Guaranteed:** $O(n)$ worst-case time

**In practice:** Quickselect is faster due to lower constants!

## Finding the Median

**Median:** Middle element when sorted
- Odd length: element at position $\lceil n/2 \rceil$
- Even length: average of positions $n/2$ and $n/2 + 1$

```python
def find_median(L):
    """Find median of list."""
    n = len(L)
    if n % 2 == 1:
        # Odd: single middle element
        return quickselect(L.copy(), n//2 + 1)
    else:
        # Even: average of two middle elements
        L_copy = L.copy()
        m1 = quickselect(L_copy, n//2)
        m2 = quickselect(L_copy, n//2 + 1)
        return (m1 + m2) / 2

L = [3, 1, 4, 1, 5]
print(find_median(L))  # 3

L = [3, 1, 4, 1, 5, 9]
print(find_median(L))  # 3.5
```

**Running time:** $O(n)$ expected

> [!note]
> For **two** median elements in even-length list, could find both in single pass

## Top-k Elements

**Problem:** Find $k$ largest (or smallest) elements

### Approach 1: Sort
```python
def top_k_sort(L, k):
    """Find k largest elements."""
    return sorted(L, reverse=True)[:k]
```
**Time:** $O(n \log n)$

### Approach 2: Heap
```python
import heapq

def top_k_heap(L, k):
    """Find k largest elements."""
    return heapq.nlargest(k, L)
```
**Time:** $O(n \log k)$ - better when $k$ is small!

Related: [[16 - Trees#Heaps]] for heap data structure

### Approach 3: Quickselect
```python
def top_k_quickselect(L, k):
    """Find k largest elements."""
    # Find (n-k+1)th smallest
    threshold = quickselect(L.copy(), len(L) - k + 1)
    return [x for x in L if x >= threshold]
```
**Time:** $O(n)$ expected

## Practical Applications

**Median:**
- Robust statistics (less sensitive to outliers than mean)
- Image processing (median filter)
- Database queries

**Top-k:**
- Search engines (top k results)
- Recommendation systems
- Leaderboards

**General selection:**
- Percentiles (90th percentile response time)
- Quartiles in statistics
- Quality control

## A Note on Derandomization

**Randomized quickselect:**
- Expected $O(n)$ time
- Simple to implement
- Works well in practice

**Median-of-medians:**
- Worst-case $O(n)$ time
- More complex
- Higher constants

> [!tip]
> Use randomized quickselect unless you need worst-case guarantees!

## Performance Comparison

| Method | Average | Worst | Notes |
|--------|---------|-------|-------|
| Sort then select | $O(n \log n)$ | $O(n \log n)$ | Simple |
| Min/max only | $O(n)$ | $O(n)$ | Best for k=1 or k=n |
| Quickselect | $O(n)$ | $O(n^2)$ | Fast in practice |
| Quickselect (random) | $O(n)$ | $O(n)$ expected | Recommended |
| Median-of-medians | $O(n)$ | $O(n)$ | Worst-case guarantee |
| Heap (top-k) | $O(n \log k)$ | $O(n \log k)$ | Good for small k |

## Related Topics

- [[13 - Sorting with Divide and Conquer#Quicksort]] - Partition algorithm
- [[12 - Sorting]] - When to sort vs select
- [[16 - Trees#Heaps]] - Alternative for top-k
- [[05 - Running Time Analysis]] - Expected vs worst-case time
- [[10 - Dynamic Programming]] - Another optimization technique

---

*Selection: finding the needle without sorting the entire haystack.*
