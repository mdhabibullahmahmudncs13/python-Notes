# Python Recursion

Recursion is when a function calls itself.

## Basic Recursion

```python
def countdown(n):
    if n <= 0:
        print("Blast off!")
    else:
        print(n)
        countdown(n - 1)

countdown(5)
# 5 4 3 2 1 Blast off!
```

## Base Case

Every recursive function needs a base case to stop:

```python
def factorial(n):
    # Base case
    if n == 0 or n == 1:
        return 1
    # Recursive case
    return n * factorial(n - 1)

print(factorial(5))  # 120
```

## Factorial Example

```python
# 5! = 5 * 4 * 3 * 2 * 1 = 120

def factorial(n):
    if n == 0:
        return 1
    return n * factorial(n - 1)

# How it works:
# factorial(5) = 5 * factorial(4)
# factorial(4) = 4 * factorial(3)
# factorial(3) = 3 * factorial(2)
# factorial(2) = 2 * factorial(1)
# factorial(1) = 1 * factorial(0)
# factorial(0) = 1
```

## Fibonacci Sequence

```python
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n-1) + fibonacci(n-2)

# First 10 Fibonacci numbers
for i in range(10):
    print(fibonacci(i), end=" ")
# 0 1 1 2 3 5 8 13 21 34
```

## Sum of Numbers

```python
def sum_numbers(n):
    if n == 0:
        return 0
    return n + sum_numbers(n - 1)

print(sum_numbers(5))  # 15 (5+4+3+2+1)
```

## List Sum

```python
def sum_list(numbers):
    if not numbers:
        return 0
    return numbers[0] + sum_list(numbers[1:])

print(sum_list([1, 2, 3, 4, 5]))  # 15
```

## Binary Search (Recursive)

```python
def binary_search(arr, target, left, right):
    if left > right:
        return -1
    
    mid = (left + right) // 2
    
    if arr[mid] == target:
        return mid
    elif arr[mid] > target:
        return binary_search(arr, target, left, mid - 1)
    else:
        return binary_search(arr, target, mid + 1, right)

arr = [1, 2, 3, 4, 5, 6, 7, 8, 9]
result = binary_search(arr, 5, 0, len(arr) - 1)
print(result)  # 4
```

## Recursion with Strings

```python
# Reverse string
def reverse_string(s):
    if len(s) == 0:
        return s
    return reverse_string(s[1:]) + s[0]

print(reverse_string("hello"))  # olleh

# Check palindrome
def is_palindrome(s):
    if len(s) <= 1:
        return True
    if s[0] != s[-1]:
        return False
    return is_palindrome(s[1:-1])

print(is_palindrome("radar"))  # True
```

## Recursion vs Iteration

```python
# Recursive factorial
def factorial_recursive(n):
    if n == 0:
        return 1
    return n * factorial_recursive(n - 1)

# Iterative factorial (more efficient)
def factorial_iterative(n):
    result = 1
    for i in range(1, n + 1):
        result *= i
    return result
```

## Maximum Recursion Depth

Python has a recursion limit:

```python
import sys

# Check limit
print(sys.getrecursionlimit())  # Usually 1000

# Set new limit (be careful!)
sys.setrecursionlimit(2000)

# Too deep recursion causes error
# factorial(2000)  # RecursionError
```

## Tail Recursion

Python doesn't optimize tail recursion:

```python
# Regular recursion
def factorial(n):
    if n == 0:
        return 1
    return n * factorial(n - 1)

# Tail recursive (not optimized in Python)
def factorial_tail(n, accumulator=1):
    if n == 0:
        return accumulator
    return factorial_tail(n - 1, n * accumulator)
```

## Memoization

Cache results to improve performance:

```python
# Without memoization (slow)
def fib(n):
    if n <= 1:
        return n
    return fib(n-1) + fib(n-2)

# With memoization (fast)
def fib_memo(n, memo={}):
    if n in memo:
        return memo[n]
    if n <= 1:
        return n
    memo[n] = fib_memo(n-1, memo) + fib_memo(n-2, memo)
    return memo[n]

# Using lru_cache decorator
from functools import lru_cache

@lru_cache(maxsize=None)
def fib_cached(n):
    if n <= 1:
        return n
    return fib_cached(n-1) + fib_cached(n-2)

print(fib_cached(100))  # Very fast!
```

## Practical Examples

```python
# Calculate power
def power(base, exp):
    if exp == 0:
        return 1
    return base * power(base, exp - 1)

# GCD (Greatest Common Divisor)
def gcd(a, b):
    if b == 0:
        return a
    return gcd(b, a % b)

# Flatten nested list
def flatten(lst):
    result = []
    for item in lst:
        if isinstance(item, list):
            result.extend(flatten(item))
        else:
            result.append(item)
    return result

nested = [1, [2, 3], [4, [5, 6]], 7]
print(flatten(nested))  # [1, 2, 3, 4, 5, 6, 7]

# Directory tree traversal
import os

def list_files(path, indent=0):
    for item in os.listdir(path):
        print("  " * indent + item)
        full_path = os.path.join(path, item)
        if os.path.isdir(full_path):
            list_files(full_path, indent + 1)
```

---

**Related:** [[Python Functions]] | [[Functions and Advanced Concepts]] | [[Python Decorators]]
