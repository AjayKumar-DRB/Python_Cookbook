# `collections.defaultdict`

## Introduction

A `defaultdict` works exactly like a standard dictionary, except it will automatically initialize a missing key with a default value. 

In coding interviews, it is the standard tool for building graphs (adjacency lists) and grouping elements.

---

## The Problem with Standard Dicts

When building a dictionary of lists (e.g., an adjacency list), a standard dictionary requires you to check if the key exists before appending.

**The Verbose Way:**
```python
edges = [("A", "B"), ("A", "C"), ("B", "C")]
graph = {}

for u, v in edges:
    if u not in graph:
        graph[u] = []
    graph[u].append(v)
```
This is tedious and error-prone under time pressure.

---

## Using `defaultdict`

You initialize a `defaultdict` by passing a **callable** (a factory function) that produces the default value.

Common factories:
- `list` (produces `[]`)
- `set` (produces `set()`)
- `int` (produces `0`)

**The Clean Way:**
```python
from collections import defaultdict

edges = [("A", "B"), ("A", "C"), ("B", "C")]

# Pass 'list' (not 'list()') to default to empty lists
graph = defaultdict(list)

for u, v in edges:
    # If 'u' doesn't exist, it automatically creates graph[u] = []
    graph[u].append(v)

print(graph)
# defaultdict(<class 'list'>, {'A': ['B', 'C'], 'B': ['C']})
```

---

## Common Use Cases

### 1. Adjacency Lists for Graphs
As shown above, `defaultdict(list)` is the standard way to represent a graph in Python.

### 2. Grouping Elements
If you need to group anagrams or similar items together:
```python
words = ["eat", "tea", "tan", "ate", "nat", "bat"]
groups = defaultdict(list)

for word in words:
    # Sort the string to use as a key
    key = tuple(sorted(word))
    groups[key].append(word)
```

### 3. Automatic Counters (Alternative to `Counter`)
While `Counter` is better for counting existing iterables, if you need to maintain counts on the fly with complex logic, use `defaultdict(int)`.

```python
counts = defaultdict(int)

counts["apple"] += 1 # "apple" defaults to 0, then adds 1
```

---

## Common Interview Mistakes

### Mistake: Calling the factory function
You must pass the function object itself, not the result of the function.

**Incorrect:**
```python
# TypeError: first argument must be callable or None
graph = defaultdict(list()) 
```

**Correct:**
```python
graph = defaultdict(list)
```

### Mistake: Missing keys create empty entries
If you check for a missing key in a `defaultdict`, it will permanently create that key with the default value!

```python
d = defaultdict(list)
print(d["missing"]) # []
print(d) # defaultdict(<class 'list'>, {'missing': []})
```
If you only want to *check* if a key exists without creating it, use the `in` operator.

---

## Summary
- Use `defaultdict(list)` to build graphs and group items cleanly.
- Pass the type (`list`, `set`, `int`), do not call it (`list()`).
- Accessing a missing key will create it permanently.
