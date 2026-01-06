# Running Time Analysis

← [[04 - Testing]] | [[Data Structures in Python]] | Next: [[06 - Stacks and Queues]] →

## Goals

Write code that is:
1. **Correct** → Debug it
2. **Efficient** → Analyze it
3. **Readable** → Review it

> [!important]
> Inefficiency problems may not appear with small test inputs!

## Objectives of Analysis

Describe efficiency in a way that:
- **Adapts to different inputs** - same code, different performance
- **Adapts to different computers** - hardware-independent description

**Solution:** **Asymptotic Analysis**

## Approach

1. **Measure** running time experimentally
2. **Count** operations (accounting scheme)
3. **Classify** functions using Big-O notation

## Timing Programs

### Example: Finding Duplicates

```python
def duplicates1(L):
    n = len(L)
    for i in range(n):
        for j in range(n):
            if i != j and L[i] == L[j]:
                return True
    return False
```

### Basic Timing

```python
import time

start = time.time()
duplicates1(list(range(1000)))
timetaken = time.time() - start
print("Time taken:", timetaken)
```

**Problem:** Variation between runs due to:
- Other processes running
- Operating system overhead
- Computer hardware differences

### Averaging Multiple Trials

```python
import time

def timetrials(func, n, trials=10):
    totaltime = 0
    for i in range(trials):
        start = time.time()
        func(list(range(n)))
        totaltime += time.time() - start
    print("average =%10.7f for n = %d" % (totaltime/trials, n))
```

### Observing Growth

```python
for n in [50, 100, 200, 400, 800, 1600, 3200]:
    timetrials(duplicates1, n)
```

> [!note]
> Time increases as input size increases - but by how much?

## Improving Efficiency

### Version 2: Eliminate Redundant Comparisons

```python
def duplicates2(L):
    n = len(L)
    for i in range(1, n):
        for j in range(i):
            if L[i] == L[j]:
                return True
    return False
```

**Improvement:** Only compare each pair once

### Version 3: Pythonic Version

```python
def duplicates3(L):
    n = len(L)
    return any(L[i] == L[j] 
               for i in range(1, n) 
               for j in range(i))
```

Uses `any()` with generator expression - more readable, similar performance.

### Version 4: Sorting Approach

```python
def duplicates4(L):
    n = len(L)
    L.sort()
    for i in range(n-1):
        if L[i] == L[i+1]:
            return True
    return False
```

**New idea:** Sort first, then check adjacent elements

### Version 5: Using Sets

```python
def duplicates5(L):
    return len(L) != len(set(L))
```

**Key insight:** Sets automatically remove duplicates!

### Performance Comparison

| Input Size | Quadratic | Sorting | Sets |
|------------|-----------|---------|------|
| n = 50 | ~0.0001s | ~0.00001s | ~0.000005s |
| n = 3200 | ~0.4s | ~0.0004s | ~0.00009s |

> [!important]
> **Data structures really matter!**
> The gap increases as input grows.

Related: [[15 - Mappings and Hash Tables]] for how sets work

## Adding First k Numbers

### Iterative Approach

```python
import time

def sumk(k):
    start = time.time()
    total = 0
    for i in range(k+1):
        total = total + i
    end = time.time()
    return total, end-start
```

**Observation:** Time proportional to k

### Mathematical Formula

$$\sum_{i=1}^{k} i = 1 + 2 + 3 + \cdots + k = \frac{k(k+1)}{2}$$

**Proof:** Pair numbers (1+k), (2+k-1), etc. 
- k/2 pairs
- Each sum is k+1

### Constant Time Approach

```python
import time

def sumk2(k):
    start = time.time()
    total = (k*(k+1))//2
    end = time.time()
    return total, end-start
```

> [!important]
> Much faster! Doesn't slow down as k increases.

## Counting Operations

### Atomic Operations

Basic operations that take constant time:
- Arithmetic: `+`, `-`, `*`, `/`
- Boolean operations: `and`, `or`, `not`
- Variable assignment
- Variable access
- Branching: `if`, `for`, `while`
- Function call
- Function return

> [!note]
> Each atomic operation takes small, constant number of CPU clock cycles

### NOT Counting Lines of Code

```python
def f001(k):
    return [sum([i, i + 1] * 100) for i in range(k)]
```

One line ≠ one operation! This does lots of work.

