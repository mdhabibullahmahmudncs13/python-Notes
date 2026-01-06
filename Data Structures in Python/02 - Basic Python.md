# Basic Python

← [[01 - Overview]] | [[Data Structures in Python]] | Next: [[03 - Object-Oriented Programming]] →

## Prerequisites

This book assumes:
- Some programming experience
- Familiarity with basic programming concepts
- Mental model of **Sequence, Selection, and Iteration**

## Core Programming Model

### Sequence, Selection, and Iteration

A fundamental way to think about imperative programming:

1. **Sequence**: Executing operations in order (default behavior)
2. **Selection**: Making decisions using conditionals (if/else)
3. **Iteration**: Repeating operations using loops or [[09 - Recursion|recursion]]

> [!note]
> Sequencing is the default - you need special constructions to do selection or iteration.

## Expressions and Evaluation

**Expressions** produce values when evaluated:

```python
2 + 2                    # Arithmetic expression → 4
5 > 7                    # Boolean expression → False
5 * (3 + abs(-12) / 3)  # Complex expression
```

### Operator Precedence
Order of operations (also called **operator precedence**) determines evaluation order.

In the complex expression above: `abs` → `/` → `+` → `*`

Related: [[05 - Running Time Analysis#Atomic Operations]]

## Variables, Types, and State

### State
Information stored for later use (like writing things down on paper during math problems).

### Assignment

```python
variable_name = some_value
```

- Right side evaluated **first**
- Then assignment happens
- Creates new variable or overwrites existing one

```python
x = x + 1    # Makes sense: x + 1 evaluated before assignment
x += 1       # Shorthand (also: -=, *=, /=)
```

> [!warning]
> Assignment is **not** an expression - it doesn't have a value.
> This prevents bugs from confusing `=` (assignment) with `==` (equality).

### Multiple Assignment
```python
x = y = 1    # Both set to 1
```

### Object Model

Every object has three properties:
1. **Identity** - Cannot change (use `is` to compare)
2. **Type** - Cannot change (check with `type()`)
3. **Value** - May or may not be changeable

```python
x = 5
y = 3.2
z = True

print(type(x))  # <class 'int'>
print(type(y))  # <class 'float'>
print(type(z))  # <class 'bool'>
```

### Identity vs Equality

```python
x = [1, 2, 3]
y = [1, 2, 3]
z = x

print(x is y)   # False (different objects)
print(x is z)   # True (same object)
print(x == z)   # True (equal values)
```

### Mutability

- **Mutable**: Value can be changed
- **Immutable**: Value cannot be changed

Examples:
- Immutable: `int`, `float`, `bool`, `str`, `tuple`
- Mutable: `list`, `dict`, `set`

## Collections

See also: [[15 - Mappings and Hash Tables]] for advanced dictionary/set operations

### Strings (str)

Sequences of characters (immutable):

```python
s = "Hello, "
t = "World."
u = s + t           # Concatenation
print(u[9])         # Indexing: 'r'
n = str(9876)
print(n[2])         # '7'
```

### Lists (list)

Ordered sequences of objects (mutable):

```python
L = [1, 2, 3, 4, 5, 6]
L.append(100)
print(L[0])         # First item: 1
print(L[-1])        # Last item: 100
print(L[-2])        # Second to last: 6

L[2] = 'skip'       # Overwriting
```

> [!important]
> Indices start at 0. Negative indices count from the end.

Related: [[06 - Stacks and Queues#List Operations]], [[05 - Running Time Analysis#List Operations]]

### Tuples (tuple)

Ordered sequences (immutable):

```python
t = (1, 2, "skip a few", 99, 100)
print(t[4])         # 100

# These will raise errors:
# t.append(101)               # No append method
# t[4] = 99.5                 # Can't assign
```

### Dictionaries (dict)

Store key-value pairs (also called **maps**, **mappings**, or **hash tables**):

```python
d = dict()
d[5] = 'five'
d[2] = 'two'
d['pi'] = 3.1415926

print(d['pi'])      # 3.1415926
```

**Key requirements:**
- Keys must be **immutable** (int, float, str, tuple)
- No fixed order (nonsequential collection)
- Accessing missing key raises `KeyError`

Related: [[15 - Mappings and Hash Tables]] for implementation details

### Sets (set)

Collections without duplicates (like mathematical sets):

```python
s = {2, 1}
s.add(3)
s.add(2)  # No effect (already exists)
print(s)  # {1, 2, 3}
```

> [!warning]
> `{}` creates an empty **dictionary**, not a set!
> Use `set()` for empty sets.

## Common Collection Operations

### Length

```python
len(a)  # Works on all collections
```

### Slicing (Lists, Tuples, Strings)

```python
a = "a string"
b = ["my", "second", "favorite", "list"]

print(a[3:7])       # "trin"
print(a[1:-2])      # "stri"
print(b[1:])        # ['second', 'favorite', 'list']
```

> [!warning]
> Slicing creates a **new object** - big slices do lots of copying!
> This can create inefficient code. See [[05 - Running Time Analysis]]

## Iteration

### For Loops

The pythonic way to iterate:

```python
mylist = [1, 3, 5]
for item in mylist:
    print(item)

mydict = {'a': 96, 'b': 97, 'c': 98}
for key in mydict:
    print(key)

for key, value in mydict.items():
    print(key, value)

for value in mydict.values():
    print(value)
```

### Range

```python
for i in range(10):
    j = 10 * i + 1
    print(j, end=' ')
# Output: 1 11 21 31 41 51 61 71 81 91
```

## Control Flow

See also: [[09 - Recursion]] for recursive control flow

### If Statements

```python
if 3 + 3 < 7:
    print("This should be printed.")

if condition:
    # do something
else:
    # do something else
```

### While Loops

```python
x = 1
while x < 128:
    print(x, end=' ')
    x = x * 2
# Output: 1 2 4 8 16 32 64
```

### Try Blocks

Catch and handle errors:

```python
x = "not a number"
try:
    f = float(x)
except ValueError:
    print("You can't do that!")
```

### Functions

```python
def foo(x, y):
    return 8 * x + y

print(foo(2, 1))           # 17
print(foo("Na", " batman")) # "NaNaNaNaNaNaNaNa batman"
```

> [!note]
> **No type requirements** - same function works with different types (duck typing)
> See [[03 - Object-Oriented Programming#Duck Typing]]

**Functions are objects:**

```python
def bar(somefunction):
    return somefunction(4)

somevariable = foo
print(bar(somevariable))   # 6
```

## Modules and Imports

A **module** is a single `.py` file.

```python
# File: twofunctions.py
def f(x):
    return 2 * x + 3

def g(x):
    return x ** 2 - 1
```

```python
# File: theimporter.py
import twofunctions

def f(x):
    return x - 1

print(twofunctions.f(1))  # 5 (from module)
print(f(1))                # 0 (local function)
print(twofunctions.g(4))   # 15
```

### The `__name__` Attribute

```python
def somefunction():
    print("Real important stuff here.")

if __name__ == '__main__':
    somefunction()  # Only runs when executed directly, not imported
```

> [!tip]
> Use this pattern to allow a module to be both imported and run as a script.

### Import Variations

```python
import module_name
from module_name import function_name
from module_name import *  # Import everything (use sparingly)
import module_name as alias
```

> [!note]
> Modules are only executed the **first time** they are imported.

## Related Topics

- [[03 - Object-Oriented Programming]] - Classes and objects
- [[04 - Testing]] - Testing Python code
- [[05 - Running Time Analysis]] - Performance of Python operations
- [[15 - Mappings and Hash Tables]] - How dicts work internally

---

*Move from thinking about code to writing code, and back again.*
