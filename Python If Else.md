# Python If Else

Conditional statements execute code based on whether conditions are true or false.

## Basic If Statement

```python
x = 10

if x > 5:
    print("x is greater than 5")
```

## If...Else

```python
x = 3

if x > 5:
    print("x is greater than 5")
else:
    print("x is not greater than 5")
```

## If...Elif...Else

```python
x = 10

if x > 15:
    print("x is greater than 15")
elif x > 5:
    print("x is greater than 5 but not greater than 15")
else:
    print("x is 5 or less")
```

## Multiple Conditions

### Using `and`
Both conditions must be true:

```python
x = 10
y = 5

if x > 5 and y > 2:
    print("Both conditions are True")
```

### Using `or`
At least one condition must be true:

```python
x = 10
y = 1

if x > 5 or y > 2:
    print("At least one condition is True")
```

### Using `not`
Inverts the condition:

```python
x = 10

if not x > 15:
    print("x is NOT greater than 15")
```

## Nested If Statements

```python
x = 41

if x > 10:
    print("x is above 10")
    if x > 20:
        print("and also above 20")
    else:
        print("but not above 20")
```

## Shorthand If (Ternary Operator)

```python
# One line if
x = 10
if x > 5: print("x is greater than 5")

# If...Else in one line
x = 3
print("Greater") if x > 5 else print("Not greater")

# Ternary operator (more common)
result = "Greater" if x > 5 else "Not greater"

# Multiple conditions
age = 25
status = "child" if age < 13 else "teen" if age < 20 else "adult"
```

## Comparison Operators in If

```python
x = 5
y = 10

if x == y:   # Equal
    print("Equal")
    
if x != y:   # Not equal
    print("Not equal")
    
if x < y:    # Less than
    print("Less than")
    
if x <= y:   # Less than or equal
    print("Less than or equal")
    
if x > y:    # Greater than
    print("Greater than")
    
if x >= y:   # Greater than or equal
    print("Greater than or equal")
```

See [[Python Operators]] for more operators.

## Logical Operators

```python
x = 5

# and - Both must be True
if x > 3 and x < 10:
    print("x is between 3 and 10")

# or - At least one must be True
if x < 3 or x > 10:
    print("x is less than 3 or greater than 10")

# not - Inverts
if not(x > 10):
    print("x is not greater than 10")
```

## Identity Operators

```python
x = ["apple", "banana"]
y = ["apple", "banana"]
z = x

if x is z:
    print("x and z are the same object")

if x is not y:
    print("x and y are not the same object")
    
if x == y:
    print("x and y have the same content")
```

## Membership Operators

```python
fruits = ["apple", "banana", "cherry"]

if "apple" in fruits:
    print("Apple is in the list")

if "orange" not in fruits:
    print("Orange is not in the list")
```

## Truthiness

Python evaluates objects as True or False:

### Falsy Values
```python
# These are all False
if not False:       print("False is falsy")
if not None:        print("None is falsy")
if not 0:           print("0 is falsy")
if not 0.0:         print("0.0 is falsy")
if not "":          print("Empty string is falsy")
if not []:          print("Empty list is falsy")
if not {}:          print("Empty dict is falsy")
if not ():          print("Empty tuple is falsy")
if not set():       print("Empty set is falsy")
```

### Truthy Values
```python
# Everything else is True
if 1:               print("Non-zero numbers are truthy")
if "hello":         print("Non-empty strings are truthy")
if [1, 2]:          print("Non-empty lists are truthy")
if {"a": 1}:        print("Non-empty dicts are truthy")
```

## Pass Statement

Placeholder for future code:

```python
x = 10

if x > 5:
    pass  # TODO: implement later

# Useful in loops and functions too
def my_function():
    pass
```

## Practical Examples

```python
# Check user age
age = 18
if age >= 18:
    print("You can vote")
else:
    print("You cannot vote yet")

# Grade calculator
score = 85
if score >= 90:
    grade = "A"
elif score >= 80:
    grade = "B"
elif score >= 70:
    grade = "C"
elif score >= 60:
    grade = "D"
else:
    grade = "F"

# Multiple conditions
temperature = 25
weather = "sunny"

if temperature > 20 and weather == "sunny":
    print("Perfect day for the beach!")

# Check if number is in range
number = 15
if 10 <= number <= 20:
    print("Number is between 10 and 20")

# Validate input
username = input("Enter username: ")
if not username:
    print("Username cannot be empty")
elif len(username) < 3:
    print("Username must be at least 3 characters")
else:
    print(f"Welcome, {username}!")
```

## Common Patterns

```python
# Check for None
value = None
if value is None:
    print("Value is None")

# Check for empty
items = []
if not items:
    print("List is empty")

# Default value
name = input("Name: ") or "Guest"

# Guard clauses
def process_data(data):
    if not data:
        return
    if len(data) < 10:
        return
    # Process data
    print("Processing...")
```

---

**Related:** [[Control Flow]] | [[Python Booleans]] | [[Python Operators]] | [[Python While Loops]]
