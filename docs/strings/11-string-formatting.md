# String Formatting

## Introduction

While string formatting is more common in development than in Data Structures and Algorithms (DSA) interviews, you may need to format output strings exactly as requested (e.g., returning time in `"HH:MM"` format, or building a specific return string).

Python offers several ways to format strings, but only one is the modern standard.

---

## F-Strings (Python 3.6+)

F-strings (formatted string literals) are the fastest, most readable, and most Pythonic way to format strings. 

Prefix the string with `f` and put variables directly inside curly braces `{}`.

```python
name = "Alice"
score = 95

# Using an f-string
result = f"Student {name} scored {score}%."
print(result) # "Student Alice scored 95%."
```

### When to use F-Strings
Always. If you need to embed variables into a string, use an f-string.

### Expressions Inside F-Strings
You can put entire expressions inside the curly braces.

```python
width = 10
height = 5
print(f"The area is {width * height}.") # "The area is 50."
```

---

## Padding and Alignment in F-Strings

In some interview questions, you might need to pad numbers with leading zeros (e.g., formatting hours and minutes). F-strings handle this elegantly.

```python
hours = 9
minutes = 5

# Pad with leading zeros to a width of 2
time_str = f"{hours:02d}:{minutes:02d}"
print(time_str) # "09:05"
```

You can also pad strings with spaces.
```python
text = "test"
print(f"{text:>10}") # Right align: "      test"
print(f"{text:<10}") # Left align:  "test      "
```

---

## Legacy Formatting Methods (Avoid)

You may see older Python code using `%` formatting or `.format()`. You should avoid these in interviews.

### The `.format()` Method
```python
# Avoid this if possible
result = "Student {} scored {}%.".format(name, score)
```
While valid, it is unnecessarily verbose compared to f-strings.

### The `%` Operator
```python
# Definitely avoid this
result = "Student %s scored %d%%." % (name, score)
```
This is the oldest method and is prone to type errors.

---

## Time and Space Complexity

- **Time Complexity**: $O(N)$ where $N$ is the length of the resulting string. F-strings evaluate at runtime and are highly optimized in C.
- **Space Complexity**: $O(N)$ to allocate the new string.

---

## Summary
- Always use **f-strings** (`f"..."`) for string formatting.
- Use format specifiers like `{value:02d}` to easily pad integers with leading zeros.
- Avoid `.format()` and `%s` in modern Python code.
