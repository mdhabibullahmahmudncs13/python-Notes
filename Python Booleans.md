# Python Booleans

Booleans represent one of two values: `True` or `False`.

## Boolean Values

```python
print(10 > 9)   # True
print(10 == 9)  # False
print(10 < 9)   # False
```

## The bool() Function

Evaluate any value as Boolean:

```python
print(bool("Hello"))  # True
print(bool(15))       # True
print(bool([1,2,3]))  # True
```

### Values that are False

```python
bool(False)    # False
bool(None)     # False
bool(0)        # False
bool("")       # False
bool([])       # False
bool(())       # False
bool({})       # False
bool(set())    # False
```

### Values that are True

Almost any value is True:
- Any non-zero number
- Any non-empty string
- Any non-empty list, tuple, set, or dict

```python
bool(1)          # True
bool(-1)         # True
bool("abc")      # True
bool([0])        # True (list is not empty)
bool(0.0)        # False (zero)
```

## Boolean in Conditions

```python
x = 10
y = 5

if x > y:
    print("x is greater than y")  # This will execute

if y:  # y is non-zero, so True
    print("y is True")
```

See [[Python If Else]] for conditional statements.

## Boolean Operators

See [[Python Operators]] for logical operators:

```python
# and - Both must be True
print(True and True)    # True
print(True and False)   # False

# or - At least one must be True
print(True or False)    # True
print(False or False)   # False

# not - Inverts the value
print(not True)         # False
print(not False)        # True
```

## Comparison Operators

All comparison operators return Boolean values:

```python
x = 5
y = 10

print(x == y)   # False (equal)
print(x != y)   # True  (not equal)
print(x > y)    # False (greater than)
print(x < y)    # True  (less than)
print(x >= y)   # False (greater or equal)
print(x <= y)   # True  (less or equal)
```

## isinstance()

Check if an object is of a certain type:

```python
x = 200
print(isinstance(x, int))  # True

y = "Hello"
print(isinstance(y, str))  # True
```

## Custom Boolean Behavior

Classes can define `__bool__()` or `__len__()`:

```python
class MyClass:
    def __bool__(self):
        return False

obj = MyClass()
print(bool(obj))  # False
```

## Truthy and Falsy

Python uses "truthy" and "falsy" concepts:

```python
# Falsy values
if not []:
    print("Empty list is falsy")

# Truthy values  
if [1, 2, 3]:
    print("Non-empty list is truthy")
```

---

**Related:** [[Python Operators]] | [[Python If Else]] | [[Python Data Types]] | [[Python Basics]]
