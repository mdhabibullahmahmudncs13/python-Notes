# Python Iterators

Iterators are objects that can be iterated upon.

## Iterator Protocol

Objects must implement `__iter__()` and `__next__()`:

```python
class Counter:
    def __init__(self, max):
        self.max = max
        self.current = 0
    
    def __iter__(self):
        return self
    
    def __next__(self):
        if self.current < self.max:
            self.current += 1
            return self.current
        raise StopIteration

counter = Counter(5)
for num in counter:
    print(num)  # 1 2 3 4 5
```

## iter() and next()

```python
numbers = [1, 2, 3]
iterator = iter(numbers)

print(next(iterator))  # 1
print(next(iterator))  # 2
print(next(iterator))  # 3
# next(iterator)  # StopIteration
```

## Custom Iterator

```python
class Fibonacci:
    def __init__(self, max):
        self.max = max
        self.a, self.b = 0, 1
        self.count = 0
    
    def __iter__(self):
        return self
    
    def __next__(self):
        if self.count < self.max:
            self.count += 1
            result = self.a
            self.a, self.b = self.b, self.a + self.b
            return result
        raise StopIteration

for fib in Fibonacci(10):
    print(fib, end=" ")
# 0 1 1 2 3 5 8 13 21 34
```

---

**Related:** [[Python Generators]] | [[Python For Loops]] | [[Functions and Advanced Concepts]]
