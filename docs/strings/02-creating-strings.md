# Creating Strings

## Introduction

In Python, strings can be created in several ways. While creating strings is trivial, knowing when to use specific string creation methods can save you time and prevent bugs during interviews.

---

## Single and Double Quotes

Python allows strings to be enclosed in either single quotes (`'`) or double quotes (`"`).

```python
s1 = 'hello'
s2 = "hello"

print(s1 == s2) # True
```

### When to use which?

Use whichever prevents you from needing to escape characters. 

If your string contains a single quote (like an apostrophe), use double quotes to enclose the string.

```python
# Avoid this
s = 'It\'s a beautiful day'

# Do this instead
s = "It's a beautiful day"
```

---

## Multi-line Strings

Use triple quotes (`'''` or `"""`) for strings that span multiple lines.

```python
query = """
SELECT id, name
FROM users
WHERE age > 18
"""
```

In interviews, multi-line strings are rarely needed unless you are hardcoding a multiline test case or an ASCII grid.

---

## Converting Other Types to Strings

You will frequently need to convert integers, lists, or other data structures into strings.

### Using `str()`

The `str()` built-in function converts an object into its string representation.

```python
num = 42
text = str(num)
print(text) # "42"
```

### Common Interview Mistake: `str()` on Lists

Beginners sometimes try to convert a list of characters back into a string using `str()`.

**Incorrect:**
```python
chars = ['a', 'b', 'c']
result = str(chars)
print(result)
```

**Output:**
```python
"['a', 'b', 'c']"
```
This includes the brackets and commas as part of the string!

**Correct:**
Use `"".join()` to convert a list of characters or strings into a single string.

```python
chars = ['a', 'b', 'c']
result = "".join(chars)
print(result) # "abc"
```

---

## Time and Space Complexity

- **Time Complexity**: $O(N)$ where $N$ is the length of the string being created or the object being converted.
- **Space Complexity**: $O(N)$ to store the newly created string.

---

## Summary
- Single and double quotes are functionally identical.
- Always use `"".join()` instead of `str()` when converting a list of characters back into a single string.
