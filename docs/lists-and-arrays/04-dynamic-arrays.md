# Dynamic Arrays in Python

## Introduction

Python lists are implemented as **dynamic arrays** under the hood. 

Understanding how dynamic arrays manage memory is a very common trivia question in interviews, and it explains the time complexity of `append()`.

---

## How Dynamic Arrays Work

When you create an empty list, Python allocates a small chunk of contiguous memory in C.

```python
nums = []
```

As you append items, Python places them in the allocated slots.

```python
nums.append(1)
nums.append(2)
```

### The Reallocation Process

Eventually, the allocated memory fills up. When you try to append the next item, Python must:
1. Allocate a **brand new, larger** block of memory elsewhere (usually $1.125\times$ to $2\times$ the old size).
2. **Copy** all existing pointers from the old array to the new array.
3. Insert the new item.
4. Free the old memory.

This reallocation is an $O(N)$ operation.

---

## Amortized $O(1)$ Time Complexity

If reallocation takes $O(N)$ time, why do we say `append()` is $O(1)$?

Because reallocation happens infrequently. As the array grows, the amount of extra space allocated grows exponentially. The expensive $O(N)$ copies are "spread out" (amortized) over a large number of cheap $O(1)$ inserts.

Mathematically, over $N$ appends, the total time taken is proportional to $N$. Therefore, the average time per append is $O(N) / N = O(1)$.

### Interview Takeaway
If an interviewer asks for the time complexity of `list.append()`, the exact correct answer is:
> **"$O(1)$ amortized, but $O(N)$ worst-case."**

---

## Memory Overhead

Because dynamic arrays over-allocate to avoid frequent resizing, a Python list usually takes up more memory than strictly necessary to hold its elements.

For most DSA problems, this overhead is perfectly acceptable and expected.

---

## Summary
- Python lists are dynamic arrays.
- They grow by allocating a larger array and copying elements over.
- `append()` is **amortized $O(1)$**.
- `append()` is **worst-case $O(N)$**.
