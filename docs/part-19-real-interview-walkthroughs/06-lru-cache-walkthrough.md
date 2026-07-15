# Walkthrough: LRU Cache

> **Difficulty:** Medium
> **Pattern:** Design (Hash Map + Doubly Linked List)

---

## The Prompt

**Interviewer:** "Design a data structure that follows the constraints of a Least Recently Used (LRU) cache. Implement the `LRUCache` class:
- `LRUCache(int capacity)` Initialize the LRU cache with positive size capacity.
- `int get(int key)` Return the value of the `key` if the key exists, otherwise return `-1`.
- `void put(int key, int value)` Update the value of the `key` if the `key` exists. Otherwise, add the `key-value` pair to the cache. If the number of keys exceeds the capacity from this operation, evict the least recently used key.

The functions `get` and `put` must each run in $O(1)$ average time complexity."

## Step 1: Match & Plan

**Candidate:** "To get $O(1)$ lookups, we absolutely need a Hash Map. But a Hash Map alone doesn't maintain an order of 'recentness', and we need to evict the least recently used item in $O(1)$ time."

**Interviewer:** "How can we maintain order and evict in $O(1)$?"

**Candidate:** "If we use an Array/List, updating the 'recentness' (moving an item to the front) would take $O(N)$ because everything else shifts. So we need a **Doubly Linked List**.
If we combine them, the Hash Map will store the `key` pointing to the actual `Node` in the Linked List. This allows us to find the node in $O(1)$, and because it's a Doubly Linked List, we can remove it and move it to the front in $O(1)$ time."

**Interviewer:** "Sounds like the standard architecture. Let's build it."

## Step 2: Implement (The Setup)

**Candidate:** "First, I'll define the Node class. It needs a key, a value, and next/prev pointers. We need the key inside the Node so that when we evict from the tail of the list, we know which key to delete from the Hash Map."

```python
class Node:
    def __init__(self, key, val):
        self.key = key
        self.val = val
        self.prev = None
        self.next = None
```

**Candidate:** "Now for the Cache class. I'll initialize the capacity, the hash map, and two dummy nodes: `left` and `right`. `left` will represent the Least Recently Used (LRU) end, and `right` will represent the Most Recently Used (MRU) end. Dummy nodes prevent null pointer exceptions when inserting/deleting."

```python
class LRUCache:
    def __init__(self, capacity: int):
        self.cap = capacity
        self.cache = {} # key: Node
        
        # Dummy nodes
        self.left = Node(0, 0)
        self.right = Node(0, 0)
        self.left.next = self.right
        self.right.prev = self.left
```

## Step 3: Implement (The Helpers)

**Candidate:** "Before writing `get` and `put`, I'll write two helper functions: `remove` and `insert`. This abstracts the messy pointer logic away."

```python
    # Remove node from list
    def remove(self, node):
        prev, nxt = node.prev, node.next
        prev.next = nxt
        nxt.prev = prev
        
    # Insert node at right (Most Recently Used)
    def insert(self, node):
        prev, nxt = self.right.prev, self.right
        prev.next = node
        nxt.prev = node
        node.prev = prev
        node.next = nxt
```

## Step 4: Implement (The Core Logic)

**Candidate:** "Now `get`. If the key exists, we return its value, but we also must update it to be the Most Recently Used. We do this by removing it and re-inserting it."

```python
    def get(self, key: int) -> int:
        if key in self.cache:
            # Update MRU
            self.remove(self.cache[key])
            self.insert(self.cache[key])
            return self.cache[key].val
        return -1
```

**Candidate:** "For `put`, if the key already exists, we must remove the old node first. Then we create the new node, insert it at the right, and put it in the cache."

```python
    def put(self, key: int, value: int) -> None:
        if key in self.cache:
            self.remove(self.cache[key])
            
        self.cache[key] = Node(key, value)
        self.insert(self.cache[key])
```

**Candidate:** "Finally, we check capacity. If we exceed it, we evict the LRU node, which is `left.next`."

```python
        if len(self.cache) > self.cap:
            # Remove from list and delete from map
            lru = self.left.next
            self.remove(lru)
            del self.cache[lru.key]
```

## Step 5: Python Specifics

**Interviewer:** "This is excellent. In Python, is there a built-in data structure that does exactly this?"

**Candidate:** "Yes! The `collections.OrderedDict`. It maintains insertion order, and we can `popitem(last=False)` to evict the LRU, and `move_to_end()` to update recentness. I could write this entire class in about 5 lines using `OrderedDict`."

**Interviewer:** "Perfect. I wanted to see the low-level implementation, but I'm glad you know `OrderedDict` exists."

---

## Interviewer Rubric Notes

- **Problem Solving:** Understood the need for a DLL + Hash Map for $O(1)$ operations.
- **Coding:** Fantastic modularity. Using `insert()` and `remove()` helper functions is a massive positive signal for code hygiene.
- **Verification:** Used dummy nodes to prevent null pointer bugs during list manipulation.
