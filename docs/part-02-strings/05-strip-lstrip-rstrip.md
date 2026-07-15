# `strip()`, `lstrip()`, and `rstrip()`

## Introduction

In coding interviews involving parsing, input strings often come with unwanted leading or trailing whitespace. Python provides three built-in methods to clean the edges of a string: `strip()`, `lstrip()`, and `rstrip()`.

---

## How They Work

By default, these methods remove all whitespace (spaces, tabs, newlines) from the edges of a string.

- `strip()`: Removes from **both** ends.
- `lstrip()`: Removes from the **left** end only.
- `rstrip()`: Removes from the **right** end only.

```python
text = "   hello \n"

print(repr(text.strip()))  # 'hello'
print(repr(text.lstrip())) # 'hello \n'
print(repr(text.rstrip())) # '   hello'
```

---

## Stripping Specific Characters

You can pass a string argument to these methods. Python will remove any characters that appear in the argument string from the edges.

```python
text = "---hello---"
print(text.strip("-")) # "hello"
```

### Common Interview Mistake: Stripping is a Set of Characters
A very common misunderstanding is thinking that `strip("abc")` removes the exact substring `"abc"`. It does not. It removes **any** character `'a'`, `'b'`, or `'c'` from the edges until it hits a character not in the set.

```python
text = "abccbaHELLOabccba"

# This removes all a's, b's, and c's from the ends.
print(text.strip("abc")) # "HELLO"
```
If you want to remove an exact prefix or suffix (e.g., Python 3.9+), use `removeprefix()` or `removesuffix()`.

---

## When to Use Them

Use `strip()` heavily when:
- Reading lines from a file or standard input.
- Parsing CSVs or unformatted user input.
- Ensuring a string is perfectly clean before checking for a palindrome or passing it to an algorithm.

---

## Time and Space Complexity

- **Time Complexity**: $O(N)$ where $N$ is the length of the string. It iterates from the edges until it finds a non-matching character.
- **Space Complexity**: $O(N)$ to create the newly stripped string copy.

---

## Summary
- Use `strip()` to clean whitespace from both sides of a string.
- Passing arguments to `strip()` removes a **set of characters**, not an exact substring.
- Remember that `strip()` returns a new string and does not modify the original.
