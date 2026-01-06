# Python NumPy

NumPy is a library for numerical computing with powerful array objects.

## Installation

```bash
pip install numpy
```

## Import NumPy

```python
import numpy as np
```

## Creating Arrays

```python
import numpy as np

# From list
arr = np.array([1, 2, 3, 4, 5])

# 2D array
arr2d = np.array([[1, 2, 3], [4, 5, 6]])

# Zeros, ones, empty
zeros = np.zeros(5)          # [0, 0, 0, 0, 0]
ones = np.ones(5)            # [1, 1, 1, 1, 1]
empty = np.empty(5)          # Uninitialized

# Range
arr = np.arange(0, 10, 2)    # [0, 2, 4, 6, 8]

# Linspace
arr = np.linspace(0, 1, 5)   # [0, 0.25, 0.5, 0.75, 1]

# Random
rand = np.random.rand(5)      # Random [0, 1)
randint = np.random.randint(0, 10, 5)  # Random integers
```

## Array Operations

```python
arr = np.array([1, 2, 3, 4, 5])

# Element-wise operations
print(arr + 10)       # [11, 12, 13, 14, 15]
print(arr * 2)        # [2, 4, 6, 8, 10]
print(arr ** 2)       # [1, 4, 9, 16, 25]

# Array operations
arr1 = np.array([1, 2, 3])
arr2 = np.array([4, 5, 6])
print(arr1 + arr2)    # [5, 7, 9]

# Aggregate functions
print(arr.sum())      # 15
print(arr.mean())     # 3.0
print(arr.max())      # 5
print(arr.min())      # 1
print(arr.std())      # Standard deviation
```

## Indexing and Slicing

```python
arr = np.array([1, 2, 3, 4, 5])

# Indexing
print(arr[0])         # 1
print(arr[-1])        # 5

# Slicing
print(arr[1:4])       # [2, 3, 4]
print(arr[:3])        # [1, 2, 3]

# 2D arrays
arr2d = np.array([[1, 2, 3], [4, 5, 6]])
print(arr2d[0, 1])    # 2
print(arr2d[:, 1])    # [2, 5] (column)
print(arr2d[1, :])    # [4, 5, 6] (row)
```

## Reshaping

```python
arr = np.array([1, 2, 3, 4, 5, 6])

# Reshape
arr2d = arr.reshape(2, 3)
# [[1, 2, 3],
#  [4, 5, 6]]

# Flatten
flat = arr2d.flatten()

# Transpose
transposed = arr2d.T
```

## Boolean Indexing

```python
arr = np.array([1, 2, 3, 4, 5])

# Boolean mask
mask = arr > 3
print(mask)           # [False, False, False, True, True]
print(arr[mask])      # [4, 5]

# Direct
print(arr[arr > 3])   # [4, 5]
```

## Common Functions

```python
# Math functions
np.sqrt(arr)
np.exp(arr)
np.log(arr)
np.sin(arr)
np.cos(arr)

# Statistical
np.mean(arr)
np.median(arr)
np.std(arr)
np.var(arr)
np.percentile(arr, 50)

# Linear algebra
a = np.array([[1, 2], [3, 4]])
b = np.array([[5, 6], [7, 8]])

np.dot(a, b)          # Matrix multiplication
np.linalg.det(a)      # Determinant
np.linalg.inv(a)      # Inverse
```

---

**Related:** [[Python Libraries and Frameworks]] | [[Python Pandas]] | [[Python Arrays]]
