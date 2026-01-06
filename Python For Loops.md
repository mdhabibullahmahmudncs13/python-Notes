# Python For Loops

For loops iterate over sequences (lists, tuples, strings, etc.) or other iterable objects.

## Basic For Loop

```python
# Iterate over list
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(fruit)

# Iterate over string
for char in "Python":
    print(char)
```

## For Loop with Range

```python
# 0 to 4
for i in range(5):
    print(i)

# 2 to 5
for i in range(2, 6):
    print(i)

# 0 to 10, step 2
for i in range(0, 11, 2):
    print(i)  # 0, 2, 4, 6, 8, 10
```

See [[Python Range]] for more details.

## Break Statement

Exit the loop early:

```python
fruits = ["apple", "banana", "cherry", "date"]
for fruit in fruits:
    if fruit == "cherry":
        break
    print(fruit)

# Output: apple banana
```

## Continue Statement

Skip to next iteration:

```python
fruits = ["apple", "banana", "cherry", "date"]
for fruit in fruits:
    if fruit == "banana":
        continue
    print(fruit)

# Output: apple cherry date
```

## For...Else

The `else` block runs when the loop completes normally (not broken):

```python
for i in range(5):
    print(i)
else:
    print("Loop finished")

# Output: 0 1 2 3 4 Loop finished
```

```python
# With break (else doesn't run)
for i in range(5):
    if i == 3:
        break
    print(i)
else:
    print("Loop finished")  # Won't print

# Output: 0 1 2
```

## Nested For Loops

```python
# Multiplication table
for i in range(1, 4):
    for j in range(1, 4):
        print(f"{i} x {j} = {i*j}")
    print()  # Blank line
```

## Iterating Over Dictionaries

```python
person = {"name": "John", "age": 36, "country": "Norway"}

# Iterate over keys
for key in person:
    print(key)

for key in person.keys():
    print(key)

# Iterate over values
for value in person.values():
    print(value)

# Iterate over key-value pairs
for key, value in person.items():
    print(f"{key}: {value}")
```

See [[Python Dictionaries]] for more details.

## Enumerate()

Get index and value together:

```python
fruits = ["apple", "banana", "cherry"]

for index, fruit in enumerate(fruits):
    print(f"{index}: {fruit}")

# Output:
# 0: apple
# 1: banana
# 2: cherry

# Start index from 1
for index, fruit in enumerate(fruits, start=1):
    print(f"{index}: {fruit}")
```

## Zip()

Iterate over multiple sequences simultaneously:

```python
names = ["John", "Jane", "Bob"]
ages = [25, 30, 35]

for name, age in zip(names, ages):
    print(f"{name} is {age} years old")

# Output:
# John is 25 years old
# Jane is 30 years old
# Bob is 35 years old
```

## Reversed()

Iterate in reverse:

```python
fruits = ["apple", "banana", "cherry"]

for fruit in reversed(fruits):
    print(fruit)

# Output: cherry banana apple
```

## Sorted()

Iterate in sorted order:

```python
numbers = [3, 1, 4, 1, 5, 9]

for num in sorted(numbers):
    print(num)
# Output: 1 1 3 4 5 9

# Reverse sort
for num in sorted(numbers, reverse=True):
    print(num)
# Output: 9 5 4 3 1 1
```

## List Comprehension

Create lists concisely:

```python
# Basic
squares = [x**2 for x in range(10)]
# [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

# With condition
evens = [x for x in range(20) if x % 2 == 0]
# [0, 2, 4, 6, 8, 10, 12, 14, 16, 18]

# Transform
fruits = ["apple", "banana", "cherry"]
upper_fruits = [fruit.upper() for fruit in fruits]
# ['APPLE', 'BANANA', 'CHERRY']

# Nested
matrix = [[i*j for j in range(3)] for i in range(3)]
# [[0, 0, 0], [0, 1, 2], [0, 2, 4]]
```

See [[Python Lists]] for more on list comprehension.

## Dictionary Comprehension

```python
# Create dictionary
squares = {x: x**2 for x in range(5)}
# {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}

# From two lists
keys = ['a', 'b', 'c']
values = [1, 2, 3]
dict_comp = {k: v for k, v in zip(keys, values)}
# {'a': 1, 'b': 2, 'c': 3}
```

## Set Comprehension

```python
# Create set
squares = {x**2 for x in range(10)}
# {0, 1, 4, 9, 16, 25, 36, 49, 64, 81}
```

## Iterating Over Multiple Lists

```python
# Using zip()
list1 = [1, 2, 3]
list2 = ['a', 'b', 'c']
list3 = [10, 20, 30]

for num, letter, value in zip(list1, list2, list3):
    print(f"{num} {letter} {value}")
```

## Iterating with Index

```python
fruits = ["apple", "banana", "cherry"]

# Using enumerate()
for i, fruit in enumerate(fruits):
    print(f"{i}: {fruit}")

# Using range(len())
for i in range(len(fruits)):
    print(f"{i}: {fruits[i]}")
```

## Pass Statement

Placeholder for future code:

```python
for i in range(5):
    pass  # TODO: implement later
```

## Practical Examples

```python
# Sum of numbers
total = 0
for i in range(1, 11):
    total += i
print(f"Sum: {total}")  # 55

# Or use sum()
total = sum(range(1, 11))

# Find maximum
numbers = [3, 7, 2, 9, 1]
max_num = numbers[0]
for num in numbers:
    if num > max_num:
        max_num = num

# Or use max()
max_num = max(numbers)

# Count occurrences
text = "hello world"
count = 0
for char in text:
    if char == 'l':
        count += 1
print(f"Count of 'l': {count}")

# Or use count()
count = text.count('l')

# Filter list
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
evens = []
for num in numbers:
    if num % 2 == 0:
        evens.append(num)

# Or use list comprehension
evens = [num for num in numbers if num % 2 == 0]

# Process files in directory
import os
for filename in os.listdir('.'):
    if filename.endswith('.txt'):
        print(f"Processing {filename}")

# Create pattern
for i in range(5):
    print('*' * (i + 1))
# *
# **
# ***
# ****
# *****

# Flatten nested list
nested = [[1, 2], [3, 4], [5, 6]]
flat = []
for sublist in nested:
    for item in sublist:
        flat.append(item)
# [1, 2, 3, 4, 5, 6]

# Or use list comprehension
flat = [item for sublist in nested for item in sublist]
```

## For vs While

### Use For When:
- Iterating over a sequence
- Known number of iterations
- Processing collections

```python
for item in items:
    process(item)
```

### Use While When:
- Don't know how many iterations
- Waiting for a condition
- Event loops

```python
while condition_is_true:
    do_something()
```

## Common Patterns

```python
# Iterate with step
for i in range(0, 10, 2):
    print(i)  # 0, 2, 4, 6, 8

# Reverse iteration
for i in range(10, 0, -1):
    print(i)  # 10, 9, 8, ..., 1

# Iterate over pairs
numbers = [1, 2, 3, 4, 5]
for i in range(len(numbers) - 1):
    print(numbers[i], numbers[i + 1])

# Iterate with condition
for num in numbers:
    if num % 2 == 0:
        print(f"{num} is even")
    else:
        print(f"{num} is odd")
```

---

**Related:** [[Control Flow]] | [[Python While Loops]] | [[Python Lists]] | [[Python Range]] | [[Python Iterators]]
