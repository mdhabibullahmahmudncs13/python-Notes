# Python Match Statements

Match statements (structural pattern matching) were introduced in Python 3.10 for pattern matching.

## Basic Match Statement

```python
status = 404

match status:
    case 200:
        print("OK")
    case 404:
        print("Not Found")
    case 500:
        print("Internal Server Error")
    case _:
        print("Unknown status")
```

The `_` acts as a wildcard (default case).

## Match with OR Pattern

```python
status = 401

match status:
    case 401 | 403:
        print("Unauthorized or Forbidden")
    case 404:
        print("Not Found")
    case _:
        print("Other status")
```

## Matching Sequences

```python
point = (0, 0)

match point:
    case (0, 0):
        print("Origin")
    case (0, y):
        print(f"On Y-axis at {y}")
    case (x, 0):
        print(f"On X-axis at {x}")
    case (x, y):
        print(f"Point at ({x}, {y})")
```

## Matching with Lists

```python
commands = ["quit"]

match commands:
    case ["quit"]:
        print("Quitting...")
    case ["load", filename]:
        print(f"Loading {filename}")
    case ["save", filename]:
        print(f"Saving {filename}")
    case _:
        print("Unknown command")
```

## Matching Dictionaries

```python
user = {"name": "John", "role": "admin"}

match user:
    case {"role": "admin"}:
        print("Admin user")
    case {"role": "guest"}:
        print("Guest user")
    case _:
        print("Unknown role")
```

## Guards (if conditions)

Add conditions to patterns:

```python
point = (4, 5)

match point:
    case (x, y) if x == y:
        print(f"Diagonal point at {x}")
    case (x, y) if x == 0:
        print(f"On Y-axis at {y}")
    case (x, y):
        print(f"Point at ({x}, {y})")
```

## Matching Objects

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

point = Point(0, 5)

match point:
    case Point(x=0, y=0):
        print("Origin")
    case Point(x=0, y=y):
        print(f"On Y-axis at {y}")
    case Point(x=x, y=0):
        print(f"On X-axis at {x}")
    case Point(x=x, y=y):
        print(f"Point at ({x}, {y})")
```

## Capturing Values

```python
command = ["move", 10, 20]

match command:
    case ["move", x, y]:
        print(f"Moving to ({x}, {y})")
    case ["draw", *coords]:
        print(f"Drawing at coordinates: {coords}")
    case _:
        print("Unknown command")
```

## Matching Types

```python
value = 42

match value:
    case int():
        print("Integer")
    case str():
        print("String")
    case list():
        print("List")
    case _:
        print("Other type")
```

## Complex Patterns

```python
data = {"type": "user", "name": "John", "age": 30}

match data:
    case {"type": "user", "name": name, "age": age} if age >= 18:
        print(f"Adult user: {name}")
    case {"type": "user", "name": name}:
        print(f"Minor user: {name}")
    case {"type": "admin", "name": name}:
        print(f"Admin: {name}")
    case _:
        print("Unknown data type")
```

## Nested Patterns

```python
data = [("point", 0, 0), ("color", "red")]

match data:
    case [("point", x, y), ("color", color)]:
        print(f"Point at ({x}, {y}) with color {color}")
    case _:
        print("Unknown pattern")
```

## AS Pattern

Capture sub-patterns:

```python
point = (1, 2)

match point:
    case (x, y) as coord:
        print(f"Coordinate {coord} with x={x}, y={y}")
```

## Literal Patterns

```python
response = "yes"

match response:
    case "yes" | "y" | "Y":
        print("Confirmed")
    case "no" | "n" | "N":
        print("Denied")
    case _:
        print("Unknown response")
```

## Practical Examples

```python
# Command parser
def handle_command(command):
    match command.split():
        case ["quit"]:
            return "Quitting"
        case ["load", filename]:
            return f"Loading {filename}"
        case ["save", filename]:
            return f"Saving {filename}"
        case ["delete", *files]:
            return f"Deleting {len(files)} files"
        case _:
            return "Unknown command"

# HTTP status handler
def handle_status(status):
    match status:
        case 200 | 201 | 204:
            return "Success"
        case 400 | 401 | 403 | 404:
            return "Client Error"
        case 500 | 502 | 503:
            return "Server Error"
        case _:
            return "Unknown Status"

# Shape calculator
class Circle:
    def __init__(self, radius):
        self.radius = radius

class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height

def calculate_area(shape):
    match shape:
        case Circle(radius=r):
            return 3.14 * r * r
        case Rectangle(width=w, height=h):
            return w * h
        case _:
            return 0

# JSON parser
def parse_json(data):
    match data:
        case {"type": "user", "data": {"name": name, "email": email}}:
            print(f"User: {name} ({email})")
        case {"type": "error", "message": msg}:
            print(f"Error: {msg}")
        case _:
            print("Unknown JSON structure")
```

## Match vs If-Elif-Else

### Using Match (Python 3.10+)
```python
match value:
    case 1:
        print("One")
    case 2:
        print("Two")
    case _:
        print("Other")
```

### Using If-Elif-Else (All versions)
```python
if value == 1:
    print("One")
elif value == 2:
    print("Two")
else:
    print("Other")
```

Match is more powerful for complex patterns, but if-elif-else works in all Python versions.

---

**Related:** [[Control Flow]] | [[Python If Else]] | [[Python Classes and Objects]] | [[Python Dictionaries]]
