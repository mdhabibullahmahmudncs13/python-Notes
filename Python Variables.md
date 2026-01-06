# Python Variables

Variables are containers for storing data values.

## Creating Variables

Python has no command for declaring variables. A variable is created when you assign a value:

```python
x = 5
y = "Hello"
name = "John"
```

## Variable Naming Rules

### Valid Names
```python
myvar = "John"
my_var = "John"
_my_var = "John"
myVar = "John"
MYVAR = "John"
myvar2 = "John"
```

### Invalid Names
```python
2myvar = "John"    # Cannot start with number
my-var = "John"    # Cannot use hyphens
my var = "John"    # Cannot contain spaces
```

### Conventions
- Use snake_case for variables: `my_variable_name`
- Use descriptive names: `user_name` instead of `un`
- Avoid Python keywords: `class`, `for`, `if`, etc.

## Multiple Values

### Assign multiple values
```python
x, y, z = "Orange", "Banana", "Cherry"
```

### Same value to multiple variables
```python
x = y = z = "Orange"
```

### Unpacking a collection
```python
fruits = ["apple", "banana", "cherry"]
x, y, z = fruits
```

## Output Variables

### Print variables
```python
x = "Python"
print(x)

# Multiple variables
x = "Python"
y = "is"
z = "awesome"
print(x, y, z)  # Python is awesome

# Concatenation
print(x + " " + y + " " + z)  # Python is awesome
```

### For numbers
```python
x = 5
y = 10
print(x + y)  # 15
```

## Global Variables

Variables created outside functions are global:

```python
x = "awesome"

def myfunc():
    print("Python is " + x)

myfunc()  # Python is awesome
```

### The global keyword

Create or modify global variables inside functions:

```python
def myfunc():
    global x
    x = "fantastic"

myfunc()
print("Python is " + x)  # Python is fantastic
```

## Variable Types

Variables can store different [[Python Data Types]]:

```python
x = 5           # int
y = 3.14        # float
z = "Hello"     # str
is_valid = True # bool
```

## Variable Scope

See [[Python Scope]] for detailed information about local and global scope.

---

**Related:** [[Python Data Types]] | [[Python Scope]] | [[Python Casting]] | [[Python Basics]]
