# Object-Oriented Programming

← [[02 - Basic Python]] | [[Data Structures in Python]] | Next: [[04 - Testing]] →

## Goals of OOP

> [!important]
> Make it possible to write code that is **close to the way you think** about the things your code represents.

This makes it easier to:
- Reason about code
- Think through correctness
- Maintain and modify programs

## Classes and Objects

- **Class**: A data type (synonymous with "type" in Python)
- **Object**: An instance of a class

```python
mylist = []
print(type(mylist))        # <class 'list'>
print(isinstance(mylist, list))   # True
print(isinstance(mylist, str))    # False
```

Everything in Python is an object:

```python
def foo():
    return 0

print(type(foo))           # <class 'function'>
```

## A Simple Example: Vector Class

### Using Tuples (Before OOP)

```python
u = (3, 4)
v = (3, 6)

def add(a, b):
    return (a[0] + b[0], a[1] + b[1])

def norm(a):
    return (a[0] * a[0] + a[1] * a[1]) ** 0.5

print(norm(u))             # 5.0
print(add(u, v))           # (6, 10)
```

Problems:
- Need separate functions for each operation
- No type checking
- `u + v` doesn't work as expected

### Using a Class

```python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y
    
    def norm(self):
        return (self.x ** 2 + self.y ** 2) ** 0.5

u = Vector(3, 4)
print(u.norm())            # 5.0
```

### Magic Methods (Dunder Methods)

Methods starting and ending with `__` (double underscores):

```python
class Vector:
    def __init__(self, x, y):
        try:
            self.x = float(x)
            self.y = float(y)
        except ValueError:
            self.x = 0.0
            self.y = 0.0
    
    def norm(self):
        return (self.x ** 2 + self.y ** 2) ** 0.5
    
    def __add__(self, other):
        return Vector(self.x + other.x, self.y + other.y)
    
    def __str__(self):
        return "(%f, %f)" % (self.x, self.y)

u = Vector(3, 4)
v = Vector(3, 6)
print(u + v)               # (6.000000, 10.000000)
```

> [!note]
> - `__init__`: Constructor/initializer
> - `__add__`: Enables `+` operator
> - `__str__`: Controls `print()` output
> - Don't invent your own dunder methods!

### Methods and self

- **Method**: A function defined in a class
- **self**: First parameter, represents the object being operated on
- Dot notation fills in `self` automatically: `u.norm()` → `Vector.norm(u)`

## Encapsulation

Two related meanings:

### 1. Combining Data and Methods

Encapsulating data and the methods that operate on it into a single class.

### 2. Public vs Private Interface

**Convention in Python:**
- Attributes starting with `_` are **private** (by convention)
- Everything else is **public**

```python
class Diary:
    def __init__(self, title):
        self.title = title          # Public
        self._entries = []          # Private
    
    def addentry(self, entry):
        self._entries.append(entry)
    
    def _lastentry(self):           # Private method
        return self._entries[-1]

mydiary = Diary("Don't read this!!!")
mydiary.addentry("It was a good day.")
print("The diary is called", mydiary.title)

# Can access private members, but shouldn't:
# print(mydiary._entries)  # Bad practice!
```

> [!important]
> **Public Interface**: Collection of all public attributes
> - Users should only interact with public interface
> - Allows internal changes without breaking external code

### Why Respect Private Members?

Not about security - about **maintainability**:
- Can change private implementation without breaking other code
- As long as public interface unchanged, other code keeps working
- Can rename `_entries` to `_diary_entries` without issues

