# Sets and Hashing

## Introduction

Sets in Python are implemented using **Hash Tables**. They are identical to dictionaries under the hood, except they do not store a corresponding value for each key.

Because of this, sets share the exact same performance characteristics and constraints as dictionary keys.

---

## Performance

Since sets use a hash function to compute the exact memory index of an element:
- **Insertion**: $O(1)$ average
- **Lookup (`in`)**: $O(1)$ average
- **Deletion**: $O(1)$ average

### Worst-Case Complexity
Just like dictionaries, if many elements hash to the same index (a collision), Python must probe for empty slots. In the worst case, operations can degrade to $O(N)$. However, Python automatically resizes the underlying hash table to keep collisions rare. In an interview, always state the average $O(1)$ complexity.

---

## The Hashability Constraint

Because elements must be passed through a `hash()` function to determine their location, **all elements in a set must be immutable (hashable)**.

You cannot put mutable objects into a set.

```python
# Valid: integers, strings, tuples
valid_set = {1, "apple", (1, 2)}

# Invalid: lists, dictionaries, other sets
# TypeError: unhashable type: 'list'
# invalid_set = {1, [1, 2]} 
```

### Why?
If you could put a list into a set, and then later append an item to that list, its hash value would change. The set would no longer be able to find the list using the original hash index, breaking the $O(1)$ lookup guarantee.

---

## Interview Application: Hashing Paths

In many graph or grid problems, you need to keep track of the coordinates you have already visited to avoid infinite loops.

Because lists are unhashable, you must use **tuples** to store coordinates in your `visited` set.

```python
visited = set()

r, c = 2, 3

# Correct: tuple is hashable
visited.add((r, c))

# Incorrect: list is unhashable (TypeError)
# visited.add([r, c])
```

---

## Summary
- Sets provide $O(1)$ insertions, lookups, and deletions.
- Sets are Hash Tables under the hood.
- All elements in a set must be **immutable** (integers, strings, tuples).
- Always use tuples, not lists, when storing coordinates in a `visited` set.
