# Built-in Functions

## Introduction

Python provides a rich set of built-in functions that are always available without importing any modules. 

In an interview, using these built-ins effectively shows that you write idiomatic, "Pythonic" code. A candidate who writes a 5-line `for` loop to find a maximum value will be judged less favorably than a candidate who simply calls `max()`.

---

## What You Need to Know

In coding interviews, you will frequently use built-ins to:
- Find the largest, smallest, or total value of an array (`max`, `min`, `sum`).
- Check if any or all elements in a sequence meet a condition (`any`, `all`).
- Iterate with indices (`enumerate`) or iterate over multiple arrays in parallel (`zip`).
- Sort arrays or strings (`sorted`).
- Manually advance an iterator in custom data structures (`iter`, `next`).

In this section, we will cover:
- **`any` and `all`**: Short-circuiting boolean evaluations.
- **`sum`, `min`, `max`**: Core reductions.
- **`map` and `filter`**: Functional programming tools (and when to avoid them).
- **`enumerate` and `zip`**: The correct way to iterate.
- **`sorted`**: Sorting out of place.
- **`iter` and `next`**: Under the hood of `for` loops.
- **Interview Recipes**: Combining built-ins with generators for one-line solutions.

---

## Key Concept: Lazy Evaluation

Many of Python's built-ins return **iterators**, not lists. 

Functions like `map()`, `filter()`, `zip()`, and `enumerate()` do not compute their results immediately. They evaluate "lazily"—yielding one element at a time only when requested. 

This means `zip(a, b)` takes $O(1)$ memory and time to initialize, regardless of how large the arrays are. 

If you actually need the result as a concrete list (for example, to index into it), you must wrap the call in `list()`, e.g., `list(zip(a, b))`.
