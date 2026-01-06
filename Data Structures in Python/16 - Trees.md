# Trees

← [[15 - Mappings and Hash Tables]] | [[Data Structures in Python]]

## What is a Tree?

**Tree:** Hierarchical data structure with:
- **Root** node at top
- **Parent-child** relationships
- **Leaves** - nodes with no children
- **No cycles** - exactly one path between any two nodes

**Visualization:**
```
        A          ← root
       /|\
      B C D        ← children of A
     /| |
    E F G          ← leaves
```

**Terminology:**
- **Parent**: Node directly above (A is parent of B)
- **Child**: Node directly below (B is child of A)
- **Sibling**: Nodes with same parent (B, C, D are siblings)
- **Ancestor**: Any node on path to root
- **Descendant**: Any node in subtree below
- **Depth**: Distance from root (E has depth 2)
- **Height**: Maximum depth of any node

Related: [[07 - Deques and Linked Lists#Linked Lists]] - linear structure vs tree

## Tree Node

```python
class TreeNode:
    def __init__(self, data):
        self.data = data
        self.children = []
    
    def add_child(self, child):
        self.children.append(child)

# Build tree
root = TreeNode('A')
b = TreeNode('B')
c = TreeNode('C')
d = TreeNode('D')

root.add_child(b)
root.add_child(c)
root.add_child(d)

b.add_child(TreeNode('E'))
b.add_child(TreeNode('F'))
c.add_child(TreeNode('G'))
```

## Binary Trees

**Binary Tree:** Each node has **at most 2 children** (left and right)

```python
class BinaryTreeNode:
    def __init__(self, data, left=None, right=None):
        self.data = data
        self.left = left
        self.right = right

# Build binary tree
root = BinaryTreeNode(1,
    BinaryTreeNode(2,
        BinaryTreeNode(4),
        BinaryTreeNode(5)
    ),
    BinaryTreeNode(3)
)
```

**Visualization:**
```
        1
       / \
      2   3
     / \
    4   5
```

### Types of Binary Trees

**Full Binary Tree:** Every node has 0 or 2 children

**Complete Binary Tree:** All levels filled except possibly last, filled left-to-right

**Perfect Binary Tree:** All internal nodes have 2 children, all leaves at same depth

**Balanced Binary Tree:** Height is $O(\log n)$

## Tree Traversals

### Depth-First Traversals

**Preorder:** Root → Left → Right

```python
def preorder(node):
    if node is None:
        return
    print(node.data)        # Visit root
    preorder(node.left)     # Traverse left
    preorder(node.right)    # Traverse right

# Output: 1, 2, 4, 5, 3
```

**Inorder:** Left → Root → Right

```python
def inorder(node):
    if node is None:
        return
    inorder(node.left)      # Traverse left
    print(node.data)        # Visit root
    inorder(node.right)     # Traverse right

# Output: 4, 2, 5, 1, 3
```

**Postorder:** Left → Right → Root

```python
def postorder(node):
    if node is None:
        return
    postorder(node.left)    # Traverse left
    postorder(node.right)   # Traverse right
    print(node.data)        # Visit root

# Output: 4, 5, 2, 3, 1
```

> [!tip]
> **Remember:** Pre/In/Post refers to when you **visit** the root

Related: [[09 - Recursion]] - tree traversals are naturally recursive

### Breadth-First Traversal (Level-Order)

Visit nodes level by level, left to right:

```python
from collections import deque

def level_order(root):
    if root is None:
        return
    
    queue = deque([root])
    
    while queue:
        node = queue.popleft()
        print(node.data)
        
        if node.left:
            queue.append(node.left)
        if node.right:
            queue.append(node.right)

# Output: 1, 2, 3, 4, 5
```

> [!note]
> Uses a [[06 - Stacks and Queues#The Queue ADT|queue]]!

## Binary Search Trees (BST)

**Property:** For every node:
- All values in **left** subtree ≤ node value
- All values in **right** subtree > node value

**Example:**
```
        8
       / \
      3   10
     / \    \
    1   6   14
       / \   /
      4   7 13
```

### BST Operations

**Search:**
```python
def search(node, target):
    if node is None:
        return False
    
    if target == node.data:
        return True
    elif target < node.data:
        return search(node.left, target)
    else:
        return search(node.right, target)
```

**Time:** $O(h)$ where $h$ = height
- **Balanced:** $O(\log n)$
- **Unbalanced:** $O(n)$ (like linked list)

**Insert:**
```python
def insert(node, value):
    if node is None:
        return BinaryTreeNode(value)
    
    if value <= node.data:
        node.left = insert(node.left, value)
    else:
        node.right = insert(node.right, value)
    
    return node
```

**Delete:** (more complex - see textbooks)

Related: [[11 - Binary Search]] - similar binary search principle

### BST vs Hash Table

| Operation | BST (balanced) | Hash Table |
|-----------|----------------|------------|
| Search | $O(\log n)$ | $O(1)$ avg |
| Insert | $O(\log n)$ | $O(1)$ avg |
| Delete | $O(\log n)$ | $O(1)$ avg |
| **Ordered** | **Yes** ✓ | No |
| Min/Max | $O(\log n)$ | $O(n)$ |
| Range queries | Efficient | Inefficient |

**Use BST when:**
- Need ordered data
- Need range queries
- Need min/max efficiently

**Use hash table when:**
- Only need lookup/insert/delete
- Don't need ordering

Related: [[15 - Mappings and Hash Tables]]

## AVL Trees (Self-Balancing BST)

**Idea:** Keep tree balanced by tracking heights and rotating

**Balance factor:** $|height(left) - height(right)| \leq 1$

**Rotations** restore balance after insert/delete:

```python
def rotate_right(y):
    """Right rotation around y."""
    x = y.left
    T2 = x.right
    
    x.right = y
    y.left = T2
    
    return x

def rotate_left(x):
    """Left rotation around x."""
    y = x.right
    T2 = y.left
    
    y.left = x
    x.right = T2
    
    return y
```

**Guarantee:** Height always $O(\log n)$ → all operations $O(\log n)$

## Heaps

**Heap:** Complete binary tree with **heap property**:

**Min-heap:** Every parent ≤ its children
**Max-heap:** Every parent ≥ its children

**Example (min-heap):**
```
        1
       / \
      3   2
     / \ / \
    7  5 6  4
```

### Heap as Array

Store complete binary tree in array:
- Root at index 0
- For node at index $i$:
  - Left child at $2i + 1$
  - Right child at $2i + 2$
  - Parent at $(i-1)//2$

```python
class MinHeap:
    def __init__(self):
        self._heap = []
    
    def push(self, value):
        """Add value and restore heap property."""
        self._heap.append(value)
        self._bubble_up(len(self._heap) - 1)
    
    def pop(self):
        """Remove and return minimum."""
        if not self._heap:
            raise IndexError("Empty heap")
        
        # Swap first and last
        self._heap[0], self._heap[-1] = self._heap[-1], self._heap[0]
        min_val = self._heap.pop()
        
        # Restore heap property
        if self._heap:
            self._bubble_down(0)
        
        return min_val
    
    def peek(self):
        """Return minimum without removing."""
        if not self._heap:
            raise IndexError("Empty heap")
        return self._heap[0]
    
    def _bubble_up(self, index):
        """Move element up to restore heap property."""
        parent = (index - 1) // 2
        
        if index > 0 and self._heap[index] < self._heap[parent]:
            self._heap[index], self._heap[parent] = \
                self._heap[parent], self._heap[index]
            self._bubble_up(parent)
    
    def _bubble_down(self, index):
        """Move element down to restore heap property."""
        left = 2 * index + 1
        right = 2 * index + 2
        smallest = index
        
        if left < len(self._heap) and self._heap[left] < self._heap[smallest]:
            smallest = left
        if right < len(self._heap) and self._heap[right] < self._heap[smallest]:
            smallest = right
        
        if smallest != index:
            self._heap[index], self._heap[smallest] = \
                self._heap[smallest], self._heap[index]
            self._bubble_down(smallest)

# Example
heap = MinHeap()
for val in [5, 3, 7, 1, 9, 2]:
    heap.push(val)

print(heap.pop())  # 1
print(heap.pop())  # 2
print(heap.pop())  # 3
```

### Heap Operations

| Operation | Time |
|-----------|------|
| `push` | $O(\log n)$ |
| `pop` | $O(\log n)$ |
| `peek` | $O(1)$ |
| Build heap from list | $O(n)$ |

### Python's heapq

```python
import heapq

# Min-heap (default)
heap = []
heapq.heappush(heap, 5)
heapq.heappush(heap, 3)
heapq.heappush(heap, 7)

print(heapq.heappop(heap))  # 3

# Create heap from list
data = [5, 3, 7, 1, 9, 2]
heapq.heapify(data)         # O(n)!
print(data)                 # [1, 3, 2, 5, 9, 7]

# N largest/smallest
print(heapq.nlargest(3, data))   # [9, 7, 5]
print(heapq.nsmallest(3, data))  # [1, 2, 3]
```

### Heap Applications

- **Priority queues** - process items by priority
- **Heapsort** - sorting in $O(n \log n)$ time, $O(1)$ space
- **Top-k problems** - see [[14 - Selection#Top-k Elements]]
- **Graph algorithms** - Dijkstra's shortest path
- **Median maintenance** - two heaps (min and max)

## Tries (Prefix Trees)

**Trie:** Tree for storing strings, sharing common prefixes

**Example:** Storing ["cat", "car", "card", "dog"]

```
         root
        /    \
       c      d
       |      |
       a      o
      / \     |
     t   r    g
         |
         d
```

```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_end = False

class Trie:
    def __init__(self):
        self.root = TrieNode()
    
    def insert(self, word):
        node = self.root
        for char in word:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
        node.is_end = True
    
    def search(self, word):
        node = self.root
        for char in word:
            if char not in node.children:
                return False
            node = node.children[char]
        return node.is_end
    
    def starts_with(self, prefix):
        node = self.root
        for char in prefix:
            if char not in node.children:
                return False
            node = node.children[char]
        return True

# Example
trie = Trie()
for word in ["cat", "car", "card", "dog"]:
    trie.insert(word)

print(trie.search("car"))          # True
print(trie.search("ca"))           # False (not complete word)
print(trie.starts_with("ca"))      # True
```

**Applications:**
- Autocomplete
- Spell checking
- IP routing
- Boggle/Scrabble solvers

## Tree Properties

### Number of Nodes

**Binary tree of height $h$:**
- Minimum nodes: $h + 1$ (linear chain)
- Maximum nodes: $2^{h+1} - 1$ (perfect tree)

**For $n$ nodes:**
- Minimum height: $\lceil \log_2(n+1) \rceil - 1$
- Maximum height: $n - 1$

### Balanced vs Unbalanced

**Balanced:** Height $O(\log n)$
```
      4
     / \
    2   6
   / \ / \
  1  3 5  7
```
Operations: $O(\log n)$

**Unbalanced:** Height $O(n)$
```
  1
   \
    2
     \
      3
       \
        4
```
Operations: $O(n)$ (like linked list!)

> [!important]
> Balance is crucial for tree performance!

## Summary: Tree Data Structures

| Structure | Ordering | Balance | Use Case |
|-----------|----------|---------|----------|
| **BST** | Yes (inorder) | Manual | Ordered data, range queries |
| **AVL** | Yes | Automatic | Guaranteed $O(\log n)$ |
| **Heap** | Partial | Implicit | Priority queue, top-k |
| **Trie** | By prefix | N/A | String operations, prefix search |
| **Hash Table** | No | N/A | Fast lookup, no ordering needed |

## Related Topics

- [[07 - Deques and Linked Lists]] - Linear vs hierarchical structures
- [[09 - Recursion]] - Tree traversals are recursive
- [[11 - Binary Search]] - Similar principle to BST search
- [[12 - Sorting#Heapsort]] - Sorting using heaps
- [[14 - Selection#Top-k Elements]] - Using heaps
- [[15 - Mappings and Hash Tables]] - Alternative to BSTs
- [[06 - Stacks and Queues]] - Used in tree traversals

---

*Trees: hierarchical structures providing efficient operations when properly balanced.*
