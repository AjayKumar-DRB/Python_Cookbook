# Choosing Data Structures

> Picking the right tool for the job.

---

## Introduction

If you pick the wrong data structure, even a brilliant algorithmic pattern will fail due to poor time complexity. 

You must know exactly *why* and *when* to use each data structure based on their fundamental time complexities.

---

## The Decision Matrix

When planning your algorithm, ask yourself: *"What operation am I performing most often?"*

### 1. I need fast lookups by a key.
Use a **Dictionary (Hash Map)**.
- **Why:** Lookups, insertions, and deletions take $O(1)$ time on average.
- **Example Use Case:** Storing counts of elements, tracking seen elements with their index.

### 2. I need fast lookups, but I only care about existence (no keys).
Use a **Set (Hash Set)**.
- **Why:** $O(1)$ lookup time, and mathematically prevents duplicates.
- **Example Use Case:** Tracking visited nodes in a graph, checking if an element exists in a pool.

### 3. I need to maintain the "Top K" or "Minimum/Maximum" element dynamically.
Use a **Heap (Priority Queue)**.
- **Why:** Finding the min/max is $O(1)$. Pushing or popping is $O(\log N)$.
- **Example Use Case:** Finding the Kth largest element in a stream.

### 4. I need First-In, First-Out (FIFO) behavior.
Use a **Queue (`collections.deque`)**.
- **Why:** Appending and popping from the left is $O(1)$.
- **Example Use Case:** Breadth-First Search (BFS), processing events in order.

### 5. I need Last-In, First-Out (LIFO) behavior.
Use a **Stack (List)**.
- **Why:** Appending and popping from the right is $O(1)$.
- **Example Use Case:** Depth-First Search (DFS), parsing parentheses, undo operations.

### 6. I need to frequently insert or delete elements in the *middle* of a collection.
Use a **Linked List**.
- **Why:** Inserting or deleting a node (if you have a reference to it) is $O(1)$. Doing this in a List is $O(N)$ because all subsequent elements must be shifted.
- **Example Use Case:** LRU Cache implementation.

### 7. I need to do prefix lookups on strings (e.g., auto-complete).
Use a **Trie (Prefix Tree)**.
- **Why:** Lookups take $O(L)$ time where $L$ is the length of the string, regardless of how many millions of strings are in the dictionary.
- **Example Use Case:** Word Search II, Autocomplete systems.

---

## Common Pitfalls

### Pitfall 1: Using `list.pop(0)`
If you use a standard Python list as a Queue and do `my_list.pop(0)`, it takes $O(N)$ time because all other elements must shift left. In a `while` loop, this degrades your algorithm to $O(N^2)$ and you will fail the interview.
**Fix:** Always use `collections.deque` and `popleft()` for $O(1)$ removal.

### Pitfall 2: Using `in` on a list
If you check `if item in my_list:`, it takes $O(N)$ time. If you do this inside a loop, it becomes $O(N^2)$.
**Fix:** Convert the list to a `set` first, so `if item in my_set:` takes $O(1)$ time.

---

## Key Takeaways

- **Hash Maps / Sets:** Fast $O(1)$ lookups.
- **Heaps:** Fast $O(\log N)$ min/max tracking.
- **Deque:** Fast $O(1)$ queues.
- **List:** Fast $O(1)$ stacks.
- Know the time complexity of the underlying operations of your chosen data structure.

---

## Related Topics

- [Python Dictionaries](../dictionaries/03-python-dictionaries.md)
- [Python Sets](../sets/03-python-sets.md)
- [Deque](../collections/02-deque.md)
- [Heapq](../standard-library/02-heapq.md)
