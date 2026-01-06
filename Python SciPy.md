# Python SciPy

SciPy is a library for scientific and technical computing.

## Installation

```bash
pip install scipy
```

## Import SciPy

```python
import scipy
from scipy import stats, optimize, integrate
```

## Statistics

```python
from scipy import stats
import numpy as np

data = np.array([1, 2, 3, 4, 5])

# Descriptive statistics
mean = stats.describe(data).mean
variance = stats.describe(data).variance

# Distributions
# Normal distribution
print(stats.norm.pdf(0))  # Probability density function
print(stats.norm.cdf(0))  # Cumulative distribution

# Generate random samples
samples = stats.norm.rvs(size=100)

# T-test
t_statistic, p_value = stats.ttest_1samp(data, 3)
print(f"p-value: {p_value}")
```

## Optimization

```python
from scipy import optimize

# Minimize function
def f(x):
    return x**2 + 5*x + 6

result = optimize.minimize(f, x0=0)
print(result.x)  # Minimum point

# Find root
def equation(x):
    return x**2 - 4

root = optimize.root(equation, x0=1)
print(root.x)  # [2.]
```

## Integration

```python
from scipy import integrate

# Integrate function
def f(x):
    return x**2

result, error = integrate.quad(f, 0, 1)
print(result)  # 0.333...
```

## Interpolation

```python
from scipy import interpolate

x = np.array([0, 1, 2, 3, 4])
y = np.array([0, 1, 4, 9, 16])

# Linear interpolation
f = interpolate.interp1d(x, y)
print(f(2.5))  # 6.5

# Cubic interpolation
f_cubic = interpolate.interp1d(x, y, kind='cubic')
```

## Linear Algebra

```python
from scipy import linalg

A = np.array([[1, 2], [3, 4]])
b = np.array([5, 6])

# Solve linear system Ax = b
x = linalg.solve(A, b)

# Eigenvalues and eigenvectors
eigenvalues, eigenvectors = linalg.eig(A)

# Matrix operations
det = linalg.det(A)
inv = linalg.inv(A)
```

## Signal Processing

```python
from scipy import signal

# Create signal
t = np.linspace(0, 1, 500)
sig = np.sin(2 * np.pi * 5 * t)

# Filter
b, a = signal.butter(4, 0.1)
filtered = signal.filtfilt(b, a, sig)
```

---

**Related:** [[Python Libraries and Frameworks]] | [[Python NumPy]] | [[Python Math]]
