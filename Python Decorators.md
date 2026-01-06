# Python Decorators

Decorators modify the behavior of functions or classes.

## Basic Decorator

```python
def my_decorator(func):
    def wrapper():
        print("Before function")
        func()
        print("After function")
    return wrapper

@my_decorator
def say_hello():
    print("Hello!")

say_hello()
# Before function
# Hello!
# After function
```

## Decorator with Arguments

```python
def repeat(times):
    def decorator(func):
        def wrapper(*args, **kwargs):
            for _ in range(times):
                func(*args, **kwargs)
        return wrapper
    return decorator

@repeat(3)
def greet(name):
    print(f"Hello {name}!")

greet("Alice")
# Hello Alice!
# Hello Alice!
# Hello Alice!
```

## Common Decorators

```python
from functools import wraps

# Preserve function metadata
def my_decorator(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        return func(*args, **kwargs)
    return wrapper

# @property - getter/setter
class Person:
    def __init__(self, name):
        self._name = name
    
    @property
    def name(self):
        return self._name
    
    @name.setter
    def name(self, value):
        self._name = value

# @staticmethod, @classmethod
class MyClass:
    @staticmethod
    def static_method():
        pass
    
    @classmethod
    def class_method(cls):
        pass
```

---

**Related:** [[Python Functions]] | [[Python Classes and Objects]] | [[Functions and Advanced Concepts]]
