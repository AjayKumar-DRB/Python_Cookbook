# Lists and Arrays in Python

## Introduction

In Python, the primary sequence data structure is the `list`. Unlike arrays in C or Java, Python lists are dynamic, heterogenous, and extremely flexible. 

They are the most commonly used data structure in Data Structures and Algorithms (DSA) interviews. Whether you are implementing a stack, a queue, an adjacency list for a graph, or a memoization table, you will use a Python list.

---

## What You Need to Know

In coding interviews, you will frequently use lists to:
- Store ordered collections of elements.
- Implement Stacks (using `append()` and `pop()`).
- Track paths in Depth-First Search (DFS).
- Build matrices for Dynamic Programming (DP) or Graph problems.

In this section, we will cover:
- **How Python Lists Work**: Understanding dynamic arrays under the hood.
- **List Operations**: `append()`, `pop()`, `insert()`, and their performance.
- **Indexing and Slicing**: Extracting and reversing data.
- **Multidimensional Lists**: Creating and manipulating matrices safely.
- **Pythonic Iteration**: Using `enumerate()`, `zip()`, and list comprehensions.
- **Interview Recipes**: Standard templates for common array problems.

---

## Key Concept: Time Complexity Traps

The most important concept to master in this section is the **time complexity of list operations**.

Because Python hides the underlying memory management, it is incredibly easy to accidentally turn an $O(N)$ algorithm into an $O(N^2)$ algorithm by using operations like `insert(0, val)` or `pop(0)`. 

Interviewers specifically look for these mistakes. By the end of this chapter, you will know exactly when to use a list and when to reach for a more specialized structure like `collections.deque`.
