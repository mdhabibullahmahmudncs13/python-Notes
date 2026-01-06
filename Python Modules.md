# Python Modules

Modules are files containing Python code that can be imported and reused.

## Creating a Module

Create a file `mymodule.py`:
```python
def greet(name):
    return f"Hello, {name}!"

PI = 3.14159
```

## Importing a Module

```python
# Import entire module
import mymodule

print(mymodule.greet("Alice"))
print(mymodule.PI)

# Import specific items
from mymodule import greet, PI

print(greet("Bob"))

# Import with alias
import mymodule as mm

# Import everything (not recommended)
from mymodule import *
```

## Built-in Modules

```python
# Math module
import math
print(math.sqrt(16))  # 4.0
print(math.pi)  # 3.141592653589793

# Random module
import random
print(random.randint(1, 10))

# Datetime module
import datetime
print(datetime.datetime.now())

# OS module
import os
print(os.getcwd())
```

## dir() Function

List all names in a module:

```python
import math
print(dir(math))
```

## The if __name__ == "__main__" Pattern

```python
# mymodule.py
def main():
    print("Running as main program")

if __name__ == "__main__":
    main()
```

This code runs only when the file is executed directly, not when imported.

---

**Related:** [[Python]] | [[Functions and Advanced Concepts]] | [[Python PIP]]
