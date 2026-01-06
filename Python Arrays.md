# Python Arrays

Arrays store multiple values of the same type. Python doesn't have built-in arrays; use the `array` module or NumPy.

## Array Module

```python
import array

# Create array
# 'i' = signed int
arr = array.array('i', [1, 2, 3, 4, 5])

# Type codes
# 'b' - signed char
# 'B' - unsigned char
# 'h' - signed short
# 'H' - unsigned short
# 'i' - signed int
# 'I' - unsigned int
# 'l' - signed long
# 'L' - unsigned long
# 'f' - float
# 'd' - double
```

## Creating Arrays

```python
import array

# Integer array
int_array = array.array('i', [1, 2, 3, 4, 5])

# Float array
float_array = array.array('f', [1.1, 2.2, 3.3])

# Empty array
empty = array.array('i')

# From list
numbers = [1, 2, 3]
arr = array.array('i', numbers)
```

## Accessing Elements

```python
arr = array.array('i', [1, 2, 3, 4, 5])

# By index
print(arr[0])   # 1
print(arr[-1])  # 5

# Slicing
print(arr[1:3])  # array('i', [2, 3])
```

## Modifying Arrays

```python
arr = array.array('i', [1, 2, 3])

# Change element
arr[1] = 10

# Append
arr.append(4)

# Insert
arr.insert(1, 99)  # Insert 99 at index 1

# Extend
arr.extend([5, 6, 7])

# Remove
arr.remove(99)  # Remove first occurrence

# Pop
arr.pop()       # Remove and return last
arr.pop(0)      # Remove and return at index
```

## Array Methods

```python
# Add
arr.append(item)
arr.insert(index, item)
arr.extend(iterable)

# Remove
arr.remove(item)
arr.pop(index)

# Search
arr.index(item)
arr.count(item)

# Reverse
arr.reverse()

# Convert
arr.tolist()     # To list
arr.tobytes()    # To bytes
```

## Looping Through Arrays

```python
arr = array.array('i', [1, 2, 3, 4, 5])

# Basic loop
for item in arr:
    print(item)

# With index
for i in range(len(arr)):
    print(f"{i}: {arr[i]}")
```

## Array Operations

```python
arr = array.array('i', [1, 2, 3])

# Length
len(arr)  # 3

# Concatenate
arr2 = array.array('i', [4, 5])
combined = arr + arr2  # Can't use extend for this

# Repeat
repeated = arr * 2  # [1, 2, 3, 1, 2, 3]
```

## NumPy Arrays (Recommended)

For numerical computing, use NumPy:

```python
import numpy as np

# Create array
arr = np.array([1, 2, 3, 4, 5])

# Multi-dimensional
matrix = np.array([[1, 2], [3, 4]])

# Array operations
arr * 2           # Multiply all elements
arr + 10          # Add to all elements
arr.mean()        # Average
arr.sum()         # Sum
arr.max()         # Maximum
```

See [[Python NumPy]] for detailed information.

## Lists vs Arrays

### Lists
- Can contain different types
- More flexible
- Slower for numerical operations

```python
my_list = [1, "hello", 3.14, True]
```

### Arrays
- Same type only
- More memory efficient
- Faster for numerical operations

```python
import array
my_array = array.array('i', [1, 2, 3, 4])
```

## When to Use Arrays

1. **Use arrays when:**
   - All elements are the same type
   - Need memory efficiency
   - Performing numerical operations

2. **Use lists when:**
   - Need mixed types
   - Need more flexibility
   - Don't need performance optimization

3. **Use NumPy when:**
   - Doing scientific computing
   - Need multi-dimensional arrays
   - Need advanced mathematical operations

## Array from List

```python
import array

# Convert list to array
numbers = [1, 2, 3, 4, 5]
arr = array.array('i', numbers)

# Convert array to list
back_to_list = arr.tolist()
```

## Common Use Cases

```python
import array

# Buffer for binary data
buffer = array.array('B')  # Unsigned bytes

# Efficient numerical storage
temperatures = array.array('f', [20.5, 21.0, 19.8])

# Image data (often bytes)
image_data = array.array('B', [255, 128, 0] * 100)
```

---

**Related:** [[Data Structures]] | [[Python Lists]] | [[Python NumPy]] | [[Python For Loops]]
