# Python None

`None` is a special constant in Python representing the absence of a value.

## None Basics

```python
x = None

print(x)         # None
print(type(x))   # <class 'NoneType'>
```

## Checking for None

```python
x = None

# Correct way
if x is None:
    print("x is None")

# Also correct
if x is not None:
    print("x has a value")

# Not recommended (but works)
if x == None:
    print("x is None")
```

## Function Returns

Functions without explicit return statement return `None`:

```python
def greet(name):
    print(f"Hello, {name}!")

result = greet("Alice")
print(result)  # None

def add(a, b):
    return a + b  # Explicit return

result = add(5, 3)
print(result)  # 8
```

## Default Arguments

```python
def process_data(data=None):
    if data is None:
        data = []
    data.append(1)
    return data

print(process_data())      # [1]
print(process_data([5]))   # [5, 1]
```

## None vs False

```python
x = None
y = False

print(x is None)    # True
print(y is None)    # False

# Both are falsy
if not x:
    print("x is falsy")

if not y:
    print("y is falsy")

# But they're different
print(x == y)    # False
print(x is y)    # False
```

## Dictionary Values

```python
data = {"name": "John", "age": None}

if data["age"] is None:
    print("Age not provided")

# get() with default
age = data.get("age", 0)
```

## Practical Examples

```python
# Optional parameter
def greet(name, title=None):
    if title is None:
        print(f"Hello, {name}!")
    else:
        print(f"Hello, {title} {name}!")

# Initialization
current_user = None

def login(username):
    global current_user
    current_user = username

def logout():
    global current_user
    current_user = None

# Sentinel value
def find_item(items, target):
    for i, item in enumerate(items):
        if item == target:
            return i
    return None  # Not found

index = find_item([1, 2, 3], 5)
if index is None:
    print("Not found")
```

---

**Related:** [[Python Data Types]] | [[Python Booleans]] | [[Python]]
