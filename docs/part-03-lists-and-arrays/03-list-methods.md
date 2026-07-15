# List Methods & Time Complexities

## Introduction

Knowing the time complexities of built-in list methods is non-negotiable for coding interviews. Using the wrong method can silently turn an optimal $O(N)$ solution into a failing $O(N^2)$ solution.

---

## The $O(1)$ Operations (Fast)

These operations happen in constant time because they interact only with the end of the list or access elements by direct index.

### 1. `append(val)`
Adds an element to the **end** of the list.
- **Time Complexity**: $O(1)$ (amortized)

### 2. `pop()`
Removes and returns the element at the **end** of the list.
- **Time Complexity**: $O(1)$

Because `append()` and `pop()` are $O(1)$, Python lists are the perfect data structure for implementing a **Stack**.

### 3. Index Access (`list[i]`)
Accessing or updating an element by its index.
- **Time Complexity**: $O(1)$

### 4. `len(list)`
Python lists store their length as a C integer under the hood, so finding the length does not require traversing the list.
- **Time Complexity**: $O(1)$

---

## The $O(N)$ Operations (Slow)

These operations require shifting elements in memory or traversing the entire list.

### 1. `insert(index, val)`
Inserts an element at a specific index.
- **Time Complexity**: $O(N)$
- **Why?**: Every element after the insertion index must be shifted one position to the right. 
- **Interview Tip**: Never use `insert(0, val)` in a loop. It is $O(N^2)$.

### 2. `pop(index)` / `pop(0)`
Removes and returns the element at a specific index.
- **Time Complexity**: $O(N)$
- **Why?**: Every element after the removed index must be shifted one position to the left.
- **Interview Tip**: If you need to repeatedly remove from the front of a sequence (like a Queue), use `collections.deque` and `popleft()`, which is $O(1)$.

### 3. `remove(val)`
Finds the first occurrence of `val` and removes it.
- **Time Complexity**: $O(N)$ (to find it, plus $O(N)$ to shift elements left).

### 4. `val in list` (Membership Testing)
Checks if a value exists in the list.
- **Time Complexity**: $O(N)$
- **Interview Tip**: If you need to do membership checks inside a loop, convert the list to a `set` first ($O(N)$ once), then do $O(1)$ checks.

### 5. `min()`, `max()`, `sum()`
- **Time Complexity**: $O(N)$ (requires a full traversal).

---

## The $O(K)$ Operations

### 1. `extend(iterable)`
Appends multiple elements to the end of the list.
- **Time Complexity**: $O(K)$ where $K$ is the number of elements being added.

### 2. Slicing (`list[start:stop]`)
Creates a new list containing a subset of elements.
- **Time Complexity**: $O(K)$ where $K$ is the length of the slice.

---

## Summary Checklist

| Operation | Syntax | Time Complexity |
|-----------|--------|-----------------|
| Append | `l.append(x)` | $O(1)$ amortized |
| Pop End | `l.pop()` | $O(1)$ |
| Access | `l[i]` | $O(1)$ |
| Length | `len(l)` | $O(1)$ |
| Pop Front | `l.pop(0)` | 🚨 **$O(N)$** |
| Insert Front| `l.insert(0, x)`| 🚨 **$O(N)$** |
| Membership | `x in l` | 🚨 **$O(N)$** |

**Never use `pop(0)` or `insert(0, x)` in a loop.**
