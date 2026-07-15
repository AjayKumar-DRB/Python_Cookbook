# Frozenset

## Introduction

A `frozenset` is exactly what it sounds like: a set that is frozen (immutable).

Once a `frozenset` is created, you cannot add or remove elements. Because it is immutable, **a frozenset is hashable**, meaning it can be used as a key in a dictionary or added as an element to another set.

---

## Creating a Frozenset

You create a frozenset by passing an iterable to the `frozenset()` constructor.

```python
fs = frozenset([1, 2, 3])

# fs.add(4) # AttributeError: 'frozenset' object has no attribute 'add'
```

---

## When to use `frozenset` in Interviews

In standard algorithm questions, you rarely need a `frozenset`. However, it becomes critical in advanced Graph traversal or Dynamic Programming problems where the "state" includes a collection of unordered items.

### Example: Memoization with Unordered States
Imagine a DP problem where the current state is defined by your current node and the set of keys you have collected so far (e.g., Shortest Path to Get All Keys).

You need to store this state `(node, collected_keys)` in a `visited` set to avoid infinite loops.

If `collected_keys` is a standard `set`, you cannot hash the state because sets are unhashable.

```python
# This fails
state = (current_node, set(["key_A", "key_B"]))
# visited.add(state) # TypeError: unhashable type: 'set'
```

You must convert the collected keys to a `frozenset` first.

```python
# This works
state = (current_node, frozenset(["key_A", "key_B"]))
visited.add(state) 
```

Because order doesn't matter in a `frozenset`, `frozenset(["A", "B"])` has the exact same hash value as `frozenset(["B", "A"])`, making it perfect for representing unordered combinations in DP states.

---

## Time and Space Complexity

- **Time Complexity**: $O(N)$ to create a frozenset from an iterable of $N$ elements.
- **Space Complexity**: $O(N)$ to store the elements.

---

## Summary
- A `frozenset` is an immutable set.
- It is hashable.
- Use it when you need to use an unordered collection of items as a dictionary key or store it in a `visited` set for Graph/DP problems.
