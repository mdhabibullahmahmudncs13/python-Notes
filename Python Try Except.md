# Python Try Except

Handle errors and exceptions in Python.

## Basic Try Except

```python
try:
    print(x)
except:
    print("An error occurred")
```

## Specific Exception

```python
try:
    print(x)
except NameError:
    print("Variable x is not defined")
except:
    print("Something else went wrong")
```

## Multiple Exceptions

```python
try:
    # Code that may raise exception
    result = 10 / 0
except (ZeroDivisionError, TypeError):
    print("Math error")
```

## Else Clause

Runs if no exception:

```python
try:
    print("Hello")
except:
    print("Error")
else:
    print("No error occurred")
```

## Finally Clause

Always executes:

```python
try:
    file = open("file.txt")
except:
    print("File not found")
finally:
    print("Cleanup code")
```

## Raise Exception

```python
x = -1

if x < 0:
    raise Exception("No negative numbers!")

# Specific exception
if x < 0:
    raise ValueError("No negative numbers!")
```

## Custom Exceptions

```python
class MyError(Exception):
    pass

try:
    raise MyError("Custom error message")
except MyError as e:
    print(e)
```

## Common Exceptions

```python
NameError       # Variable not defined
TypeError       # Wrong type
ValueError      # Wrong value
KeyError        # Key not in dict
IndexError      # Index out of range
FileNotFoundError  # File not found
ZeroDivisionError  # Division by zero
AttributeError  # Attribute doesn't exist
```

## Exception Object

```python
try:
    result = 10 / 0
except ZeroDivisionError as e:
    print(f"Error: {e}")
```

## Practical Examples

```python
# File handling
try:
    with open("file.txt", "r") as file:
        content = file.read()
except FileNotFoundError:
    print("File not found")
except PermissionError:
    print("No permission to read file")

# User input
try:
    age = int(input("Enter age: "))
except ValueError:
    print("Please enter a number")

# Dictionary access
data = {"name": "John"}
try:
    print(data["age"])
except KeyError:
    print("Key not found")
    data["age"] = 0
```

---

**Related:** [[Python]] | [[Python File Handling]] | [[Python Functions]]