Related: [[04 - Testing#Testing and Object-Oriented Design]]

## Inheritance

### The "is a" Relationship

> [!important]
> **Inheritance means "is a"**

If `ClassB` extends `ClassA`, then a `ClassB` object **is a** `ClassA` object.

### Example: Polygons

Without inheritance:

```python
class Triangle:
    def __init__(self, points):
        self._sides = 3
        self._points = list(points)
        if len(self._points) != 3:
            raise ValueError("Wrong number of points.")
    
    def sides(self):
        return 3

class Square:
    def __init__(self, points):
        self._sides = 4
        self._points = list(points)
        if len(self._points) != 4:
            raise ValueError("Wrong number of points.")
    
    def sides(self):
        return 4
```

With inheritance (factoring out superclass):

```python
class Polygon:
    def __init__(self, sides, points):
        self._sides = sides
        self._points = list(points)
        if len(self._points) != self._sides:
            raise ValueError("Wrong number of points.")
    
    def sides(self):
        return self._sides

class Triangle(Polygon):
    def __init__(self, points):
        Polygon.__init__(self, 3, points)
    
    def __str__(self):
        return "I'm a triangle."

class Square(Polygon):
    def __init__(self, points):
        Polygon.__init__(self, 4, points)
    
    def __str__(self):
        return "I'm so square."
```

**Terminology:**
- **Superclass**: `Polygon` (base class)
- **Subclass**: `Triangle`, `Square` (derived classes)
- **Inheritance/Extends**: `Triangle` inherits from `Polygon`

### Method Resolution Order

When calling a method:
1. Look in the object's class
2. If not found, look in superclass
3. Continue up the inheritance chain

### Calling Superclass Methods

Superclass `__init__` is **not** automatically called:

```python
# Must explicitly call:
Polygon.__init__(self, 3, points)
```

> [!note]
> One of the few times it's okay to call a dunder method by name.

### Avoiding Duplication (DRY)

**DRY**: **D**on't **R**epeat **Y**ourself

- Duplication multiplies bugs
- Fix in one place, might forget other places
- **Factoring out a superclass**: Removing duplication by creating a common parent class

Related: [[04 - Testing#What to Test]] for testing inheritance hierarchies

## Duck Typing

> [!quote]
> "If it walks like a duck and quacks like a duck, it's a duck."

Python's **polymorphism** based on having the right methods, not inheritance:

```python
class PolygonCollection:
    def __init__(self):
        self._triangles = []
        self._squares = []
    
    def add(self, polygon):
        if polygon.sides() == 3:
            self._triangles.append(polygon)
        if polygon.sides() == 4:
            self._squares.append(polygon)
```

This works with **any** object that has a `sides()` method!

### Implications

- Not every "is a" relationship needs inheritance
- Inheritance **should** mean "is a"
- Duck typing provides flexibility without inheritance

### Example: str() Function

```python
# Any class with __str__() can be converted to string:
class Triangle:
    def __str__(self):
        return "I'm a triangle."

t = Triangle()
print(str(t))  # Calls t.__str__() which is Triangle.__str__(t)
```

Related: [[02 - Basic Python#Functions]] for more on polymorphism

## Composition

### The "has a" Relationship

> [!important]
> **Composition means "has a"**

One class stores an instance of another class.

### Example: Limited List

Wrong approach (using inheritance):
```python
# DON'T DO THIS - a limited list is NOT a list!
class MyLimitedList(list):  # Wrong!
    pass
```

Correct approach (using composition):
```python
class MyLimitedList:
    def __init__(self):
        self._L = []  # HAS A list
    
    def append(self, item):
        self._L.append(item)
    
    def __getitem__(self, index):
        return self._L[index]

L = MyLimitedList()
L.append(1)
L.append(10)
L.append(100)
print(L[2])  # 100
```

**Magic method `__getitem__`** enables square bracket notation.

### When to Use Composition

- Want to share functionality without "is a" relationship
- Need to customize behavior while using existing classes
- Want to control which methods are exposed

Related: [[07 - Deques and Linked Lists#The Wrapper Pattern]] for design pattern

## Summary

| Concept | Rule | Example |
|---------|------|---------|
| Inheritance | "is a" | Triangle is a Polygon |
| Composition | "has a" | LimitedList has a list |
| Encapsulation | Public/Private | Use `_` prefix for private |
| Duck Typing | Right methods | Any object with `sides()` |

## Related Topics

- [[02 - Basic Python]] - Python fundamentals
- [[04 - Testing]] - Testing OOP code
- [[07 - Deques and Linked Lists#The Wrapper Pattern]] - Composition pattern
- [[15 - Mappings and Hash Tables#Factoring Out A Superclass]] - Advanced inheritance example

---

*Write code close to how you think about the problem.*
