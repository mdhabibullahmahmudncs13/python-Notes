# Python File Handling

Python can read, write, and manipulate files.

## Opening Files

```python
# Open file
file = open("filename.txt", "r")

# Always close
file.close()
```

## File Modes

- `"r"` - Read (default)
- `"w"` - Write (overwrites)
- `"a"` - Append
- `"x"` - Create (fails if exists)
- `"b"` - Binary mode
- `"t"` - Text mode (default)
- `"+"` - Read and write

## Reading Files

```python
# Read entire file
with open("file.txt", "r") as file:
    content = file.read()
    print(content)

# Read line by line
with open("file.txt", "r") as file:
    for line in file:
        print(line.strip())

# Read specific number of characters
with open("file.txt", "r") as file:
    content = file.read(10)  # First 10 characters

# Read one line
with open("file.txt", "r") as file:
    line = file.readline()

# Read all lines into list
with open("file.txt", "r") as file:
    lines = file.readlines()
```

## Writing Files

```python
# Write (overwrites)
with open("file.txt", "w") as file:
    file.write("Hello World\n")
    file.write("Second line")

# Append
with open("file.txt", "a") as file:
    file.write("\nNew line")

# Write list of lines
lines = ["Line 1\n", "Line 2\n", "Line 3\n"]
with open("file.txt", "w") as file:
    file.writelines(lines)
```

## With Statement

Automatically closes files:

```python
# Manual close (old way)
file = open("file.txt", "r")
content = file.read()
file.close()

# With statement (recommended)
with open("file.txt", "r") as file:
    content = file.read()
# File automatically closed
```

## File Existence

```python
import os

if os.path.exists("file.txt"):
    os.remove("file.txt")
else:
    print("File does not exist")
```

## Delete Files

```python
import os

# Delete file
os.remove("file.txt")

# Delete folder
os.rmdir("foldername")
```

## File Paths

```python
import os

# Current directory
print(os.getcwd())

# Join paths
path = os.path.join("folder", "file.txt")

# Check if file
os.path.isfile("file.txt")

# Check if directory
os.path.isdir("folder")

# List files
files = os.listdir(".")
```

## Binary Files

```python
# Read binary
with open("image.jpg", "rb") as file:
    data = file.read()

# Write binary
with open("copy.jpg", "wb") as file:
    file.write(data)
```

## File Position

```python
with open("file.txt", "r") as file:
    print(file.tell())  # Current position
    file.seek(0)        # Go to beginning
    file.seek(10)       # Go to position 10
```

## Practical Examples

```python
# Copy file
with open("source.txt", "r") as source:
    with open("dest.txt", "w") as dest:
        dest.write(source.read())

# Count lines
with open("file.txt", "r") as file:
    lines = file.readlines()
    print(f"Lines: {len(lines)}")

# Find and replace
with open("file.txt", "r") as file:
    content = file.read()

content = content.replace("old", "new")

with open("file.txt", "w") as file:
    file.write(content)
```

---

**Related:** [[File and Database Handling]] | [[Python Try Except]] | [[Python JSON]]
