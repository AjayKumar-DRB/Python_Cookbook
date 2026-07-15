# The Python Standard Library for Interviews

## Introduction

Python's standard library is vast ("batteries included"), but for Data Structures and Algorithms (DSA) interviews, you only need to master a small subset of it.

Knowing these specific modules will save you from writing hundreds of lines of boilerplate code, preventing bugs and saving precious interview time.

---

## What You Need to Know

In coding interviews, you will frequently use the standard library to:
- Implement a Priority Queue / Min-Heap (`heapq`).
- Perform Binary Search on sorted arrays (`bisect`).
- Cache recursive function calls for Dynamic Programming (`functools.lru_cache`).
- Handle infinity and infinity-based comparisons (`math.inf`).
- Generate combinations and permutations (`itertools`).

In this section, we will cover:
- **`heapq`**: The standard array-based heap implementation.
- **`bisect`**: Optimized binary search.
- **`math`**: Essential mathematical constants and functions.
- **`functools`**: Decorators for caching and reduction.
- **`itertools`**: Combinatorics and advanced iterators.
- **`operator`**: Functional equivalents of mathematical operators.
- **Interview Recipes**: Standard templates for heaps, caching, and searching.

---

## Key Concept: Do Not Reinvent the Wheel

If a problem asks you to "Find the Kth Largest Element," you *could* write a complete Min-Heap class from scratch with `sift_up` and `sift_down` methods. It would take you 40 lines of code and 15 minutes.

Or, you could use `import heapq` and solve it in 5 lines. 

Unless the interviewer explicitly forbids it (e.g., "Design a Heap data structure"), you are expected to use these standard library modules. They demonstrate fluency in Python and an understanding of optimal, real-world engineering practices.
