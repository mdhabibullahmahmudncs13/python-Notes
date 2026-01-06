# Python Scope

Variable scope determines where variables can be accessed.

## LEGB Rule

Python follows the LEGB rule for variable lookup:
- **L**ocal: Inside current function
- **E**nclosing: In enclosing functions
- **G**lobal: At module level
- **B**uilt-in: Python built-in names

## Local Scope

```python
def my_function():
    x = 10  # Local variable
    print(x)

my_function()  # 10
# print(x)  # Error: x not defined
```

## Global Scope

```python
x = 10  # Global variable

def my_function():
    print(x)  # Can access global

my_function()  # 10
print(x)  # 10
```

## Global Keyword

```python
x = 10

def modify_global():
    global x
    x = 20

modify_global()
print(x)  # 20
```

## Enclosing Scope

```python
def outer():
    x = 10  # Enclosing scope
    
    def inner():
        print(x)  # Access enclosing variable
    
    inner()

outer()  # 10
```

## Nonlocal Keyword

```python
def outer():
    x = 10
    
    def inner():
        nonlocal x
        x = 20
    
    inner()
    print(x)  # 20

outer()
```

---

**Related:** [[Python Variables]] | [[Python Functions]] | [[Functions and Advanced Concepts]]
