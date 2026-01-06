# Recursion

← [[08 - Doubly-Linked Lists]] | [[Data Structures in Python]] | Next: [[10 - Dynamic Programming]] →

## What is Recursion?

**Recursion**: A function that calls itself

**Key components:**
1. **Base case** - stops the recursion
2. **Recursive case** - breaks problem into smaller sub-problems

> [!important]
> Every recursive function **must** have a base case or it will recurse forever!

## Simple Examples

### Countdown

```python
def countdown(n):
    if n == 0:           # Base case
        print("Blastoff!")
    else:                # Recursive case
        print(n)
        countdown(n - 1)  # Recursive call

countdown(5)
# Output: 5 4 3 2 1 Blastoff!
```

### Factorial

$$n! = n \times (n-1) \times (n-2) \times \cdots \times 2 \times 1$$

Recursive definition: $n! = n \times (n-1)!$ with $0! = 1$

```python
def factorial(n):
    if n == 0:           # Base case
        return 1
    else:                # Recursive case
        return n * factorial(n - 1)

print(factorial(5))      # 120
```

## The Call Stack

**How recursion works internally:**

Each function call gets a **stack frame** containing:
- Local variables
- Parameters
- Return address

Related: [[06 - Stacks and Queues#The Stack ADT]] - function calls use a stack!

**Example: `factorial(3)`**

```
factorial(3)
  └─ return 3 * factorial(2)
                  └─ return 2 * factorial(1)
                                  └─ return 1 * factorial(0)
                                                  └─ return 1
```

Stack frames:
```
┌─────────────────┐
│ factorial(0)    │
│ n = 0           │
│ returns 1       │
├─────────────────┤
│ factorial(1)    │
│ n = 1           │
│ returns 1 * 1   │
├─────────────────┤
│ factorial(2)    │
│ n = 2           │
│ returns 2 * 1   │
├─────────────────┤
│ factorial(3)    │
│ n = 3           │
│ returns 3 * 2   │
└─────────────────┘
```

## Recursion vs Iteration

### Iterative Factorial

```python
def factorial_iter(n):
    result = 1
    for i in range(1, n + 1):
        result *= i
    return result
```

### Comparison

| Aspect | Recursion | Iteration |
|--------|-----------|-----------|
| Readability | Often clearer | Can be verbose |
| Memory | Uses call stack | Uses loop variables |
| Performance | Function call overhead | Usually faster |
| Depth | Limited by stack size | No limit (except time) |

> [!tip]
> Use recursion when it makes the problem clearer, not just because you can!

## Recursive List Operations

### Sum of List

```python
def sum_list(L):
    if len(L) == 0:              # Base case
        return 0
    else:                         # Recursive case
        return L[0] + sum_list(L[1:])

print(sum_list([1, 2, 3, 4]))    # 10
```

> [!warning]
> **Problem:** `L[1:]` creates a new list - $O(n)$ per call!
> Total time: $O(n^2)$

See [[05 - Running Time Analysis#Slicing]] for why slicing is expensive.

### Better Approach with Helper Function

```python
def sum_list(L):
    def helper(L, i):
        if i == len(L):          # Base case
            return 0
        else:                     # Recursive case
            return L[i] + helper(L, i + 1)
    
    return helper(L, 0)
```

**Now:** $O(n)$ time - no copying!

## Recursive Data Structures

### Linked List Length (Recursive)

```python
def length_recursive(node):
    if node is None:             # Base case
        return 0
    else:                         # Recursive case
        return 1 + length_recursive(node.link)
```

### Linked List Search

```python
def search(node, target):
    if node is None:             # Base case: not found
        return False
    elif node.data == target:    # Base case: found
        return True
    else:                         # Recursive case
        return search(node.link, target)
```

Related: [[07 - Deques and Linked Lists#Linked Lists]]

## Towers of Hanoi

Classic recursion problem:
- 3 pegs, n disks of different sizes
- Move all disks from peg A to peg C
- Rules: Move one disk at a time, never place larger disk on smaller

**Recursive solution:**

```python
def hanoi(n, source, target, auxiliary):
    if n == 1:
        print(f"Move disk from {source} to {target}")
    else:
        # Move n-1 disks to auxiliary peg
        hanoi(n - 1, source, auxiliary, target)
        
        # Move largest disk to target
        print(f"Move disk from {source} to {target}")
        
        # Move n-1 disks from auxiliary to target
        hanoi(n - 1, auxiliary, target, source)

hanoi(3, 'A', 'C', 'B')
```

**Analysis:** $2^n - 1$ moves required

## Euclid's Algorithm

**Find GCD (Greatest Common Divisor):**

**Mathematical insight:** 
$$\gcd(a, b) = \gcd(b, a \mod b)$$

```python
def gcd(a, b):
    if b == 0:               # Base case
        return a
    else:                     # Recursive case
        return gcd(b, a % b)

print(gcd(48, 18))           # 6
```

**Why it works:**
- Any divisor of both $a$ and $b$ also divides $a \mod b$
- Process terminates when $b = 0$

**Running time:** $O(\log \min(a, b))$ - very efficient!

## Binary Search (Recursive)

```python
def binary_search(L, target, left=0, right=None):
    if right is None:
        right = len(L) - 1
    
    if left > right:             # Base case: not found
        return False
    
    mid = (left + right) // 2
    
    if L[mid] == target:         # Base case: found
        return True
    elif L[mid] < target:        # Search right half
        return binary_search(L, target, mid + 1, right)
    else:                         # Search left half
        return binary_search(L, target, left, mid - 1)

L = [1, 3, 5, 7, 9, 11, 13]
print(binary_search(L, 7))       # True
print(binary_search(L, 6))       # False
```

Related: [[11 - Binary Search]] for detailed analysis

## Fibonacci Numbers (Naive)

$$F(n) = F(n-1) + F(n-2)$$ with $F(0) = 0, F(1) = 1$

```python
def fib(n):
    if n <= 1:               # Base cases
        return n
    else:                     # Recursive case
        return fib(n - 1) + fib(n - 2)

print(fib(10))               # 55
```

> [!warning]
> **Extremely inefficient!** Time: $O(2^n)$
> - Recalculates same values many times
> - `fib(5)` calculated multiple times when computing `fib(10)`

**Solution:** [[10 - Dynamic Programming#Memoization]]

## Recursion Patterns

### Direct Recursion
Function calls itself directly:
```python
def f(n):
    return f(n - 1)
```

### Indirect Recursion
Functions call each other:
```python
def is_even(n):
    if n == 0:
        return True
    return is_odd(n - 1)

def is_odd(n):
    if n == 0:
        return False
    return is_even(n - 1)
```

### Multiple Recursive Calls
Function makes multiple recursive calls:
```python
def fibonacci(n):
    return fibonacci(n - 1) + fibonacci(n - 2)
```

## Tail Recursion

**Tail recursive:** Recursive call is the last operation

```python
def factorial_tail(n, accumulator=1):
    if n == 0:
        return accumulator
    else:
        return factorial_tail(n - 1, n * accumulator)
```

> [!note]
> Some languages optimize tail recursion to use $O(1)$ space.
> Python does **not** optimize tail recursion!

## Recursion Guidelines

### When to Use Recursion

✓ Problem naturally recursive (e.g., trees, [[16 - Trees]])
✓ Divide and conquer algorithms ([[13 - Sorting with Divide and Conquer]])
✓ Backtracking problems
✓ Makes code significantly clearer

### When to Avoid Recursion

✗ Simple iteration works better
✗ Deep recursion (stack overflow)
✗ Redundant calculations (use [[10 - Dynamic Programming]])
✗ Performance critical code

### Recursion Checklist

- [ ] Base case(s) defined
- [ ] Recursive case makes progress toward base case
- [ ] No infinite recursion possible
- [ ] Function call overhead acceptable
- [ ] Stack depth won't exceed limit

## Common Pitfalls

**Missing base case:**
```python
def infinite(n):
    return infinite(n - 1)  # Never stops!
```

**Not making progress:**
```python
def bad(n):
    if n == 0:
        return 0
    return bad(n)  # Doesn't decrease n!
```

**Unnecessary recursion:**
```python
# Bad: Recursion for simple loop
def print_n(n):
    if n > 0:
        print(n)
        print_n(n - 1)

# Good: Use a loop
for i in range(n, 0, -1):
    print(i)
```

## Related Topics

- [[10 - Dynamic Programming]] - Optimizing recursive solutions
- [[11 - Binary Search]] - Recursive divide and conquer
- [[13 - Sorting with Divide and Conquer]] - Merge sort, quicksort
- [[16 - Trees]] - Naturally recursive structure
- [[05 - Running Time Analysis]] - Analyzing recursive algorithms
- [[06 - Stacks and Queues#The Stack ADT]] - Call stack

---

*Recursion is powerful when used appropriately - let the problem guide the solution.*
