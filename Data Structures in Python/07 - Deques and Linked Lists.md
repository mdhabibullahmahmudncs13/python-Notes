# Deques and Linked Lists

← [[06 - Stacks and Queues]] | [[Data Structures in Python]] | Next: [[08 - Doubly-Linked Lists]] →

## The Deque ADT

**Deque** (pronounced "deck"): **D**ouble-**E**nded **Que**ue

Operations at **both** ends:
- Add/remove from front
- Add/remove from back

### Deque Operations

| Operation | Description | Returns |
|-----------|-------------|---------|
| `addfirst(item)` | Add item to front | None |
| `addlast(item)` | Add item to back | None |
| `removefirst()` | Remove and return front item | item |
| `removelast()` | Remove and return back item | item |
| `len()` | Number of items | int |

> [!note]
> Deque generalizes both [[06 - Stacks and Queues#The Stack ADT|Stack]] and [[06 - Stacks and Queues#The Queue ADT|Queue]]!

### Deque as Stack

```python
# Stack operations using deque
push(item)    → addlast(item)
pop()         → removelast()
```

### Deque as Queue

```python
# Queue operations using deque
enqueue(item) → addlast(item)
dequeue()     → removefirst()
```

## Why Not Use Lists?

Consider operations at both ends:

| Operation | List Time | Desired |
|-----------|-----------|---------|
| Add to end | $O(1)$ | $O(1)$ ✓ |
| Remove from end | $O(1)$ | $O(1)$ ✓ |
| Add to front | $O(n)$ | $O(1)$ ✗ |
| Remove from front | $O(n)$ | $O(1)$ ✗ |

> [!important]
> Lists are inefficient for operations at the front!

See [[05 - Running Time Analysis#List Operations]] for why.

## Linked Lists

**Big idea:** Store items in **nodes** with **links** to next node

### Node Structure

```python
class Node:
    def __init__(self, data, link=None):
        self.data = data
        self.link = link
```

**Visualization:**
```
┌──────┬──────┐    ┌──────┬──────┐    ┌──────┬──────┐
│ data │ link │───▶│ data │ link │───▶│ data │ None │
└──────┴──────┘    └──────┴──────┘    └──────┴──────┘
```

### Building a Linked List

```python
# Create nodes
node1 = Node(3)
node2 = Node(5) node3 = Node(9)

# Link them
node1.link = node2
node2.link = node3

# Or chain construction:
L = Node(3, Node(5, Node(9)))
```

### Traversing a Linked List

```python
current = L
while current is not None:
    print(current.data)
    current = current.link
```

## LinkedList Class

```python
class LinkedList:
    def __init__(self):
        self._head = None
        self._length = 0
    
    def addfirst(self, item):
        self._head = Node(item, self._head)
        self._length += 1
    
    def removefirst(self):
        if self._head is None:
            raise RuntimeError("Cannot remove from empty list")
        item = self._head.data
        self._head = self._head.link
        self._length -= 1
        return item
    
    def __len__(self):
        return self._length
```

**Running time:**
- `addfirst`: $O(1)$ - just update head
- `removefirst`: $O(1)$ - just update head
- `len`: $O(1)$ - store length

> [!tip]
> Storing length avoids $O(n)$ traversal to count nodes!

### Adding to End (Naive)

```python
def addlast(self, item):
    if self._head is None:
        self.addfirst(item)
    else:
        # Find last node
        current = self._head
        while current.link is not None:
            current = current.link
        # Add new node
        current.link = Node(item)
        self._length += 1
```

> [!warning]
> **Problem:** $O(n)$ time - must traverse entire list!

### Optimization: Store Tail Reference

```python
class LinkedList:
    def __init__(self):
        self._head = None
        self._tail = None
        self._length = 0
    
    def addfirst(self, item):
        self._head = Node(item, self._head)
        if self._tail is None:  # Was empty
            self._tail = self._head
        self._length += 1
    
    def addlast(self, item):
        if self._head is None:
            self.addfirst(item)
        else:
            self._tail.link = Node(item)
            self._tail = self._tail.link
            self._length += 1
```

**Now:** `addlast` is $O(1)$!

### Removing from End

```python
def removelast(self):
    if self._head is None:
        raise RuntimeError("Cannot remove from empty list")
    
    # Special case: only one node
    if self._head.link is None:
        item = self._head.data
        self._head = None
        self._tail = None
        self._length -= 1
        return item
    
    # Find second-to-last node
    current = self._head
    while current.link.link is not None:
        current = current.link
    
    item = current.link.data
    current.link = None
    self._tail = current
    self._length -= 1
    return item
```

> [!warning]
> Still $O(n)$ - need to find second-to-last node!

**Solution:** [[08 - Doubly-Linked Lists]] allow $O(1)$ removal from end

## Performance Summary

### LinkedList (Singly-Linked)

| Operation | Time | Notes |
|-----------|------|-------|
| `addfirst` | $O(1)$ | Update head |
| `addlast` | $O(1)$ | With tail reference |
| `removefirst` | $O(1)$ | Update head |
| `removelast` | $O(n)$ | Must find previous node |
| `len` | $O(1)$ | Store length |

### Comparison with List

| Operation | List | LinkedList |
|-----------|------|------------|
| Add to front | $O(n)$ | $O(1)$ ✓ |
| Add to back | $O(1)$ | $O(1)$ ✓ |
| Remove from front | $O(n)$ | $O(1)$ ✓ |
| Remove from back | $O(1)$ | $O(n)$ ✗ |
| Index access | $O(1)$ | $O(n)$ ✗ |

> [!important]
> **Tradeoff:** Linked lists excel at front operations but lose random access!

## Design Patterns: The Wrapper Pattern

**Problem:** LinkedList has different method names than built-in list

**Solution:** Create wrapper class matching expected interface

```python
class Stack:
    def __init__(self):
        self._L = LinkedList()
    
    def push(self, item):
        self._L.addfirst(item)
    
    def pop(self):
        return self._L.removefirst()
    
    def peek(self):
        return self._L._head.data
    
    def isempty(self):
        return len(self._L) == 0
```

**Benefits:**
- Matches expected [[06 - Stacks and Queues#The Stack ADT|Stack ADT]]
- Can swap implementations easily
- Follows [[03 - Object-Oriented Programming#Composition|composition]] ("has a" relationship)

Related: [[03 - Object-Oriented Programming#Composition and has a relationships]]

## Iterating over LinkedList

### Using Indices (Bad!)

```python
# Don't do this!
for i in range(len(L)):
    print(L[i])  # Each access is O(n)!
```

Total time: $O(n^2)$ 😱

### Using Iterator (Good!)

```python
class LinkedList:
    # ... other methods ...
    
    def __iter__(self):
        current = self._head
        while current is not None:
            yield current.data
            current = current.link

# Now can do:
for item in L:
    print(item)  # O(n) total!
```

> [!tip]
> Implementing `__iter__` allows using `for` loops naturally!

Related: [[02 - Basic Python#Iterating over a collection]]

## When to Use Linked Lists

**Use when:**
- Frequent insertions/deletions at beginning
- Don't need random access by index
- Size changes frequently

**Don't use when:**
- Need fast random access
- Access by index is common
- Memory overhead matters (nodes use extra space)

## Related Topics

- [[06 - Stacks and Queues]] - ADTs implemented with linked lists
- [[08 - Doubly-Linked Lists]] - Efficient operations at both ends
- [[05 - Running Time Analysis]] - Performance analysis
- [[03 - Object-Oriented Programming#Composition]] - Wrapper pattern
- [[16 - Trees]] - Another linked structure

---

*Linked lists trade random access for efficient insertion/deletion.*
