# Dictionaries in Python

## Introduction

If there is one data structure you must master to pass a coding interview, it is the hash map. In Python, this is implemented as the `dict` (dictionary).

Dictionaries allow you to store key-value pairs with average $O(1)$ lookup, insertion, and deletion times. This property makes them the optimal solution for reducing time complexity from $O(N^2)$ to $O(N)$ in countless algorithms.

---

## What You Need to Know

In coding interviews, you will frequently use dictionaries to:
- Count character or number frequencies (Frequency Maps).
- Cache results of expensive function calls (Memoization in DP).
- Store visited nodes in Graph traversals.
- Map relationships (e.g., parent-to-child in Trees).
- Implement the "Two Sum" pattern (trading space for time).

In this section, we will cover:
- **Hash Tables**: The underlying theory of how dictionaries achieve $O(1)$ time.
- **Python Dictionaries**: Creating, accessing, and safely updating dictionaries.
- **Dictionary Methods**: `get()`, `keys()`, `values()`, and `items()`.
- **Frequency Maps**: The most common interview use-case.
- **Dictionary Comprehensions**: Elegant ways to build mappings.
- **Interview Recipes**: Standard templates for common dictionary problems.

---

## Key Concept: Trading Space for Time

The defining characteristic of dictionary-based solutions in interviews is **trading space for time**.

If a naive solution uses a nested loop to search an array (taking $O(N^2)$ time and $O(1)$ space), you can almost always optimize it by storing the array elements in a dictionary first. This reduces the time complexity to $O(N)$ but increases the space complexity to $O(N)$.

This is the most common optimization expected by interviewers.
