# String Performance

## Introduction

In Python coding interviews, a correct algorithm can fail if the string operations used to implement it are inefficient. 

Because strings are immutable, operations that seem like $O(1)$ modifications are actually $O(N)$ allocations. Understanding these performance traps is essential for writing optimal code.

---

## The Concatenation Trap

The most frequent performance mistake candidates make is concatenating strings inside a loop.

### The Problem

```python
def build_string(n):
    result = ""
    for i in range(n):
        result += "a"
    return result
```

In many languages, appending a character to a string buffer is amortized $O(1)$. 
In Python, strings are immutable. `result += "a"` forces Python to allocate a brand new string of length $L+1$ and copy all existing characters over.

- 1st iteration: copy 1 char
- 2nd iteration: copy 2 chars
- ...
- $N$th iteration: copy $N$ chars

Total operations: $1 + 2 + \dots + N \approx \frac{N^2}{2}$.
This is an **$O(N^2)$ algorithm**.

### The Solution

Use a list to collect the pieces, then `join()` them at the end.

```python
def build_string_fast(n):
    result = []
    for i in range(n):
        result.append("a")
    return "".join(result)
```

Appending to a list is amortized $O(1)$. `"".join()` allocates the total required memory exactly once.
This is an **$O(N)$ algorithm**.

---

## The Slicing Trap

Slicing a string creates a **new string copy**. It does not return a view or a pointer.

### The Problem

```python
def process_string(s):
    while len(s) > 0:
        # Do something with s[0]
        
        # Remove the first character
        s = s[1:]
```

`s[1:]` copies the entire remaining string. If the string is length $N$, this loop copies $N-1$ chars, then $N-2$, etc.
This is an **$O(N^2)$ algorithm**.

### The Solution

If you need to repeatedly remove characters from the front of a string, either:

1. Use a pointer (index) to track your current position instead of modifying the string.
   
```python
def process_string_fast(s):
    for i in range(len(s)):
        char = s[i]
        # Do something with char
```

2. Convert the string to a `collections.deque`, which supports $O(1)$ removals from both ends.

```python
from collections import deque

def process_string_deque(s):
    q = deque(s)
    while q:
        char = q.popleft() # O(1)
```

---

## Searching Substrings

When you need to check if `substring in string`, Python uses the highly optimized Boyer-Moore-Horspool algorithm under the hood.

```python
if "pattern" in text:
    pass
```

While the worst-case time complexity is theoretically $O(N \times M)$ (where $N$ is text length and $M$ is pattern length), the average practical performance is often sub-linear $O(N/M)$. 

Do not try to write a manual search loop (which is strictly $O(N \times M)$) unless the interviewer specifically asks for a string matching algorithm. Rely on `in`, `find()`, or `startswith()`.

---

## Summary
- **Never** use `+=` to build strings in a loop. Use a list and `"".join()`.
- **Never** slice a string inside a loop to remove characters. Use index pointers or a `deque`.
- Rely on Python's built-in `in` and `find()` for searching, as they are implemented in highly optimized C code.
