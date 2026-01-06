# Python Numbers

Python has three numeric types: `int`, `float`, and `complex`.

## Numeric Types

### Integer (int)
Whole numbers, positive or negative, without decimals:

```python
x = 1
y = 35656222554887711
z = -3255522
```

### Float
Numbers with decimal points:

```python
x = 1.10
y = 1.0
z = -35.59
```

Scientific notation:
```python
x = 35e3    # 35000.0
y = 12E4    # 120000.0
z = -87.7e100
```

### Complex
Numbers with a real and imaginary part (j):

```python
x = 3+5j
y = 5j
z = -5j
```

## Type Checking

```python
x = 1    # int
y = 2.8  # float
z = 1j   # complex

print(type(x))  # <class 'int'>
print(type(y))  # <class 'float'>
print(type(z))  # <class 'complex'>
```

## Type Conversion

See [[Python Casting]] for details:

```python
x = 1      # int
y = 2.8    # float
z = 1j     # complex

# Convert int to float
a = float(x)   # 1.0

# Convert float to int
b = int(y)     # 2

# Convert int to complex
c = complex(x) # (1+0j)

# Note: Cannot convert complex to other types
```

## Random Numbers

Python doesn't have a built-in `random()` function, but has a `random` module:

```python
import random

print(random.randrange(1, 10))  # Random number between 1 and 9
```

## Arithmetic Operations

See [[Python Operators]] for all operators:

```python
x = 10
y = 3

print(x + y)   # 13 Addition
print(x - y)   # 7  Subtraction
print(x * y)   # 30 Multiplication
print(x / y)   # 3.333... Division
print(x // y)  # 3  Floor division
print(x % y)   # 1  Modulus
print(x ** y)  # 1000 Exponentiation
```

## Math Module

See [[Python Math]] for advanced mathematical operations:

```python
import math

print(math.sqrt(64))   # 8.0
print(math.ceil(2.3))  # 3
print(math.floor(2.9)) # 2
print(math.pi)         # 3.141592653589793
```

## Number Formatting

See [[Python String Formatting]]:

```python
x = 3.14159

print(f"{x:.2f}")     # 3.14
print("{:.2f}".format(x))  # 3.14
```

---

**Related:** [[Python Data Types]] | [[Python Casting]] | [[Python Operators]] | [[Python Math]]
