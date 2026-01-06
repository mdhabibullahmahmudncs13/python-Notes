# Python Generators

Generators are functions that yield values one at a time, enabling lazy evaluation.

## Basic Generator

```python
def count_up_to(n):
    count = 1
    while count <= n:
        yield count
        count += 1

counter = count_up_to(5)
for num in counter:
    print(num)  # 1 2 3 4 5
```

## Generator Expression

```python
# List comprehension (creates full list)
squares_list = [x**2 for x in range(10)]

# Generator expression (lazy)
squares_gen = (x**2 for x in range(10))

for square in squares_gen:
    print(square)
```

## Yield vs Return

```python
# Return - returns once
def return_example():
    return 1
    return 2  # Never reached

# Yield - can yield multiple times
def yield_example():
    yield 1
    yield 2
    yield 3

for value in yield_example():
    print(value)  # 1 2 3
```

## Practical Examples

```python
# Fibonacci generator
def fibonacci(n):
    a, b = 0, 1
    for _ in range(n):
        yield a
        a, b = b, a + b

for fib in fibonacci(10):
    print(fib, end=" ")
# 0 1 1 2 3 5 8 13 21 34

# Read large file
def read_large_file(file_path):
    with open(file_path) as file:
        for line in file:
            yield line.strip()
```

---

**Related:** [[Python Functions]] | [[Python Iterators]] | [[Functions and Advanced Concepts]]
