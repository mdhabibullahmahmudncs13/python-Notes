# Python Math

Mathematical operations and functions.

## Built-in Math Functions

```python
# Min and Max
print(min(5, 10, 25))  # 5
print(max(5, 10, 25))  # 25

# Absolute value
print(abs(-7.25))  # 7.25

# Power
print(pow(4, 3))  # 64 (4^3)

# Round
print(round(3.14159, 2))  # 3.14
```

## Math Module

```python
import math

# Square root
print(math.sqrt(64))  # 8.0

# Ceiling and floor
print(math.ceil(1.4))   # 2
print(math.floor(1.4))  # 1

# Pi and E
print(math.pi)  # 3.141592653589793
print(math.e)   # 2.718281828459045

# Trigonometric functions
print(math.sin(math.pi/2))  # 1.0
print(math.cos(0))          # 1.0
print(math.tan(0))          # 0.0

# Logarithms
print(math.log(10))     # Natural log
print(math.log10(100))  # 2.0 (log base 10)

# Factorial
print(math.factorial(5))  # 120
```

## Random Numbers

```python
import random

# Random float between 0 and 1
print(random.random())

# Random integer
print(random.randint(1, 10))

# Random choice from list
items = ["apple", "banana", "cherry"]
print(random.choice(items))

# Shuffle list
random.shuffle(items)

# Random sample
print(random.sample(items, 2))
```

---

**Related:** [[Python Numbers]] | [[Python]] | [[Python NumPy]]
