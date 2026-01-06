# Sorting with Divide and Conquer

← [[12 - Sorting]] | [[Data Structures in Python]] | Next: [[14 - Selection]] →

## Divide and Conquer Strategy

**Three steps:**
1. **Divide:** Break problem into smaller subproblems
2. **Conquer:** Solve subproblems recursively
3. **Combine:** Merge solutions to create solution to original problem

> [!important]
> Divide and conquer often achieves $O(n \log n)$ time!

Related: [[09 - Recursion]] for recursive problem solving

## Merge Sort

**Idea:** 
- Divide list in half
- Recursively sort each half  
- Merge the sorted halves

### The Merge Operation

**Key operation:** Merge two sorted lists into one sorted list

```python
def merge(left, right):
    """Merge two sorted lists into one sorted list."""
    result = []
    i, j = 0, 0
    
    # Compare elements from left and right
    while i < len(left) and j < len(right):
        if left[i] <= right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1
    
    # Append remaining elements
    result.extend(left[i:])
    result.extend(right[j:])
    
    return result

# Example
left = [1, 3, 5, 7]
right = [2, 4, 6, 8]
print(merge(left, right))  # [1, 2, 3, 4, 5, 6, 7, 8]
```

**Running time:** $O(n)$ where $n = |left| + |right|$

### Merge Sort Implementation

```python
def mergesort(L):
    # Base case: list of 0 or 1 elements is sorted
    if len(L) <= 1:
        return L
    
    # Divide
    mid = len(L) // 2
    left = L[:mid]
    right = L[mid:]
    
    # Conquer (recursive sort)
    left = mergesort(left)
    right = mergesort(right)
    
    # Combine (merge)
    return merge(left, right)

L = [38, 27, 43, 3, 9, 82, 10]
sorted_L = mergesort(L)
print(sorted_L)  # [3, 9, 10, 27, 38, 43, 82]
```

### Visualization

Sorting `[38, 27, 43, 3, 9, 82, 10]`:

```
                [38, 27, 43, 3, 9, 82, 10]
                        /  \
            [38, 27, 43, 3]  [9, 82, 10]
               /    \           /    \
        [38, 27]  [43, 3]   [9, 82]  [10]
         /   \     /   \     /   \
       [38] [27] [43] [3]  [9] [82]
         \   /     \   /     \   /
        [27, 38]  [3, 43]   [9, 82]
            \      /           \     \
          [3, 27, 38, 43]    [9, 10, 82]
                    \          /
              [3, 9, 10, 27, 38, 43, 82]
```

### Analysis

**Recurrence relation:**
$$T(n) = 2T(n/2) + O(n)$$

- $2T(n/2)$: Two recursive calls on half-sized lists
- $O(n)$: Time to merge

**Solution:** $T(n) = O(n \log n)$

**Why?**
- Tree has $\log n$ levels (halving each time)
- Each level does $O(n)$ total work
- Total: $O(n) \times \log n = O(n \log n)$

**Space complexity:** $O(n)$ - need extra space for merging

### Properties

✓ **Stable:** Equal elements maintain relative order
✓ **Predictable:** Always $O(n \log n)$, even worst case
✓ **Good for linked lists:** No random access needed
✗ **Space:** Requires $O(n)$ extra space

