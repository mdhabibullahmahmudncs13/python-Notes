# Python Dictionaries

Dictionaries store data in key-value pairs. They are ordered (Python 3.7+), mutable, and don't allow duplicate keys.

## Creating Dictionaries

```python
# Using curly braces
person = {
    "name": "John",
    "age": 36,
    "country": "Norway"
}

# Using dict() constructor
person = dict(name="John", age=36, country="Norway")

# Empty dictionary
empty = {}
empty = dict()

# From list of tuples
person = dict([("name", "John"), ("age", 36)])
```

## Accessing Items

```python
person = {"name": "John", "age": 36}

# Using key
name = person["name"]  # Error if key doesn't exist

# Using get()
name = person.get("name")  # Returns None if not found
name = person.get("city", "Unknown")  # Default value

# Get all keys
keys = person.keys()

# Get all values
values = person.values()

# Get key-value pairs
items = person.items()
```

## Changing Items

```python
person = {"name": "John", "age": 36}

# Change value
person["age"] = 40

# Using update()
person.update({"age": 40})
person.update({"city": "Oslo"})  # Adds if doesn't exist
```

## Adding Items

```python
person = {"name": "John"}

# Direct assignment
person["age"] = 36

# Using update()
person.update({"country": "Norway"})

# Multiple items
person.update({
    "city": "Oslo",
    "job": "Developer"
})
```

## Removing Items

```python
person = {"name": "John", "age": 36, "country": "Norway"}

# Remove specific key
person.pop("age")

# Remove last inserted item (3.7+)
person.popitem()

# Delete specific key
del person["country"]

# Clear all items
person.clear()

# Delete dictionary
del person
```

## Looping Through Dictionaries

```python
person = {"name": "John", "age": 36, "country": "Norway"}

# Loop through keys
for key in person:
    print(key)

for key in person.keys():
    print(key)

# Loop through values
for value in person.values():
    print(value)

# Loop through key-value pairs
for key, value in person.items():
    print(f"{key}: {value}")
```

## Copying Dictionaries

```python
original = {"name": "John", "age": 36}

# Using copy()
copy1 = original.copy()

# Using dict()
copy2 = dict(original)

# Shallow vs Deep copy
import copy
nested = {"person": {"name": "John"}}
shallow = nested.copy()
deep = copy.deepcopy(nested)
```

## Nested Dictionaries

```python
# Nested dictionary
family = {
    "child1": {
        "name": "Emil",
        "year": 2004
    },
    "child2": {
        "name": "Tobias",
        "year": 2007
    }
}

# Access nested values
print(family["child1"]["name"])  # Emil

# Create nested from existing
child1 = {"name": "Emil", "year": 2004}
child2 = {"name": "Tobias", "year": 2007}
family = {
    "child1": child1,
    "child2": child2
}

# Loop through nested
for name, info in family.items():
    print(f"\n{name}:")
    for key, value in info.items():
        print(f"  {key}: {value}")
```

## Dictionary Methods

```python
# Access
dict.get(key, default)
dict.keys()
dict.values()
dict.items()

# Modify
dict[key] = value
dict.update(dict2)
dict.setdefault(key, default)

# Remove
dict.pop(key, default)
dict.popitem()
dict.clear()

# Other
dict.copy()
dict.fromkeys(keys, value)
```

## Dictionary Comprehension

```python
# Basic
squares = {x: x**2 for x in range(6)}
# {0: 0, 1: 1, 2: 4, 3: 9, 4: 16, 5: 25}

# With condition
even_squares = {x: x**2 for x in range(10) if x % 2 == 0}
# {0: 0, 2: 4, 4: 16, 6: 36, 8: 64}

# From lists
keys = ['a', 'b', 'c']
values = [1, 2, 3]
dict_from_lists = {k: v for k, v in zip(keys, values)}
# {'a': 1, 'b': 2, 'c': 3}

# Swap keys and values
original = {'a': 1, 'b': 2}
swapped = {v: k for k, v in original.items()}
# {1: 'a', 2: 'b'}
```

## Common Operations

```python
person = {"name": "John", "age": 36}

# Length
len(person)  # 2

# Check if key exists
if "name" in person:
    print("Name exists")

# Get with default
city = person.get("city", "Unknown")

# setdefault (get or set)
country = person.setdefault("country", "USA")
# Returns "USA" and adds to dict if not present
```

## Merging Dictionaries

```python
dict1 = {"a": 1, "b": 2}
dict2 = {"c": 3, "d": 4}

# Using update()
dict1.update(dict2)

# Using ** (Python 3.5+)
merged = {**dict1, **dict2}

# Using | (Python 3.9+)
merged = dict1 | dict2
```

## OrderedDict

Maintains insertion order (less important since Python 3.7+):

```python
from collections import OrderedDict

# Create OrderedDict
ordered = OrderedDict()
ordered['a'] = 1
ordered['b'] = 2
ordered['c'] = 3

# Move to end
ordered.move_to_end('a')

# Reverse
ordered = OrderedDict(reversed(list(ordered.items())))
```

## DefaultDict

Provides default values for missing keys:

```python
from collections import defaultdict

# With list
dd = defaultdict(list)
dd['a'].append(1)  # No KeyError

# With int
dd = defaultdict(int)
dd['count'] += 1  # Starts at 0

# With custom function
dd = defaultdict(lambda: 'N/A')
print(dd['missing'])  # 'N/A'
```

## Practical Examples

```python
# Count occurrences
text = "hello world"
count = {}
for char in text:
    count[char] = count.get(char, 0) + 1

# Or with defaultdict
from collections import defaultdict
count = defaultdict(int)
for char in text:
    count[char] += 1

# Group items
from collections import defaultdict
students = [
    {"name": "John", "grade": "A"},
    {"name": "Jane", "grade": "B"},
    {"name": "Bob", "grade": "A"}
]
by_grade = defaultdict(list)
for student in students:
    by_grade[student["grade"]].append(student["name"])
```

---

**Related:** [[Data Structures]] | [[Python Lists]] | [[Python Sets]] | [[Python For Loops]]
