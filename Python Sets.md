# Python Sets

Sets are unordered collections of unique items.

## Creating Sets

```python
# Using curly braces
fruits = {"apple", "banana", "cherry"}

# Using set() constructor
fruits = set(["apple", "banana", "cherry"])

# Empty set (must use set())
empty = set()  # NOT {}

# Duplicates are removed
numbers = {1, 2, 2, 3, 3, 3}
print(numbers)  # {1, 2, 3}
```

## Accessing Items

You cannot access items by index (sets are unordered), but you can loop through them:

```python
fruits = {"apple", "banana", "cherry"}

# Loop through set
for fruit in fruits:
    print(fruit)

# Check if exists
if "apple" in fruits:
    print("Apple exists")
```

## Adding Items

```python
fruits = {"apple", "banana"}

# Add single item
fruits.add("cherry")

# Add multiple items (from any iterable)
fruits.update(["orange", "mango"])
fruits.update({"kiwi", "grape"})
fruits.update(("pear", "melon"))
```

## Removing Items

```python
fruits = {"apple", "banana", "cherry"}

# Remove (raises error if not found)
fruits.remove("banana")

# Discard (no error if not found)
fruits.discard("orange")  # No error

# Pop (removes random item)
item = fruits.pop()

# Clear all items
fruits.clear()

# Delete set
del fruits
```

## Looping Through Sets

```python
fruits = {"apple", "banana", "cherry"}

# Basic loop
for fruit in fruits:
    print(fruit)
```

## Joining Sets

### Union

Combine all unique items from multiple sets:

```python
set1 = {1, 2, 3}
set2 = {3, 4, 5}

# Using union()
set3 = set1.union(set2)
# {1, 2, 3, 4, 5}

# Using |
set3 = set1 | set2
# {1, 2, 3, 4, 5}

# Multiple sets
set4 = set1.union(set2, {6, 7})
```

### Intersection

Get items that exist in both sets:

```python
set1 = {1, 2, 3}
set2 = {3, 4, 5}

# Using intersection()
set3 = set1.intersection(set2)
# {3}

# Using &
set3 = set1 & set2
# {3}
```

### Difference

Get items in first set but not in second:

```python
set1 = {1, 2, 3}
set2 = {3, 4, 5}

# Using difference()
set3 = set1.difference(set2)
# {1, 2}

# Using -
set3 = set1 - set2
# {1, 2}
```

### Symmetric Difference

Get items in either set, but not in both:

```python
set1 = {1, 2, 3}
set2 = {3, 4, 5}

# Using symmetric_difference()
set3 = set1.symmetric_difference(set2)
# {1, 2, 4, 5}

# Using ^
set3 = set1 ^ set2
# {1, 2, 4, 5}
```

## Set Methods

```python
# Add/Remove
set.add(item)
set.update(iterable)
set.remove(item)      # Error if not found
set.discard(item)     # No error
set.pop()             # Remove random
set.clear()

# Set operations
set1.union(set2)
set1.intersection(set2)
set1.difference(set2)
set1.symmetric_difference(set2)

# Update operations (modify in place)
set1.update(set2)                      # Union
set1.intersection_update(set2)         # Intersection
set1.difference_update(set2)           # Difference
set1.symmetric_difference_update(set2) # Symmetric difference

# Comparison
set1.issubset(set2)
set1.issuperset(set2)
set1.isdisjoint(set2)  # No common elements

# Copy
set.copy()
```

## Frozenset

Immutable version of set:

```python
# Create frozenset
frozen = frozenset([1, 2, 3])

# Cannot modify
# frozen.add(4)  # Error

# Can be used as dictionary key
dict_with_frozen_key = {
    frozenset([1, 2]): "value1",
    frozenset([3, 4]): "value2"
}

# Set operations work
frozen1 = frozenset([1, 2, 3])
frozen2 = frozenset([3, 4, 5])
result = frozen1 | frozen2  # frozenset({1, 2, 3, 4, 5})
```

## Set Comprehension

```python
# Basic
squares = {x**2 for x in range(10)}
# {0, 1, 4, 9, 16, 25, 36, 49, 64, 81}

# With condition
evens = {x for x in range(20) if x % 2 == 0}
# {0, 2, 4, 6, 8, 10, 12, 14, 16, 18}
```

## Common Operations

```python
fruits = {"apple", "banana", "cherry"}

# Length
len(fruits)  # 3

# Check membership
"apple" in fruits  # True

# Convert to list
fruit_list = list(fruits)

# Remove duplicates from list
numbers = [1, 2, 2, 3, 3, 3, 4]
unique = list(set(numbers))  # [1, 2, 3, 4]
```

## Practical Examples

```python
# Remove duplicates
def remove_duplicates(items):
    return list(set(items))

# Find common elements
list1 = [1, 2, 3, 4]
list2 = [3, 4, 5, 6]
common = set(list1) & set(list2)  # {3, 4}

# Find unique elements
unique = set(list1) ^ set(list2)  # {1, 2, 5, 6}

# Check if lists have same elements
set(list1) == set(list2)
```

---

**Related:** [[Data Structures]] | [[Python Lists]] | [[Python Dictionaries]] | [[Python Frozenset]]
