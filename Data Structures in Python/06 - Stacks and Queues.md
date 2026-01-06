# Stacks and Queues

← [[05 - Running Time Analysis]] | [[Data Structures in Python]] | Next: [[07 - Deques and Linked Lists]] →

## Abstract Data Types (ADTs)

An **Abstract Data Type** describes:
- What data is stored
- What operations are supported
- **Not** how it's implemented

> [!important]
> ADT = Interface/Behavior, not Implementation

Related: [[03 - Object-Oriented Programming#Encapsulation]] for public interfaces

## The Stack ADT

**Mental model:** Stack of plates
- Add to top (**push**)
- Remove from top (**pop**)
- Look at top without removing (**peek**)

**LIFO:** **L**ast **I**n, **F**irst **O**ut

### Stack Operations

| Operation | Description | Returns |
|-----------|-------------|---------|
| `push(item)` | Add item to top | None |
| `pop()` | Remove and return top item | item |
| `peek()` | Return top item without removing | item |
| `isempty()` | Check if stack is empty | bool |

### Stack Implementation with List

```python
class ListStack:
    def __init__(self):
        self._L = []
    
    def push(self, item):
        self._L.append(item)
    
    def pop(self):
        return self._L.pop()
    
    def peek(self):
        return self._L[-1]
    
    def isempty(self):
        return len(self._L) == 0
```

**Running time:** All operations $O(1)$ 

See [[05 - Running Time Analysis#List Operations]] for list operation costs.

### Stack Applications

**Reversing:**
```python
def reverse(L):
    stack = ListStack()
    for item in L:
        stack.push(item)
    result = []
    while not stack.isempty():
        result.append(stack.pop())
    return result
```

**Matching parentheses:**
```python
def match_parens(s):
    stack = ListStack()
    for char in s:
        if char == '(':
            stack.push(char)
        elif char == ')':
            if stack.isempty():
                return False
            stack.pop()
    return stack.isempty()
```

Related: [[09 - Recursion#Call Stack]] - function calls use a stack!

## The Queue ADT

**Mental model:** Line at a store
- Join at back (**enqueue**)
- Leave from front (**dequeue**)

**FIFO:** **F**irst **I**n, **F**irst **O**ut

### Queue Operations

| Operation | Description | Returns |
|-----------|-------------|---------|
| `enqueue(item)` | Add item to back | None |
| `dequeue()` | Remove and return front item | item |
| `peek()` | Return front item without removing | item |
| `isempty()` | Check if queue is empty | bool |

### Naive Queue Implementation

```python
class ListQueueNaive:
    def __init__(self):
        self._L = []
    
    def enqueue(self, item):
        self._L.append(item)
    
    def dequeue(self):
        return self._L.pop(0)  # Problem!
    
    def peek(self):
        return self._L[0]
    
    def isempty(self):
        return len(self._L) == 0
```

> [!warning]
> **Problem:** `L.pop(0)` is $O(n)$ - must shift all elements!

### Better Queue Implementation

**Idea:** Track front index, only shift when necessary

```python
class ListQueue:
    def __init__(self):
        self._L = []
        self._front = 0
    
    def enqueue(self, item):
        self._L.append(item)
    
    def dequeue(self):
        item = self._L[self._front]
        self._front += 1
        # Clean up if too much wasted space
        if self._front > len(self._L) // 2:
            self._L = self._L[self._front:]
            self._front = 0
        return item
    
    def peek(self):
        return self._L[self._front]
    
    def isempty(self):
        return self._front == len(self._L)
```

**Amortized running time:** $O(1)$ per operation

> [!note]
> **Amortized analysis:** Average cost over sequence of operations
> - Some operations expensive
> - Most operations cheap
> - Average is good

Related: [[05 - Running Time Analysis#Big-O Notation]]

## Dealing with Errors

### Option 1: Return Special Value

```python
def dequeue(self):
    if self.isempty():
        return None
    return self._L[self._front]
```

**Problem:** Can't distinguish empty queue from queue containing `None`

### Option 2: Raise Exception

```python
def dequeue(self):
    if self.isempty():
        raise RuntimeError("Cannot dequeue from empty queue")
    return self._L[self._front]
```

**Better:** Explicit error message

### Option 3: Custom Exception

```python
class QueueEmptyError(Exception):
    pass

class ListQueue:
    # ... other methods ...
    
    def dequeue(self):
        if self.isempty():
            raise QueueEmptyError("Queue is empty")
        item = self._L[self._front]
        self._front += 1
        return item
```

**Best:** Caller can catch specific exception

```python
try:
    item = queue.dequeue()
except QueueEmptyError:
    print("Queue was empty!")
```

Related: [[02 - Basic Python#Try Blocks]] for exception handling, [[04 - Testing]] for testing error cases

## Comparison: Stack vs Queue

| Aspect | Stack | Queue |
|--------|-------|-------|
| Order | LIFO | FIFO |
| Add | Push to top | Enqueue to back |
| Remove | Pop from top | Dequeue from front |
| Analogy | Stack of plates | Line at store |
| Uses | Recursion, undo, parsing | Scheduling, breadth-first search |

## Queue Applications

**Task scheduling:**
```python
task_queue = ListQueue()
task_queue.enqueue("Process email")
task_queue.enqueue("Update database")
task_queue.enqueue("Generate report")

while not task_queue.isempty():
    task = task_queue.dequeue()
    process(task)
```

**Breadth-first search:**
See [[16 - Trees#Breadth-First Search]] for graph/tree traversal

## Performance Summary

### ListStack

| Operation | Time |
|-----------|------|
| `push` | $O(1)$ |
| `pop` | $O(1)$ |
| `peek` | $O(1)$ |
| `isempty` | $O(1)$ |

### ListQueue

| Operation | Time (Amortized) |
|-----------|------------------|
| `enqueue` | $O(1)$ |
| `dequeue` | $O(1)$ |
| `peek` | $O(1)$ |
| `isempty` | $O(1)$ |

## Design Principles

> [!tip]
> **Separate interface from implementation**
> - Define what operations are needed (ADT)
> - Implement efficiently
> - Can change implementation without changing code that uses it

This follows [[03 - Object-Oriented Programming#Duck Typing|duck typing]] - any class with right methods can be used!

## Related Topics

- [[07 - Deques and Linked Lists]] - More flexible data structures
- [[08 - Doubly-Linked Lists]] - Efficient implementation
- [[09 - Recursion#Call Stack]] - Stacks in function calls
- [[16 - Trees#Breadth-First Search]] - Queue-based algorithm
- [[05 - Running Time Analysis]] - Analyzing performance

---

*Stacks and queues are simple but powerful abstractions.*
