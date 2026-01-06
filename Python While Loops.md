# Python While Loops

While loops execute code repeatedly as long as a condition is true.

## Basic While Loop

```python
i = 1
while i < 6:
    print(i)
    i += 1

# Output: 1 2 3 4 5
```

⚠️ **Remember to increment** to avoid infinite loops!

## Infinite Loop

```python
# Don't do this (unless intentional)
while True:
    print("This will run forever!")
    # Use Ctrl+C to stop
```

## Break Statement

Exit the loop early:

```python
i = 1
while i < 6:
    print(i)
    if i == 3:
        break
    i += 1

# Output: 1 2 3
```

## Continue Statement

Skip to the next iteration:

```python
i = 0
while i < 6:
    i += 1
    if i == 3:
        continue
    print(i)

# Output: 1 2 4 5 6 (skips 3)
```

## While with Else

The `else` block runs when the loop completes normally (not broken):

```python
i = 1
while i < 6:
    print(i)
    i += 1
else:
    print("Loop finished")

# Output: 1 2 3 4 5 Loop finished
```

```python
# With break (else doesn't run)
i = 1
while i < 6:
    print(i)
    if i == 3:
        break
    i += 1
else:
    print("Loop finished")  # Won't print

# Output: 1 2 3
```

## Nested While Loops

```python
i = 1
while i <= 3:
    j = 1
    while j <= 3:
        print(f"({i}, {j})", end=" ")
        j += 1
    print()  # New line
    i += 1

# Output:
# (1, 1) (1, 2) (1, 3)
# (2, 1) (2, 2) (2, 3)
# (3, 1) (3, 2) (3, 3)
```

## Common Patterns

### Menu Loop
```python
while True:
    print("\n1. Option 1")
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

### Input Validation
```python
password = ""
while len(password) < 8:
    password = input("Enter password (min 8 chars): ")
    if len(password) < 8:
        print("Too short!")

print("Password accepted")
```

### Count Down
```python
count = 5
while count > 0:
    print(count)
    count -= 1
print("Blast off!")
```

### Accumulator Pattern
```python
total = 0
i = 1
while i <= 10:
    total += i
    i += 1
print(f"Sum: {total}")  # 55
```

## While with User Input

```python
# Read until specific input
user_input = ""
while user_input != "quit":
    user_input = input("Enter command (or 'quit'): ")
    print(f"You entered: {user_input}")
```

```python
# Walrus operator (Python 3.8+)
while (user_input := input("Enter: ")) != "quit":
    print(f"You entered: {user_input}")
```

## While with Lists

```python
# Process list items
items = [1, 2, 3, 4, 5]
while items:
    item = items.pop()
    print(f"Processing: {item}")
```

```python
# Wait for condition
numbers = []
while len(numbers) < 5:
    num = int(input("Enter number: "))
    numbers.append(num)

print(f"Numbers: {numbers}")
```

## While with Multiple Conditions

```python
count = 0
total = 0

while count < 10 and total < 100:
    total += count
    count += 1

print(f"Count: {count}, Total: {total}")
```

## While True with Break

Common pattern for event loops:

```python
while True:
    command = input("Enter command: ")
    
    if command == "quit":
        break
    elif command == "help":
        print("Available commands: help, quit")
    else:
        print(f"Unknown command: {command}")
```

## Practical Examples

```python
# Guess the number game
import random

secret = random.randint(1, 100)
attempts = 0

while True:
    guess = int(input("Guess the number (1-100): "))
    attempts += 1
    
    if guess < secret:
        print("Too low!")
    elif guess > secret:
        print("Too high!")
    else:
        print(f"Correct! You got it in {attempts} attempts")
        break

# Calculate factorial
n = 5
factorial = 1
i = 1

while i <= n:
    factorial *= i
    i += 1

print(f"{n}! = {factorial}")

# Process file line by line
file = open("data.txt")
line = file.readline()
while line:
    print(line.strip())
    line = file.readline()
file.close()

# Or use for loop (better for files)
with open("data.txt") as file:
    for line in file:
        print(line.strip())
```

## While vs For

### Use While When:
- You don't know how many iterations needed
- Waiting for a condition
- Processing until user input
- Event loops

```python
while user_wants_to_continue():
    do_something()
```

### Use For When:
- Iterating over a sequence
- Known number of iterations
- Processing collections

```python
for item in items:
    process(item)
```

## Common Mistakes

```python
# Infinite loop - forgot to increment
i = 0
# while i < 5:  # Don't do this
#     print(i)
# Fix: Add i += 1

# Wrong condition
i = 0
# while i != 5:  # Problem if i skips 5
#     i += 2
# Fix: Use i < 5

# Modifying loop variable incorrectly
i = 0
while i < 5:
    print(i)
    i += 1
    i = 0  # Resets to 0 - infinite loop!
```

---

**Related:** [[Control Flow]] | [[Python For Loops]] | [[Python If Else]] | [[Python Break Continue]]
