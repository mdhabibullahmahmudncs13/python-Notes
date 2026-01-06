# Doubly-Linked Lists

← [[07 - Deques and Linked Lists]] | [[Data Structures in Python]] | Next: [[09 - Recursion]] →

## Motivation

**Problem with singly-linked lists:**
- Removing from end requires finding previous node: $O(n)$
- Even with tail reference!

**Solution:** Each node links to **both** next and previous nodes

## Node Structure

```python
class Node:
    def __init__(self, data, prev=None, link=None):
        self.data = data
        self.prev = prev
        self.link = link  # next
```

**Visualization:**
```
       ┌──────────────────────────┐
       │                          ▼
┌──────┼──────┬──────┐    ┌──────┴──────┬──────┐
│ prev │ data │ link │───▶│ prev │ data │ link │───▶ None
└──────┴──────┴──────┘    └──────┬──────┴──────┘
       ▲                          │
       └──────────────────────────┘
```

## DoublyLinkedList Class

```python
class DoublyLinkedList:
    def __init__(self):
        self._head = None
        self._tail = None
        self._length = 0
    
    def __len__(self):
        return self._length
    
    def isempty(self):
        return self._length == 0
```

### Adding to Front

```python
def addfirst(self, item):
    new_node = Node(item, None, self._head)
    
    if self._head is None:  # Empty list
        self._head = new_node
        self._tail = new_node
    else:
        self._head.prev = new_node
        self._head = new_node
    
    self._length += 1
```

**Running time:** $O(1)$

### Adding to End

```python
def addlast(self, item):
    new_node = Node(item, self._tail, None)
    
    if self._tail is None:  # Empty list
        self._head = new_node
        self._tail = new_node
    else:
        self._tail.link = new_node
        self._tail = new_node
    
    self._length += 1
```

**Running time:** $O(1)$ - no traversal needed!

### Removing from Front

```python
def removefirst(self):
    if self.isempty():
        raise RuntimeError("Cannot remove from empty list")
    
    item = self._head.data
    self._head = self._head.link
    
    if self._head is None:  # List now empty
        self._tail = None
    else:
        self._head.prev = None
    
    self._length -= 1
    return item
```

**Running time:** $O(1)$

### Removing from End

```python
def removelast(self):
    if self.isempty():
        raise RuntimeError("Cannot remove from empty list")
    
    item = self._tail.data
    self._tail = self._tail.prev
    
    if self._tail is None:  # List now empty
        self._head = None
    else:
        self._tail.link = None
    
    self._length -= 1
    return item
```

**Running time:** $O(1)$ - use prev link! ✓

> [!important]
> This is the key advantage of doubly-linked lists!

## Complete Deque Implementation

```python
class Deque:
    def __init__(self):
        self._list = DoublyLinkedList()
    
    def addfirst(self, item):
        self._list.addfirst(item)
    
    def addlast(self, item):
        self._list.addlast(item)
    
    def removefirst(self):
        return self._list.removefirst()
    
    def removelast(self):
        return self._list.removelast()
    
    def __len__(self):
        return len(self._list)
    
    def isempty(self):
        return self._list.isempty()
```

All operations: $O(1)$! 🎉

Related: [[07 - Deques and Linked Lists#The Wrapper Pattern]]

## Performance Summary

### DoublyLinkedList

| Operation | Time | Compare to Singly-Linked |
|-----------|------|--------------------------|
| `addfirst` | $O(1)$ | Same |
| `addlast` | $O(1)$ | Same |
| `removefirst` | $O(1)$ | Same |
| `removelast` | $O(1)$ | **Improved!** (was $O(n)$) |
| `len` | $O(1)$ | Same |

### Cost

**Tradeoff:** Extra space for prev pointers

- **Memory:** 50% more pointers per node
- **Benefit:** $O(1)$ operations at both ends

> [!tip]
> Worth it when you need efficient operations at both ends!

## Concatenating Doubly Linked Lists

Joining two doubly-linked lists efficiently:

```python
def concatenate(self, other):
    """Append other list to end of this list."""
    if other.isempty():
        return
    
    if self.isempty():
        self._head = other._head
        self._tail = other._tail
    else:
        # Link tail of self to head of other
        self._tail.link = other._head
        other._head.prev = self._tail
        self._tail = other._tail
    
    self._length += other._length
    
    # Clear other list
    other._head = None
    other._tail = None
    other._length = 0
```

**Running time:** $O(1)$ - just update pointers!

Compare to lists:
```python
L1 = L1 + L2  # O(len(L1) + len(L2)) - must copy both!
```

> [!important]
> Linked list concatenation is $O(1)$, Python list concatenation is $O(n)$

See [[05 - Running Time Analysis#List Operations]]

## Sentinel Nodes

**Optional optimization:** Use dummy nodes at ends to simplify code

```python
class DoublyLinkedList:
    def __init__(self):
        # Create sentinel nodes
        self._head_sentinel = Node(None)
        self._tail_sentinel = Node(None)
        
        # Link them
        self._head_sentinel.link = self._tail_sentinel
        self._tail_sentinel.prev = self._head_sentinel
        
        self._length = 0
```

**Benefits:**
- No special cases for empty list
- Simplifies insertion/deletion code
- Fewer edge cases to test

**Cost:**
- Two extra nodes always present
- Slightly more memory

## Iteration

```python
class DoublyLinkedList:
    def __iter__(self):
        """Forward iteration."""
        current = self._head
        while current is not None:
            yield current.data
            current = current.link
    
    def __reversed__(self):
        """Backward iteration."""
        current = self._tail
        while current is not None:
            yield current.data
            current = current.prev

# Usage:
for item in dlist:           # Forward
    print(item)

for item in reversed(dlist): # Backward
    print(item)
```

> [!note]
> Doubly-linked lists can iterate in **both directions**!

Related: [[02 - Basic Python#Iterating over a collection]]

## When to Use Doubly-Linked Lists

**Use when:**
- Need $O(1)$ operations at both ends ([[07 - Deques and Linked Lists#The Deque ADT|Deque]])
- Need to iterate backwards
- Need efficient concatenation
- Frequent insertions/deletions at known positions

**Don't use when:**
- Need random access by index
- Memory is very constrained
- Only need stack or simple queue (singly-linked is enough)

## Comparison Summary

| Feature | Python List | Singly-Linked | Doubly-Linked |
|---------|-------------|---------------|---------------|
| Add to front | $O(n)$ | $O(1)$ | $O(1)$ |
| Add to back | $O(1)$ | $O(1)$ | $O(1)$ |
| Remove from front | $O(n)$ | $O(1)$ | $O(1)$ |
| Remove from back | $O(1)$ | $O(n)$ | $O(1)$ |
| Index access | $O(1)$ | $O(n)$ | $O(n)$ |
| Concatenate | $O(n)$ | $O(1)$ | $O(1)$ |
| Memory per item | 1 word | 2 words | 3 words |
| Reverse iteration | $O(1)$ | $O(n)$ | $O(1)$ |

## Related Topics

- [[07 - Deques and Linked Lists]] - Singly-linked lists and deques
- [[06 - Stacks and Queues]] - ADTs that can use doubly-linked lists
- [[05 - Running Time Analysis]] - Performance analysis
- [[03 - Object-Oriented Programming#Composition]] - Wrapper pattern
- [[16 - Trees]] - Another doubly-linked structure (parent/child pointers)

---

*Doubly-linked lists provide efficient operations at both ends at the cost of extra memory.*
