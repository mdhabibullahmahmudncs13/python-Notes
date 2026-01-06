# Python Range

The `range()` function returns a sequence of numbers.

## Basic Syntax

```python
range(stop)
range(start, stop)
range(start, stop, step)
```

## Creating Ranges

```python
# From 0 to 5 (exclusive)
r = range(6)
# 0, 1, 2, 3, 4, 5

# From 2 to 6 (exclusive)
r = range(2, 6)
# 2, 3, 4, 5

# From 0 to 10, step 2
r = range(0, 10, 2)
# 0, 2, 4, 6, 8

# Negative step (countdown)
r = range(10, 0, -1)
# 10, 9, 8, 7, 6, 5, 4, 3, 2, 1

# Negative numbers
r = range(-5, 5)
# -5, -4, -3, -2, -1, 0, 1, 2, 3, 4
```

## Using Range in Loops

```python
# Print 0 to 4
for i in range(5):
    print(i)

# Print 2 to 5
for i in range(2, 6):
    print(i)

# Print even numbers
for i in range(0, 10, 2):
    print(i)

# Countdown
for i in range(10, 0, -1):
    print(i)
```

## Converting Range to List

```python
# Range is not a list
r = range(5)
print(type(r))  # <class 'range'>

# Convert to list
numbers = list(range(5))
# [0, 1, 2, 3, 4]

# Convert to tuple
numbers = tuple(range(5))
# (0, 1, 2, 3, 4)
```

## Accessing Range Elements

```python
r = range(10, 20)

# Access by index
print(r[0])   # 10
print(r[5])   # 15
print(r[-1])  # 19

# Slicing
print(r[2:5])   # range(12, 15)
print(list(r[2:5]))  # [12, 13, 14]

# Length
print(len(r))  # 10

# Check membership
print(15 in r)  # True
print(25 in r)  # False
```

## Range with enumerate()

```python
for index, value in enumerate(range(10, 15)):
    print(f"Index {index}: Value {value}")
# Index 0: Value 10
# Index 1: Value 11
# ...
```

## Range for List Indices

```python
fruits = ["apple", "banana", "cherry", "date"]

# Loop through indices
for i in range(len(fruits)):
    print(f"{i}: {fruits[i]}")

# Loop through reversed indices
for i in range(len(fruits)-1, -1, -1):
    print(fruits[i])
```

## Empty Range

```python
# When start >= stop (for positive step)
r = range(5, 5)
print(list(r))  # []

r = range(5, 2)
print(list(r))  # []

# When start <= stop (for negative step)
r = range(2, 5, -1)
print(list(r))  # []
```

## Range Properties

```python
r = range(5, 15, 2)

# Start
print(r.start)  # 5

# Stop
print(r.stop)   # 15

# Step
print(r.step)   # 2

# Count
print(r.count(7))   # 1
print(r.count(8))   # 0

# Index
print(r.index(7))   # 1
```

## Practical Examples

```python
# Create list of squares
squares = [x**2 for x in range(10)]
# [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

# Create multiplication table
for i in range(1, 11):
    for j in range(1, 11):
        print(f"{i} x {j} = {i*j}")

# Sum of numbers
total = sum(range(1, 101))  # Sum of 1 to 100

# Repeat action n times
for _ in range(5):
    print("Hello")

# Create coordinates
coords = [(x, y) for x in range(3) for y in range(3)]
# [(0,0), (0,1), (0,2), (1,0), (1,1), (1,2), (2,0), (2,1), (2,2)]
```

## Range vs List

### Range (Memory Efficient)
```python
# Uses constant memory regardless of size
r = range(1000000)
```

### List (More Memory)
```python
# Stores all elements in memory
numbers = list(range(1000000))
```

## Reversed Range

```python
# Using reversed()
for i in reversed(range(5)):
    print(i)  # 4, 3, 2, 1, 0

# Using negative step
for i in range(4, -1, -1):
    print(i)  # 4, 3, 2, 1, 0
```

## Range Comparison

```python
r1 = range(5)
r2 = range(5)
r3 = range(0, 5)

print(r1 == r2)  # True
print(r1 == r3)  # True

# Ranges are equal if start, stop, and step are equal
r4 = range(0, 10, 2)
r5 = range(0, 10, 2)
print(r4 == r5)  # True
```

---

**Related:** [[Data Structures]] | [[Python For Loops]] | [[Python Lists]] | [[Python Iterators]]
