# Python Lists

Lists are ordered, mutable collections that can contain items of different types.

## Creating Lists

```python
# Empty list
my_list = []
my_list = list()

# List with items
fruits = ["apple", "banana", "cherry"]
numbers = [1, 2, 3, 4, 5]
mixed = [1, "hello", True, 3.14]
```

## Accessing Items

```python
fruits = ["apple", "banana", "cherry"]

# By index (0-based)
print(fruits[0])   # apple
print(fruits[1])   # banana
print(fruits[-1])  # cherry (last item)
print(fruits[-2])  # banana

# Check if item exists
if "apple" in fruits:
    print("Apple is in the list")
```

## Slicing

```python
fruits = ["apple", "banana", "cherry", "orange", "kiwi"]

print(fruits[1:3])   # ['banana', 'cherry']
print(fruits[:3])    # ['apple', 'banana', 'cherry']
print(fruits[2:])    # ['cherry', 'orange', 'kiwi']
print(fruits[-3:-1]) # ['cherry', 'orange']
print(fruits[::2])   # ['apple', 'cherry', 'kiwi'] (every 2nd)
print(fruits[::-1])  # Reverse the list
```

## Changing Items

```python
fruits = ["apple", "banana", "cherry"]

# Change single item
fruits[1] = "blackberry"

# Change range
fruits[1:3] = ["mango", "orange"]

# Replace with more items
fruits[1:2] = ["kiwi", "melon"]
```

## Adding Items

```python
fruits = ["apple", "banana"]

# Append (add to end)
fruits.append("cherry")

# Insert at position
fruits.insert(1, "orange")  # Insert at index 1

# Extend (add multiple items)
fruits.extend(["mango", "kiwi"])

# Using + operator
fruits = fruits + ["grape"]

# Using +=
fruits += ["pear"]
```

## Removing Items

```python
fruits = ["apple", "banana", "cherry", "orange"]

# Remove specific item
fruits.remove("banana")

# Remove by index
fruits.pop(1)      # Removes and returns item at index 1
fruits.pop()       # Removes and returns last item

# Delete by index
del fruits[0]

# Delete a range
del fruits[1:3]

# Clear the list
fruits.clear()
```

## Looping Through Lists

```python
fruits = ["apple", "banana", "cherry"]

# Basic loop
for fruit in fruits:
    print(fruit)

# With index
for i in range(len(fruits)):
    print(f"{i}: {fruits[i]}")

# Using enumerate
for index, fruit in enumerate(fruits):
    print(f"{index}: {fruit}")

# While loop
i = 0
while i < len(fruits):
    print(fruits[i])
    i += 1
```

## List Comprehension

Create lists in a concise way:

```python
# Basic syntax: [expression for item in iterable]
squares = [x**2 for x in range(10)]
# [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

# With condition
evens = [x for x in range(20) if x % 2 == 0]
# [0, 2, 4, 6, 8, 10, 12, 14, 16, 18]

# Transform items
fruits = ["apple", "banana", "cherry"]
upper_fruits = [fruit.upper() for fruit in fruits]
# ['APPLE', 'BANANA', 'CHERRY']

# Nested comprehension
matrix = [[i*j for j in range(3)] for i in range(3)]
# [[0, 0, 0], [0, 1, 2], [0, 2, 4]]
```

## Sorting Lists

```python
numbers = [5, 2, 8, 1, 9]

# Sort ascending
numbers.sort()           # [1, 2, 5, 8, 9]

# Sort descending
numbers.sort(reverse=True)  # [9, 8, 5, 2, 1]

# sorted() - returns new list
nums = [5, 2, 8, 1, 9]
sorted_nums = sorted(nums)  # Original unchanged

# Custom sorting
fruits = ["banana", "apple", "cherry"]
fruits.sort(key=len)  # Sort by length

# Reverse
numbers.reverse()
```

## Copying Lists

```python
original = [1, 2, 3]

# Using copy()
copy1 = original.copy()

# Using list()
copy2 = list(original)

# Using slice
copy3 = original[:]

# Shallow vs Deep copy
import copy
nested = [[1, 2], [3, 4]]
shallow = nested.copy()      # Shallow copy
deep = copy.deepcopy(nested) # Deep copy
```

## Joining Lists

```python
list1 = [1, 2, 3]
list2 = [4, 5, 6]

# Using +
list3 = list1 + list2

# Using extend()
list1.extend(list2)

# Using append() for each item
for item in list2:
    list1.append(item)
```

## List Methods

```python
# Add/Remove
list.append(item)
list.insert(index, item)
list.extend(iterable)
list.remove(item)
list.pop(index)
list.clear()

# Search
list.index(item)
list.count(item)

# Sort/Reverse
list.sort()
list.reverse()

# Copy
list.copy()
```

## Common Operations

```python
fruits = ["apple", "banana", "cherry"]

# Length
len(fruits)  # 3

# Count occurrences
fruits.count("apple")  # 1

# Find index
fruits.index("banana")  # 1

# Min/Max (for comparable items)
numbers = [3, 1, 4, 1, 5]
min(numbers)  # 1
max(numbers)  # 5
sum(numbers)  # 14
```

## Nested Lists

```python
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

# Access nested items
print(matrix[0][1])  # 2
print(matrix[1][2])  # 6

# Loop through nested lists
for row in matrix:
    for item in row:
        print(item, end=" ")
```

---

**Related:** [[Data Structures]] | [[Python Tuples]] | [[Python For Loops]] | [[Python Iterators]]
