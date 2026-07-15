# `find()`, `index()`, and `count()`

## Introduction

Python strings have built-in methods for searching and counting substrings. While you could write your own loops to perform these tasks, using the standard library methods is faster, cleaner, and less prone to off-by-one errors.

---

## `find()`

The `find()` method searches for a substring and returns the **lowest index** where it begins. If the substring is not found, it returns `-1`.

```python
text = "hello world"
print(text.find("world")) # 6
print(text.find("Python")) # -1
```

### When to use `find()`
Use `find()` when you need to check if a substring exists and you also need its position, but you want to gracefully handle cases where the substring is missing.

---

## `index()`

The `index()` method behaves identically to `find()`, with one critical difference: if the substring is not found, it raises a `ValueError` instead of returning `-1`.

```python
text = "hello world"
print(text.index("world")) # 6

# Raises ValueError: substring not found
text.index("Python") 
```

### When to use `index()`
Use `index()` when the logic of your program dictates that the substring *must* exist. If it doesn't, failing early with an exception is the correct behavior. 

In most coding interviews, `find()` is safer unless you wrap `index()` in a `try-except` block.

---

## `count()`

The `count()` method returns the number of **non-overlapping** occurrences of a substring.

```python
text = "aaaa"
print(text.count("aa")) # 2 (not 3, because it doesn't overlap)
```

### When to use `count()`
Use `count()` when you need a quick frequency count of a specific character or substring. However, if you need the frequencies of *all* characters in the string, use `collections.Counter` instead, as calling `count()` for every character would be inefficient.

---

## Common Interview Mistakes

### Mistake: Calling `count()` inside a loop
A very common performance trap is calling `count()` inside a loop to build a frequency map.

**Incorrect:**
```python
s = "programming"
freq = {}
for char in s:
    # O(N) operation inside an O(N) loop
    freq[char] = s.count(char) 
```
This turns an $O(N)$ problem into an $O(N^2)$ problem.

**Correct:**
```python
from collections import Counter
s = "programming"
freq = Counter(s) # O(N) time
```

### Mistake: Manual searching instead of `find()`
Do not write a manual nested loop to search for a substring unless the problem specifically asks you to implement a string matching algorithm (like KMP or Rabin-Karp).

**Avoid:**
```python
# Manually searching for a substring (O(N*M))
def contains_substring(s, sub):
    for i in range(len(s) - len(sub) + 1):
        if s[i:i+len(sub)] == sub:
            return i
    return -1
```
Just use `s.find(sub)`—it's highly optimized in C.

---

## Time and Space Complexity

- **`find(sub)` and `index(sub)`**: 
  - **Time Complexity**: $O(N \times M)$ in the worst case (where $N$ is `len(s)` and $M$ is `len(sub)`), but typical performance is much faster due to the optimized Boyer-Moore-Horspool algorithm implemented in C.
  - **Space Complexity**: $O(1)$
- **`count(sub)`**:
  - **Time Complexity**: $O(N)$
  - **Space Complexity**: $O(1)$

---

## Summary
- Use `find()` to safely get the index of a substring or `-1`.
- Use `index()` if a missing substring should be treated as an error.
- Use `count()` to count occurrences, but avoid calling it inside a loop to prevent $O(N^2)$ time complexity.
