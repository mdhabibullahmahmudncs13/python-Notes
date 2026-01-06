# Python Tuples

Tuples are ordered, immutable collections.

## Creating Tuples

```python
# Empty tuple
my_tuple = ()
my_tuple = tuple()

# Tuple with items
fruits = ("apple", "banana", "cherry")

# Single item (comma required)
single = ("apple",)  # Tuple
not_tuple = ("apple")  # String

# Without parentheses
coords = 10, 20, 30
```

## Accessing Items

```python
fruits = ("apple", "banana", "cherry")

# By index
print(fruits[0])   # apple
print(fruits[-1])  # cherry

# Check if exists
if "apple" in fruits:
    print("Apple exists")
```

## Slicing

```python
fruits = ("apple", "banana", "cherry", "orange", "kiwi")

print(fruits[1:3])   # ('banana', 'cherry')
print(fruits[:3])    # ('apple', 'banana', 'cherry')
print(fruits[2:])    # ('cherry', 'orange', 'kiwi')
print(fruits[-3:-1]) # ('cherry', 'orange')
```

## Update Tuples

Tuples are immutable, but you can work around it:

```python
fruits = ("apple", "banana", "cherry")

# Convert to list, modify, convert back
temp = list(fruits)
temp[1] = "kiwi"
fruits = tuple(temp)

# Add items
temp = list(fruits)
temp.append("orange")
fruits = tuple(temp)

# Add tuple to tuple
fruits = fruits + ("mango",)

# Remove items (convert to list)
temp = list(fruits)
temp.remove("apple")
fruits = tuple(temp)

# Delete tuple completely
del fruits
```

## Unpacking Tuples

```python
# Basic unpacking
fruits = ("apple", "banana", "cherry")
x, y, z = fruits
print(x)  # apple
print(y)  # banana

# Using asterisk (*)
fruits = ("apple", "banana", "cherry", "strawberry", "raspberry")
x, y, *rest = fruits
print(x)     # apple
print(rest)  # ['cherry', 'strawberry', 'raspberry']

# Asterisk in middle
x, *middle, z = fruits
print(middle)  # ['banana', 'cherry', 'strawberry']
```

## Looping Through Tuples

```python
fruits = ("apple", "banana", "cherry")

# Basic loop
for fruit in fruits:
    print(fruit)

# With index
for i in range(len(fruits)):
    print(fruits[i])

# Using enumerate
for index, fruit in enumerate(fruits):
    print(f"{index}: {fruit}")

# While loop
i = 0
while i < len(fruits):
    print(fruits[i])
    i += 1
```

## Joining Tuples

```python
tuple1 = (1, 2, 3)
tuple2 = (4, 5, 6)

# Using +
tuple3 = tuple1 + tuple2
# (1, 2, 3, 4, 5, 6)

# Multiply tuple
repeated = tuple1 * 2
# (1, 2, 3, 1, 2, 3)
```

## Tuple Methods

Tuples have only two methods:

```python
fruits = ("apple", "banana", "cherry", "apple")

# Count occurrences
count = fruits.count("apple")  # 2

# Find index
index = fruits.index("banana")  # 1
```

## Common Operations

```python
fruits = ("apple", "banana", "cherry")

# Length
len(fruits)  # 3

# Min/Max
numbers = (3, 1, 4, 1, 5)
min(numbers)  # 1
max(numbers)  # 5
sum(numbers)  # 14

# Membership
"apple" in fruits  # True
```

## Nested Tuples

```python
nested = ((1, 2), (3, 4), (5, 6))

# Access
print(nested[0])     # (1, 2)
print(nested[0][1])  # 2

# Unpack nested
(a, b), (c, d) = ((1, 2), (3, 4))
```

## Why Use Tuples?

1. **Immutability**: Data integrity - can't be changed accidentally
2. **Performance**: Faster than lists
3. **Dictionary keys**: Tuples can be dict keys (lists can't)
4. **Data integrity**: Protect data from modification

```python
# Tuple as dictionary key
locations = {
    (40.7128, -74.0060): "New York",
    (51.5074, -0.1278): "London"
}

# Function returning multiple values
def get_coordinates():
    return (10, 20)  # Returns tuple

x, y = get_coordinates()
```

## Named Tuples

For more readable code:

```python
from collections import namedtuple

# Define named tuple
Point = namedtuple('Point', ['x', 'y'])

# Create instance
p = Point(10, 20)

# Access by name or index
print(p.x)    # 10
print(p[0])   # 10
print(p.y)    # 20
```

---

**Related:** [[Data Structures]] | [[Python Lists]] | [[Python Dictionaries]] | [[Python For Loops]]
