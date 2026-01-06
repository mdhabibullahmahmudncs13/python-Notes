# Python Matplotlib

Matplotlib is a library for creating visualizations and plots.

## Installation

```bash
pip install matplotlib
```

## Import

```python
import matplotlib.pyplot as plt
```

## Line Plot

```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]
y = [2, 4, 6, 8, 10]

plt.plot(x, y)
plt.xlabel('X axis')
plt.ylabel('Y axis')
plt.title('Line Plot')
plt.show()
```

## Multiple Lines

```python
x = [1, 2, 3, 4, 5]
y1 = [1, 4, 9, 16, 25]
y2 = [1, 2, 3, 4, 5]

plt.plot(x, y1, label='Squared')
plt.plot(x, y2, label='Linear')
plt.legend()
plt.show()
```

## Scatter Plot

```python
x = [1, 2, 3, 4, 5]
y = [2, 4, 5, 7, 8]

plt.scatter(x, y)
plt.xlabel('X')
plt.ylabel('Y')
plt.title('Scatter Plot')
plt.show()
```

## Bar Chart

```python
categories = ['A', 'B', 'C', 'D']
values = [10, 24, 36, 40]

plt.bar(categories, values)
plt.xlabel('Category')
plt.ylabel('Value')
plt.title('Bar Chart')
plt.show()
```

## Histogram

```python
import numpy as np

data = np.random.randn(1000)

plt.hist(data, bins=30)
plt.xlabel('Value')
plt.ylabel('Frequency')
plt.title('Histogram')
plt.show()
```

## Pie Chart

```python
sizes = [15, 30, 45, 10]
labels = ['A', 'B', 'C', 'D']

plt.pie(sizes, labels=labels, autopct='%1.1f%%')
plt.title('Pie Chart')
plt.show()
```

## Subplots

```python
fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(10, 4))

# First subplot
ax1.plot([1, 2, 3], [1, 4, 9])
ax1.set_title('Plot 1')

# Second subplot
ax2.plot([1, 2, 3], [1, 2, 3])
ax2.set_title('Plot 2')

plt.tight_layout()
plt.show()
```

## Customization

```python
x = [1, 2, 3, 4, 5]
y = [2, 4, 6, 8, 10]

plt.plot(x, y, 
         color='red',           # Line color
         linestyle='--',        # Line style
         linewidth=2,           # Line width
         marker='o',            # Marker style
         markersize=8,          # Marker size
         label='Data')

plt.grid(True)                  # Show grid
plt.legend()                    # Show legend
plt.xlim(0, 6)                  # X axis limits
plt.ylim(0, 12)                 # Y axis limits
plt.show()
```

## Save Figure

```python
plt.plot([1, 2, 3], [1, 4, 9])
plt.savefig('plot.png', dpi=300, bbox_inches='tight')
```

## 3D Plots

```python
from mpl_toolkits.mplot3d import Axes3D
import numpy as np

fig = plt.figure()
ax = fig.add_subplot(111, projection='3d')

x = np.random.randn(100)
y = np.random.randn(100)
z = np.random.randn(100)

ax.scatter(x, y, z)
ax.set_xlabel('X')
ax.set_ylabel('Y')
ax.set_zlabel('Z')
plt.show()
```

---

**Related:** [[Python Libraries and Frameworks]] | [[Python NumPy]] | [[Python Pandas]]