Related: [[05 - Running Time Analysis#Asymptotic Analysis]]

## Quicksort

**Idea:**
- Choose a **pivot** element
- **Partition** list: elements < pivot, pivot, elements > pivot
- Recursively sort left and right partitions

### Partition Operation

```python
def partition(L, left, right):
    """
    Partition L[left:right+1] around pivot.
    Return index where pivot ends up.
    """
    # Choose rightmost element as pivot
    pivot = L[right]
    i = left - 1
    
    for j in range(left, right):
        if L[j] <= pivot:
            i += 1
            L[i], L[j] = L[j], L[i]
    
    # Place pivot in correct position
    L[i + 1], L[right] = L[right], L[i + 1]
    return i + 1

# Example
L = [10, 80, 30, 90, 40, 50, 70]
pivot_index = partition(L, 0, len(L) - 1)
print(L)           # [10, 30, 40, 50, 70, 90, 80]
print(pivot_index) # 4 (50 is now at index 4)
```

### Quicksort Implementation

```python
def quicksort(L, left=0, right=None):
    if right is None:
        right = len(L) - 1
    
    if left < right:
        # Partition and get pivot index
        pivot_index = partition(L, left, right)
        
        # Recursively sort left and right
        quicksort(L, left, pivot_index - 1)
        quicksort(L, pivot_index + 1, right)

L = [10, 80, 30, 90, 40, 50, 70]
quicksort(L)
print(L)  # [10, 30, 40, 50, 70, 80, 90]
```

### Visualization

Sorting `[10, 80, 30, 90, 40, 50, 70]` (pivot = rightmost):

```
[10, 80, 30, 90, 40, 50, 70]  pivot=70
    → partition →
[10, 30, 40, 50, 70, 90, 80]
 \_____________/     \______/
    left < 70        right > 70
    
Left: [10, 30, 40, 50]  pivot=50
    → partition →
[10, 30, 40, 50]
 \________/
  left < 50

Continue recursively...
```

### Analysis

**Best/Average case:** $O(n \log n)$
- Good pivot choices divide list evenly
- Tree height $\log n$, each level $O(n)$ work

**Worst case:** $O(n^2)$
- Poor pivot choices (e.g., always smallest/largest)
- Happens when list already sorted!
- Tree height $n$

**Example worst case:**
```
[1, 2, 3, 4, 5] with rightmost pivot
Choose 5: [1, 2, 3, 4] | [5]
Choose 4: [1, 2, 3] | [4]
Choose 3: [1, 2] | [3]
...
Total: 1 + 2 + 3 + 4 + 5 = O(n²)
```

### Improving Quicksort

**Random pivot:**
```python
import random

def partition_random(L, left, right):
    # Choose random pivot
    pivot_index = random.randint(left, right)
    L[pivot_index], L[right] = L[right], L[pivot_index]
    
    # Use regular partition
    return partition(L, left, right)
```

**Expected time:** $O(n \log n)$ even for sorted input!

**Median-of-three:**
```python
def median_of_three(L, left, right):
    mid = (left + right) // 2
    
    # Sort left, mid, right
    if L[left] > L[mid]:
        L[left], L[mid] = L[mid], L[left]
    if L[left] > L[right]:
        L[left], L[right] = L[right], L[left]
    if L[mid] > L[right]:
        L[mid], L[right] = L[right], L[mid]
    
    # Use middle value as pivot
    L[mid], L[right] = L[right], L[mid]
    return partition(L, left, right)
```

**Hybrid approach:**
```python
def quicksort_hybrid(L, left=0, right=None):
    if right is None:
        right = len(L) - 1
    
    # Use insertion sort for small sublists
    if right - left < 10:
        insertion_sort_range(L, left, right)
        return
    
    pivot_index = partition(L, left, right)
    quicksort_hybrid(L, left, pivot_index - 1)
    quicksort_hybrid(L, pivot_index + 1, right)
```

Related: [[12 - Sorting#Insertion Sort]] for small lists

### Properties

✓ **Fast in practice:** Often fastest sorting algorithm
✓ **In-place:** Only $O(\log n)$ extra space (recursion stack)
✓ **Cache-friendly:** Good memory locality
✗ **Not stable:** Relative order of equal elements may change
✗ **Worst case:** $O(n^2)$ without randomization

## Comparison: Merge Sort vs Quicksort

| Aspect | Merge Sort | Quicksort |
|--------|------------|-----------|
| **Average Time** | $O(n \log n)$ | $O(n \log n)$ |
| **Worst Time** | $O(n \log n)$ | $O(n^2)$ |
| **Space** | $O(n)$ | $O(\log n)$ |
| **Stable** | Yes | No |
| **In-place** | No | Yes |
| **Cache** | Less efficient | More efficient |
| **Practical speed** | Good | Often faster |

> [!tip]
> - Use **merge sort** when stability matters or worst-case guarantee needed
> - Use **quicksort** (with randomization) when space matters or want fastest average case

## Three-Way Quicksort

**For lists with many duplicates:**

```python
def quicksort_3way(L, left=0, right=None):
    if right is None:
        right = len(L) - 1
    
    if left >= right:
        return
    
    # Partition into: < pivot, = pivot, > pivot
    lt, gt = left, right
    pivot = L[left]
    i = left
    
    while i <= gt:
        if L[i] < pivot:
            L[lt], L[i] = L[i], L[lt]
            lt += 1
            i += 1
        elif L[i] > pivot:
            L[i], L[gt] = L[gt], L[i]
            gt -= 1
        else:
            i += 1
    
    # Recursively sort < and > portions
    quicksort_3way(L, left, lt - 1)
    quicksort_3way(L, gt + 1, right)

L = [4, 2, 4, 1, 4, 3, 4, 2, 4]
quicksort_3way(L)
print(L)  # [1, 2, 2, 3, 4, 4, 4, 4, 4]
```

**Benefit:** Linear time $O(n)$ when all elements equal!

## Master Theorem

General formula for divide-and-conquer recurrences:

$$T(n) = aT(n/b) + f(n)$$

**Merge sort:** $a=2, b=2, f(n)=O(n)$ → $T(n) = O(n \log n)$

**Binary search:** $a=1, b=2, f(n)=O(1)$ → $T(n) = O(\log n)$

Related: [[11 - Binary Search#Running Time Analysis]]

## When to Use Each

**Merge Sort:**
- Need stability
- Need guaranteed $O(n \log n)$
- Sorting linked lists
- External sorting (data doesn't fit in memory)

**Quicksort:**
- General purpose, fastest average case
- Space is limited
- Data fits in memory

**Python's Timsort:**
- Hybrid of merge sort and insertion sort
- Best of both worlds for practical data
- Default in Python's `sort()` and `sorted()`

## Related Topics

- [[12 - Sorting]] - Simple sorting algorithms
- [[09 - Recursion]] - Recursive problem solving
- [[14 - Selection]] - Finding kth element without full sort
- [[11 - Binary Search]] - Another divide-and-conquer algorithm
- [[05 - Running Time Analysis]] - Analyzing recursive algorithms

---

*Divide and conquer: break big problems into small ones, solve recursively.*
