# Python Break Continue

Control statements that modify loop behavior by exiting loops early or skipping iterations.

## Break Statement

The `break` statement exits the loop immediately, skipping any remaining iterations.

### Break in For Loop

```python
# Exit when condition is met
fruits = ["apple", "banana", "cherry", "date", "elderberry"]
for fruit in fruits:
    if fruit == "cherry":
        break
    print(fruit)

# Output:
# apple
# banana
```

```python
# Find first occurrence
numbers = [1, 3, 5, 7, 8, 9, 11]
for num in numbers:
    if num % 2 == 0:
        print(f"First even number: {num}")
        break
# Output: First even number: 8
```

### Break in While Loop

```python
# Exit when condition is met
i = 1
while i <= 10:
    print(i)
    if i == 5:
        break
    i += 1

# Output: 1 2 3 4 5
```

```python
# User input validation
while True:
    password = input("Enter password (min 6 chars): ")
    if len(password) >= 6:
        print("Password accepted!")
        break
    print("Too short, try again.")
```

### Break in Nested Loops

⚠️ `break` only exits the innermost loop:

```python
for i in range(1, 4):
    for j in range(1, 4):
        if j == 2:
            break  # Only breaks inner loop
        print(f"({i}, {j})", end=" ")
    print()

# Output:
# (1, 1) 
# (2, 1) 
# (3, 1)
```

To break out of multiple loops, use a flag:

```python
found = False
for i in range(1, 4):
    for j in range(1, 4):
        if i == 2 and j == 2:
            found = True
            break
    if found:
        break
    print(f"i = {i}")

# Output:
# i = 1
```

Or use a function with `return`:

```python
def search_matrix():
    for i in range(1, 4):
        for j in range(1, 4):
            if i == 2 and j == 2:
                return f"Found at ({i}, {j})"
    return "Not found"

print(search_matrix())  # Found at (2, 2)
```

## Continue Statement

The `continue` statement skips the rest of the current iteration and moves to the next one.

### Continue in For Loop

```python
# Skip specific items
fruits = ["apple", "banana", "cherry", "date"]
for fruit in fruits:
    if fruit == "banana":
        continue
    print(fruit)

# Output:
# apple
# cherry
# date
```

```python
# Process only even numbers
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
for num in numbers:
    if num % 2 != 0:
        continue
    print(f"{num} is even")

# Output:
# 2 is even
# 4 is even
# 6 is even
# 8 is even
# 10 is even
```

### Continue in While Loop

```python
# Skip specific values
i = 0
while i < 6:
    i += 1
    if i == 3:
        continue
    print(i)

# Output: 1 2 4 5 6 (skips 3)
```

⚠️ **Important:** Update the counter BEFORE the continue:

```python
# ❌ WRONG - Infinite loop!
# i = 0
# while i < 6:
#     if i == 3:
#         continue
#     print(i)
#     i += 1  # Never reaches when i=3

# ✅ CORRECT
i = 0
while i < 6:
    i += 1  # Increment first
    if i == 3:
        continue
    print(i)
```

### Continue in Nested Loops

```python
for i in range(1, 4):
    for j in range(1, 4):
        if j == 2:
            continue  # Skip j=2 in inner loop
        print(f"({i}, {j})", end=" ")
    print()

# Output:
# (1, 1) (1, 3) 
# (2, 1) (2, 3) 
# (3, 1) (3, 3)
```

## Break vs Continue vs Pass

| Statement | Effect |
|-----------|--------|
| `break` | Exits the loop completely |
| `continue` | Skips to the next iteration |
| `pass` | Does nothing (placeholder) |

```python
# break - exits loop
for i in range(5):
    if i == 3:
        break
    print(i)
# Output: 0 1 2

# continue - skips iteration
for i in range(5):
    if i == 3:
        continue
    print(i)
# Output: 0 1 2 4

# pass - does nothing
for i in range(5):
    if i == 3:
        pass  # Placeholder, does nothing
    print(i)
# Output: 0 1 2 3 4
```

## Effect on Else Clause

The `else` clause in loops runs only if the loop completes normally (NOT broken):

### With Break (else doesn't run)

```python
for i in range(5):
    if i == 3:
        break
    print(i)
else:
    print("Loop completed")

# Output:
# 0
# 1
# 2
```

### With Continue (else runs)

```python
for i in range(5):
    if i == 3:
        continue
    print(i)
else:
    print("Loop completed")

# Output:
# 0
# 1
# 2
# 4
# Loop completed
```

## Practical Examples

### Search and Exit

```python
# Find item in list
items = ["apple", "banana", "cherry", "date"]
search = "cherry"

for item in items:
    if item == search:
        print(f"Found {search}!")
        break
else:
    print(f"{search} not found")

# Output: Found cherry!
```

### Skip Invalid Data

```python
# Process only valid numbers
data = [10, 20, "invalid", 30, None, 40]

for item in data:
    if not isinstance(item, (int, float)):
        continue
    print(f"Processing: {item}")

# Output:
# Processing: 10
# Processing: 20
# Processing: 30
# Processing: 40
```

### User Menu

```python
while True:
    print("\n1. Option A")
    print("2. Option B")
    print("3. Exit")
    
    choice = input("Choose: ")
    
    if choice == "1":
        print("You chose A")
    elif choice == "2":
        print("You chose B")
    elif choice == "3":
        print("Goodbye!")
        break
    else:
        print("Invalid choice")
        continue
```

### Validation Loop

```python
# Skip invalid entries, break on sentinel
numbers = []
while True:
    user_input = input("Enter number (or 'done'): ")
    
    if user_input.lower() == 'done':
        break
    
    try:
        num = float(user_input)
        numbers.append(num)
    except ValueError:
        print("Invalid number, try again")
        continue

print(f"You entered: {numbers}")
```

### Filter and Process

```python
# Process files, skip certain extensions
files = ["doc.txt", "image.png", "data.csv", "script.py", "backup.tmp"]

for file in files:
    # Skip temporary files
    if file.endswith('.tmp'):
        continue
    
    # Stop at Python files
    if file.endswith('.py'):
        print(f"Found Python file: {file}")
        break
    
    print(f"Processing: {file}")

# Output:
# Processing: doc.txt
# Processing: image.png
# Processing: data.csv
# Found Python file: script.py
```

## Common Patterns

### Early Exit Pattern

```python
# Exit as soon as condition is met
def has_duplicates(items):
    seen = set()
    for item in items:
        if item in seen:
            return True  # or use break
        seen.add(item)
    return False
```

### Skip and Continue Pattern

```python
# Process only valid items
def process_numbers(numbers):
    results = []
    for num in numbers:
        if num < 0:
            continue  # Skip negative
        if num > 100:
            continue  # Skip too large
        results.append(num * 2)
    return results
```

### Sentinel-Controlled Loop

```python
# Read until sentinel value
data = []
while True:
    value = input("Enter value (or 'quit'): ")
    if value == 'quit':
        break
    data.append(value)
```

## Best Practices

✅ **Do:**
- Use `break` to exit early when a condition is met
- Use `continue` to skip invalid/unwanted items
- Use descriptive conditions with break/continue
- Consider extracting complex break logic into functions

❌ **Don't:**
- Overuse break/continue (can make code hard to follow)
- Forget to update loop variables before `continue` in while loops
- Use break for flow control when a function return would be clearer
- Create deeply nested loops with multiple break statements

---

**Related:** [[Control Flow]] | [[Python For Loops]] | [[Python While Loops]] | [[Python If Else]]
