# Indexing and Slicing

## Introduction

Because strings in Python are sequences, you can access individual characters using **indexing** and extract substrings using **slicing**.

Mastering slicing is critical for interviews. It allows you to reverse strings, extract prefixes or suffixes, and manipulate sequences succinctly without writing manual loops.

---

## Indexing

Python supports both positive (zero-based) and negative indexing.

```python
s = "Python"

# Positive indexing (left to right)
print(s[0]) # 'P'
print(s[2]) # 't'

# Negative indexing (right to left)
print(s[-1]) # 'n' (last character)
print(s[-2]) # 'o' (second to last character)
```

### Common Interview Mistake: `IndexError`
Attempting to access an index that is out of bounds will raise an `IndexError`. Always ensure `index < len(s)` before accessing.

---

## Slicing

Slicing extracts a substring. The syntax is `s[start:stop:step]`.

- `start`: The starting index (inclusive). Defaults to `0`.
- `stop`: The ending index (exclusive). Defaults to `len(s)`.
- `step`: The step size. Defaults to `1`.

### Basic Slicing

```python
s = "interview"

# From index 0 to 4 (exclusive)
print(s[0:5]) # "inter"

# Omit start to default to 0
print(s[:5])  # "inter"

# Omit stop to default to the end
print(s[5:])  # "view"
```

### Slicing with Negative Indices

```python
s = "interview"

# Last 4 characters
print(s[-4:]) # "view"

# Everything except the last 4 characters
print(s[:-4]) # "inter"
```

---

## The Step Parameter

The `step` parameter determines the increment.

```python
s = "abcdefg"

# Every second character
print(s[0:7:2]) # "aceg"
```

### Reversing a String
The most common use of the `step` parameter in coding interviews is string reversal using a step of `-1`.

```python
s = "hello"
reversed_s = s[::-1]
print(reversed_s) # "olleh"
```

This is the most Pythonic way to reverse a string. It is highly optimized and runs in C. 

---

## Slicing Gracefully Handles Out-of-Bounds

Unlike indexing, which raises an error if the index doesn't exist, **slicing handles out-of-bounds indices gracefully**.

```python
s = "cat"

# Indexing out of bounds crashes
# print(s[10]) -> IndexError

# Slicing out of bounds just returns the available characters (or an empty string)
print(s[1:10]) # "at"
print(s[10:20]) # ""
```

This is an incredibly useful property in interviews when dealing with substrings that might go slightly out of bounds.

---

## Performance Considerations

Slicing always creates a **new string object**. It does not return a view of the original string (unlike slices in Go or Rust).

```python
s = "A" * 1000000

# This allocates memory for a new string of length 500,000
first_half = s[:500000] 
```

### The Substring Time Complexity Trap

In a loop, slicing can unintentionally degrade your time complexity.

**Example: Removing the first character repeatedly**
```python
s = "abcdefg"
while s:
    # O(N) operation inside an O(N) loop!
    s = s[1:] 
```
The time complexity of this loop is $O(N^2)$ because `s[1:]` copies the string every iteration. 

If you need to repeatedly remove characters from the front of a string, convert it to a `collections.deque` instead.

---

## Time and Space Complexity

- **Time Complexity**: $O(K)$ where $K$ is the length of the slice being extracted.
- **Space Complexity**: $O(K)$ to store the newly created substring object.

---

## Summary
- `s[start:stop:step]` creates a new substring.
- Use negative indices like `s[-1]` to quickly access the end of a string.
- Use `s[::-1]` to reverse a string in Python.
- Slicing creates copies. Be careful not to slice strings repeatedly inside loops to avoid $O(N^2)$ time complexity.
