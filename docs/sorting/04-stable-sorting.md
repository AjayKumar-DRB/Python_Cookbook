# Stable Sorting

## Introduction

Python's Timsort is a **stable** sorting algorithm. 

In a stable sort, if two elements have the exact same sorting key, their original relative order is preserved in the sorted output. 

Understanding stability allows you to perform complex multi-pass sorts effortlessly.

---

## What is Stability?

Imagine sorting a list of files by their size.

```python
files = [
    ("a.txt", 100),
    ("b.txt", 50),
    ("c.txt", 100)
]

# Sort by size (index 1)
files.sort(key=lambda x: x[1])
```

Because 100 == 100, `a.txt` and `c.txt` tie. 
In an *unstable* sort (like Quick Sort), `c.txt` might randomly end up before `a.txt`.
In a **stable** sort (like Python's Timsort), because `a.txt` came before `c.txt` in the original array, it is guaranteed to come before `c.txt` in the sorted array.

---

## The Multi-Pass Sort Trick

Suppose an interview question asks you to sort an array of logs.
- Primary condition: Sort by User ID (Ascending).
- Secondary condition: Sort by Action Name (Descending).

Because Action Name is a string, you cannot easily negate it in a tuple `key=lambda x: (x.id, -x.action)`.

Instead, you can leverage stability by **sorting multiple times, starting with the least important condition and ending with the most important condition**.

```python
logs = [
    {"id": 2, "action": "LOGIN"},
    {"id": 1, "action": "LOGOUT"},
    {"id": 2, "action": "CLICK"}
]

# 1. Sort by Secondary Condition first (Action Descending)
logs.sort(key=lambda x: x["action"], reverse=True)

# 2. Sort by Primary Condition last (ID Ascending)
# Because it is a stable sort, ties in ID will preserve 
# the descending Action order established in Step 1!
logs.sort(key=lambda x: x["id"])

for log in logs:
    print(log)
    
# {'id': 1, 'action': 'LOGOUT'}
# {'id': 2, 'action': 'LOGIN'}
# {'id': 2, 'action': 'CLICK'}
```

---

## Time Complexity of Multi-Pass

Running $O(N \log N)$ twice is still $O(N \log N)$. Furthermore, because Timsort is heavily optimized for partially sorted data, the second sort pass runs incredibly fast.

---

## Summary
- Python's sort is **stable** (preserves original order on ties).
- If you have complex multi-criteria sorting (especially mixing ascending and descending strings), sort multiple times.
- Always sort from **least important** criteria to **most important** criteria.
