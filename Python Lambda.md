# Python Lambda

Lambda functions are small anonymous functions defined with the `lambda` keyword.
**Deep Dive:** See [[Data Structures in Python/02 - Basic Python|Basic Python]] and [[Data Structures in Python/12 - Sorting|Sorting]] for lambda functions in sorting
## Basic Syntax

```python
# Syntax: lambda arguments: expression

# Regular function
def add(x, y):
    return x + y

# Lambda equivalent
add = lambda x, y: x + y

print(add(5, 3))  # 8
```

## Single Argument

```python
square = lambda x: x ** 2
print(square(5))  # 25

double = lambda x: x * 2
print(double(10))  # 20
```

## Multiple Arguments

```python
multiply = lambda x, y: x * y
print(multiply(5, 3))  # 15

max_of_two = lambda a, b: a if a > b else b
print(max_of_two(10, 5))  # 10
```

## No Arguments

```python
get_pi = lambda: 3.14159
print(get_pi())  # 3.14159
```

## Lambda with map()

Apply function to each item:

```python
numbers = [1, 2, 3, 4, 5]

# Square each number
squared = list(map(lambda x: x ** 2, numbers))
print(squared)  # [1, 4, 9, 16, 25]

# Double each number
doubled = list(map(lambda x: x * 2, numbers))
print(doubled)  # [2, 4, 6, 8, 10]
```

## Lambda with filter()

Filter items based on condition:

```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# Get even numbers
evens = list(filter(lambda x: x % 2 == 0, numbers))
print(evens)  # [2, 4, 6, 8, 10]

# Get numbers > 5
greater_than_5 = list(filter(lambda x: x > 5, numbers))
print(greater_than_5)  # [6, 7, 8, 9, 10]
```

## Lambda with reduce()

Reduce sequence to single value:

```python
from functools import reduce

numbers = [1, 2, 3, 4, 5]

# Sum all numbers
total = reduce(lambda x, y: x + y, numbers)
print(total)  # 15

# Find maximum
maximum = reduce(lambda x, y: x if x > y else y, numbers)
print(maximum)  # 5
```

## Lambda with sorted()

Custom sorting:

```python
# Sort by absolute value
numbers = [-5, -2, 1, 3, -4]
sorted_nums = sorted(numbers, key=lambda x: abs(x))
print(sorted_nums)  # [1, -2, 3, -4, -5]

# Sort tuples by second element
pairs = [(1, 5), (2, 3), (3, 1), (4, 4)]
sorted_pairs = sorted(pairs, key=lambda x: x[1])
print(sorted_pairs)  # [(3, 1), (2, 3), (4, 4), (1, 5)]

# Sort strings by length
words = ["apple", "pie", "banana", "cat"]
sorted_words = sorted(words, key=lambda x: len(x))
print(sorted_words)  # ['pie', 'cat', 'apple', 'banana']
```

## Lambda in List Comprehension

```python
# Not common, but possible
squares = [(lambda x: x ** 2)(x) for x in range(5)]
print(squares)  # [0, 1, 4, 9, 16]

# Better to use regular comprehension
squares = [x ** 2 for x in range(5)]
```

## Lambda with Conditional

```python
# Ternary operator in lambda
max_of_two = lambda a, b: a if a > b else b
print(max_of_two(10, 20))  # 20

# Check if even
is_even = lambda x: "Even" if x % 2 == 0 else "Odd"
print(is_even(4))  # Even
print(is_even(5))  # Odd

# Absolute value
abs_value = lambda x: x if x >= 0 else -x
print(abs_value(-5))  # 5
```

## Multiple Lambdas

```python
# Dictionary of operations
operations = {
    'add': lambda x, y: x + y,
    'subtract': lambda x, y: x - y,
    'multiply': lambda x, y: x * y,
    'divide': lambda x, y: x / y if y != 0 else None
}

print(operations['add'](10, 5))       # 15
print(operations['multiply'](10, 5))  # 50
```

## Lambda with Default Arguments

```python
multiply = lambda x, y=2: x * y
print(multiply(5))     # 10
print(multiply(5, 3))  # 15
```

## Limitations of Lambda

### Single Expression Only
```python
# Can't do this in lambda
# def complex_function(x):
#     if x > 0:
#         return x ** 2
#     else:
#         return x ** 3

# Must use regular function for multiple statements
```

### No Annotations
```python
# Can't do this with lambda
def add(x: int, y: int) -> int:
    return x + y

# Lambda doesn't support type hints
add = lambda x, y: x + y
```

### No Docstrings
```python
# Can't document lambda functions
# Must use regular function for documentation
```

## Practical Examples

```python
# Convert list of strings to uppercase
words = ["hello", "world", "python"]
upper = list(map(lambda x: x.upper(), words))
print(upper)  # ['HELLO', 'WORLD', 'PYTHON']

# Filter names starting with 'A'
names = ["Alice", "Bob", "Anna", "Charlie"]
a_names = list(filter(lambda x: x.startswith('A'), names))
print(a_names)  # ['Alice', 'Anna']

# Calculate total price with tax
prices = [10, 20, 30]
with_tax = list(map(lambda x: x * 1.1, prices))
print(with_tax)  # [11.0, 22.0, 33.0]

# Sort dictionaries by value
students = [
    {"name": "John", "grade": 85},
    {"name": "Jane", "grade": 92},
    {"name": "Bob", "grade": 78}
]
sorted_students = sorted(students, key=lambda x: x['grade'], reverse=True)
print([s['name'] for s in sorted_students])  # ['Jane', 'John', 'Bob']
```

## When to Use Lambda

### Good Use Cases
```python
# Simple operations with map/filter
numbers = [1, 2, 3, 4, 5]
squared = list(map(lambda x: x ** 2, numbers))

# Simple sorting keys
words = ["apple", "pie", "banana"]
sorted_words = sorted(words, key=lambda x: len(x))

# Short-lived callbacks
button.connect('clicked', lambda: print("Clicked!"))
```

### When to Use Regular Functions
```python
# Complex logic
def complex_calculation(x):
    if x > 0:
        result = x ** 2
    else:
        result = abs(x)
    return result

# Need documentation
def calculate_area(radius):
    """Calculate area of circle."""
    return 3.14 * radius ** 2

# Reused multiple times
def validate_email(email):
    # Complex validation logic
    pass
```

## Lambda vs List Comprehension

```python
# Using lambda with map
squared = list(map(lambda x: x ** 2, range(5)))

# Using list comprehension (more Pythonic)
squared = [x ** 2 for x in range(5)]

# Using lambda with filter
evens = list(filter(lambda x: x % 2 == 0, range(10)))

# Using list comprehension (more Pythonic)
evens = [x for x in range(10) if x % 2 == 0]
```

Generally, list comprehensions are more Pythonic and readable.

---

**Related:** [[Python Functions]] | [[Python For Loops]] | [[Functions and Advanced Concepts]]
