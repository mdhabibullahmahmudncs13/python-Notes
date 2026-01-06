# Python Functions

Functions are reusable blocks of code that perform specific tasks.

## Defining Functions

```python
def greet():
    print("Hello!")

# Call the function
greet()
```

## Functions with Parameters

```python
def greet(name):
    print(f"Hello, {name}!")

greet("Alice")  # Hello, Alice!
```

## Multiple Parameters

```python
def add(a, b):
    return a + b

result = add(5, 3)  # 8
```

## Return Values

```python
def multiply(a, b):
    return a * b

result = multiply(4, 5)  # 20

# Multiple return values
def get_name():
    return "John", "Doe"

first, last = get_name()
```

## Default Parameters

```python
def greet(name="Guest"):
    print(f"Hello, {name}!")

greet()          # Hello, Guest!
greet("Alice")   # Hello, Alice!
```

## Keyword Arguments

```python
def describe_pet(animal, name):
    print(f"I have a {animal} named {name}")

# Positional arguments
describe_pet("dog", "Max")

# Keyword arguments
describe_pet(name="Max", animal="dog")
describe_pet(animal="cat", name="Whiskers")
```

## *args (Variable Positional Arguments)

```python
def sum_all(*args):
    return sum(args)

print(sum_all(1, 2, 3))        # 6
print(sum_all(1, 2, 3, 4, 5))  # 15

# args is a tuple
def print_args(*args):
    for arg in args:
        print(arg)

print_args("a", "b", "c")
```

## **kwargs (Variable Keyword Arguments)

```python
def print_info(**kwargs):
    for key, value in kwargs.items():
        print(f"{key}: {value}")

print_info(name="John", age=30, city="New York")

# kwargs is a dictionary
def build_profile(**kwargs):
    return kwargs

profile = build_profile(name="John", age=30)
# {'name': 'John', 'age': 30}
```

## Combining *args and **kwargs

```python
def make_pizza(size, *toppings, **details):
    print(f"\nMaking a {size}-inch pizza")
    print("Toppings:")
    for topping in toppings:
        print(f"  - {topping}")
    print("Details:")
    for key, value in details.items():
        print(f"  {key}: {value}")

make_pizza(12, "pepperoni", "mushrooms", 
           crust="thick", sauce="tomato")
```

## Order of Parameters

```python
# Correct order:
# 1. Regular parameters
# 2. *args
# 3. Default parameters
# 4. **kwargs

def function(a, b, *args, c=10, **kwargs):
    pass
```

## Docstrings

Document your functions:

```python
def calculate_area(length, width):
    """
    Calculate the area of a rectangle.
    
    Args:
        length (float): The length of the rectangle
        width (float): The width of the rectangle
    
    Returns:
        float: The area of the rectangle
    """
    return length * width

# Access docstring
print(calculate_area.__doc__)
```

## Lambda Functions

See [[Python Lambda]] for anonymous functions:

```python
# Regular function
def square(x):
    return x ** 2

# Lambda equivalent
square = lambda x: x ** 2
```

## Nested Functions

```python
def outer():
    def inner():
        print("Inside inner function")
    
    print("Inside outer function")
    inner()

outer()
```

## Functions as Arguments

```python
def apply_operation(func, x, y):
    return func(x, y)

def add(a, b):
    return a + b

result = apply_operation(add, 5, 3)  # 8
```

## Returning Functions

```python
def create_multiplier(n):
    def multiplier(x):
        return x * n
    return multiplier

times_3 = create_multiplier(3)
print(times_3(10))  # 30
```

## Recursion

See [[Python Recursion]] for recursive functions.

## Type Hints (Python 3.5+)

```python
def add(a: int, b: int) -> int:
    return a + b

def greet(name: str) -> None:
    print(f"Hello, {name}!")

# Complex types
from typing import List, Dict, Optional

def process_list(items: List[int]) -> Dict[str, int]:
    return {"count": len(items), "sum": sum(items)}
```

## Practical Examples

```python
# Fibonacci
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n-1) + fibonacci(n-2)

# Factorial
def factorial(n):
    if n == 0:
        return 1
    return n * factorial(n-1)

# Is prime
def is_prime(n):
    if n < 2:
        return False
    for i in range(2, int(n**0.5) + 1):
        if n % i == 0:
            return False
    return True

# Find maximum
def find_max(numbers):
    if not numbers:
        return None
    max_num = numbers[0]
    for num in numbers:
        if num > max_num:
            max_num = num
    return max_num

# Count vowels
def count_vowels(text):
    vowels = "aeiou"
    count = 0
    for char in text.lower():
        if char in vowels:
            count += 1
    return count
```

## Pass by Reference vs Value

Python passes by object reference:

```python
# Immutable objects (int, str, tuple)
def modify_number(x):
    x += 10
    print(f"Inside: {x}")

num = 5
modify_number(num)  # Inside: 15
print(f"Outside: {num}")  # Outside: 5

# Mutable objects (list, dict)
def modify_list(lst):
    lst.append(4)
    print(f"Inside: {lst}")

my_list = [1, 2, 3]
modify_list(my_list)  # Inside: [1, 2, 3, 4]
print(f"Outside: {my_list}")  # Outside: [1, 2, 3, 4]
```

## Function Annotations

```python
def greet(name: str, age: int = 0) -> str:
    return f"Hello {name}, you are {age} years old"

# Access annotations
print(greet.__annotations__)
# {'name': <class 'str'>, 'age': <class 'int'>, 'return': <class 'str'>}
```

---

**Related:** [[Functions and Advanced Concepts]] | [[Python Lambda]] | [[Python Decorators]] | [[Python Scope]]