Related: [[02 - Basic Python#Expressions and Evaluation]] for operation precedence

## Python Collection Operations

### List Operations

| Operation | Code | Running Time |
|-----------|------|--------------|
| Index | `L[i]` | $O(1)$ |
| Store | `L[i] = x` | $O(1)$ |
| Length | `len(L)` | $O(1)$ |
| Append | `L.append(x)` | $O(1)$ |
| Pop from end | `L.pop()` | $O(1)$ |
| Clear | `L.clear()` | $O(1)$ |
| Slice | `L[a:b]` | $O(b-a)$ |
| Extend | `L.extend(L2)` | $O(|L2|)$ |
| Concatenate | `L1 + L2` | $O(|L1|+|L2|)$ |
| Sort | `L.sort()` | $O(n \log n)$ |
| Multiply | `k*L` | $O(kn)$ |
| Delete | `del L[i]` | $O(n)$ |
| Contains | `x in L` | $O(n)$ |
| Copy | `L.copy()` | $O(n)$ |
| Remove | `L.remove(x)` | $O(n)$ |
| Pop from front | `L.pop(0)` | $O(n)$ |

> [!warning]
> **Slicing and concatenation create new collections!**
> Cost proportional to new collection size.

### Dictionary Operations

| Operation | Code | Running Time |
|-----------|------|--------------|
| Get item | `D[key]` | $O(1)$ |
| Set item | `D[key] = value` | $O(1)$ |
| Delete | `del D[key]` | $O(1)$ |
| Contains | `key in D` | $O(1)$ |
| Length | `len(D)` | $O(1)$ |

> [!note]
> Dictionary operations seem impossibly fast!
> - Clever algorithm (see [[15 - Mappings and Hash Tables]])
> - This is a model (accurate on average)
> - Actual cost varies (amortized analysis)

### Set Operations

Sets implemented like dictionaries (keys without values).

| Operation | Code | Running Time |
|-----------|------|--------------|
| Add | `S.add(x)` | $O(1)$ |
| Remove | `S.remove(x)` | $O(1)$ |
| Contains | `x in S` | $O(1)$ |
| Length | `len(S)` | $O(1)$ |
| Union | `S | T` | $O(|S|+|T|)$ |
| Intersection | `S & T` | $O(\min(|S|,|T|))$ |
| Difference | `S - T` | $O(|S|)$ |

> [!note]
> Operations producing new sets leave input unchanged.

Related: [[15 - Mappings and Hash Tables#Hash Tables]] for implementation

## Asymptotic Analysis

### Order of Growth

**Goal:** Predict how time grows as input size grows

**Example:** If time proportional to n:
- 100× larger input → 100× more time

**Example:** If time proportional to n²:
- 100× larger input → 10,000× more time

> [!important]
> Exact constant doesn't matter - it's the **growth rate** that matters!

### Input Size

**Input size:** Number of bits (or words) to encode input
- Integer: 1 word (constant)
- Float: 1 word (constant)
- List of n items: n words

> [!note]
> Convention: Assume ints and floats fit in constant bits
> (Necessary to assume arithmetic is constant time)

### Worst Case Analysis

Different inputs of same size may have different running times.

> [!tip]
> Standard convention: Consider **worst case**
> - Provides upper bound
> - If actual time is better, that's okay!

## Big-O Notation

### Intuition

Function $f(n) = 5n^2 + 3n + 2$

The $5n^2$ term dominates - other terms become negligible as n grows.

### Formal Definition

$f(n) = O(g(n))$ if there exist constants $c$ and $n_0$ such that for all $n > n_0$:

$$f(n) \leq c \cdot g(n)$$

**Example:** $f(n) = 5n^2 + 3n + 2 = O(n^2)$

**Proof:** Take $c = 6$. For $n > 4$:
$$f(n) = 5n^2 + 3n + 2 < 5n^2 + 4n < 5n^2 + n^2 \leq 6n^2$$

### Common Growth Rates

From fastest to slowest:

| Notation | Name | Example |
|----------|------|---------|
| $O(1)$ | Constant | Array access, hash table lookup |
| $O(\log n)$ | Logarithmic | [[11 - Binary Search\|Binary search]] |
| $O(n)$ | Linear | Linear search, sum array |
| $O(n \log n)$ | Linearithmic | [[12 - Sorting\|Merge sort]], [[13 - Sorting with Divide and Conquer\|quicksort]] |
| $O(n^2)$ | Quadratic | Nested loops, bubble sort |
| $O(n^3)$ | Cubic | Triple nested loops |
| $O(2^n)$ | Exponential | Recursive fibonacci |
| $O(n!)$ | Factorial | Generate all permutations |

### Properties of Big-O

**Constants don't matter:**
- $O(5n) = O(n)$
- $O(100) = O(1)$

**Lower order terms don't matter:**
- $O(n^2 + n) = O(n^2)$
- $O(n^2 + \log n) = O(n^2)$

**Composition:**
- If $f(n) = O(g(n))$ and $g(n) = O(h(n))$, then $f(n) = O(h(n))$

## Analyzing Code

### Simple Loop
```python
total = 0
for i in range(n):
    total += i
```
**Analysis:** $O(n)$ - loop runs n times, each iteration $O(1)$

### Nested Loop
```python
for i in range(n):
    for j in range(n):
        print(i, j)
```
**Analysis:** $O(n^2)$ - outer loop n times, inner loop n times

### Dependent Nested Loop
```python
for i in range(n):
    for j in range(i):
        print(i, j)
```
**Analysis:** $O(n^2)$ - total iterations: $1+2+\cdots+n = \frac{n(n+1)}{2}$

### Sequential Operations
```python
for i in range(n):
    print(i)
for j in range(n):
    print(j)
```
**Analysis:** $O(n) + O(n) = O(n)$

## Practice Examples

**Example 1:** What is the running time?
```python
def mystery1(L):
    for item in L:
        print(item)
```
Answer: $O(n)$ where $n = $ `len(L)`

**Example 2:** What is the running time?
```python
def mystery2(L):
    for i in range(len(L)):
        for j in range(i, len(L)):
            print(L[i], L[j])
```
Answer: $O(n^2)$

**Example 3:** What is the running time?
```python
def mystery3(L):
    L.sort()
    return L[0]
```
Answer: $O(n \log n)$ dominated by sorting

Related: [[12 - Sorting]], [[13 - Sorting with Divide and Conquer]]

## Key Takeaways

> [!important]
> 1. **Data structures matter** - choose wisely for efficiency
> 2. **Focus on growth rate** - constants matter less than Big-O class
> 3. **Worst case analysis** - provides upper bounds
> 4. **Algorithm design** - better algorithm beats faster computer

## Related Topics

- [[06 - Stacks and Queues]] - Efficient data structures
- [[11 - Binary Search]] - $O(\log n)$ searching
- [[12 - Sorting]] - $O(n \log n)$ algorithms
- [[15 - Mappings and Hash Tables]] - $O(1)$ operations
- [[10 - Dynamic Programming]] - Optimization technique

---

*Thinking about efficiency helps develop good habits and intuitions for good design.*
