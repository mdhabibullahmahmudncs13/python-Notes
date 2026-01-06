# Python User Input

Get input from users in Python programs.

## input() Function

```python
name = input("Enter your name: ")
print(f"Hello, {name}!")
```

## Input is Always String

```python
age = input("Enter your age: ")
print(type(age))  # <class 'str'>

# Convert to integer
age = int(input("Enter your age: "))
print(type(age))  # <class 'int'>
```

## Type Conversion

```python
# Integer
age = int(input("Enter age: "))

# Float
price = float(input("Enter price: "))

# Multiple values
x, y = input("Enter two numbers: ").split()
x = int(x)
y = int(y)

# List
numbers = list(map(int, input("Enter numbers: ").split()))
```

## Input Validation

```python
# Basic validation
while True:
    try:
        age = int(input("Enter age: "))
        if age < 0:
            print("Age cannot be negative")
        else:
            break
    except ValueError:
        print("Please enter a number")

# With function
def get_positive_int(prompt):
    while True:
        try:
            value = int(input(prompt))
            if value > 0:
                return value
            print("Please enter a positive number")
        except ValueError:
            print("Please enter a number")

age = get_positive_int("Enter age: ")
```

## Menu Example

```python
while True:
    print("\nMenu:")
    print("1. Option 1")
    print("2. Option 2")
    print("3. Exit")
    
    choice = input("Choose: ")
    
    if choice == "1":
        print("Option 1 selected")
    elif choice == "2":
        print("Option 2 selected")
    elif choice == "3":
        break
    else:
        print("Invalid choice")
```

## Password Input

```python
import getpass

password = getpass.getpass("Enter password: ")
# Input is hidden
```

## Reading Multiple Lines

```python
print("Enter text (press Ctrl+D or Ctrl+Z when done):")
lines = []
while True:
    try:
        line = input()
        lines.append(line)
    except EOFError:
        break

text = "\n".join(lines)
```

---

**Related:** [[Python]] | [[Python Strings]] | [[Python Try Except]]
