# Sorting in Python

## Introduction

Sorting is a fundamental operation in computer science. In interviews, sorting an array is frequently the first step to optimizing a problem (e.g., transforming an $O(N^2)$ brute-force Two Sum search into an $O(N \log N)$ Two Pointer solution).

Python provides highly optimized, built-in sorting mechanisms. Unless an interviewer explicitly asks you to "implement Merge Sort," you are expected to use Python's built-in sorting.

---

## What You Need to Know

In coding interviews, you will frequently need to:
- Sort an array in place to save memory.
- Sort strings, tuples, or custom objects.
- Sort by multiple criteria (e.g., sort by length, then alphabetically).
- Understand the time and space complexity of Python's underlying sorting algorithm.

In this section, we will cover:
- **`sort()` vs `sorted()`**: When to modify in place vs returning a new list.
- **Custom Sorting**: Using the `key` argument and `lambda` functions.
- **Timsort**: The algorithm powering Python's sort, and its performance characteristics.
- **Stable Sorting**: What stability means and how to leverage it for complex sorts.
- **Interview Recipes**: Standard patterns for interval merging, anagram grouping, and multi-field sorting.

---

## Key Concept: The Sorting Optimization

When facing an array problem, always ask yourself: *"Would sorting the array help?"*

If the problem involves:
- Finding duplicates
- Finding the Kth largest/smallest item
- Interval overlaps
- 3Sum or Closest Sums

Sorting is almost certainly part of the optimal solution. 
Because sorting takes $O(N \log N)$ time, if your current brute-force approach is $O(N^2)$, sorting the array first is a mathematically "free" operation that often unlocks a faster $O(N)$ linear scan.
