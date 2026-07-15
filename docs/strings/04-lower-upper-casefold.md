# `lower()`, `upper()`, and `casefold()`

## Introduction

Many string problems (like checking for palindromes or anagrams) require case-insensitive comparisons. Python provides methods to easily convert the casing of strings.

---

## `lower()` and `upper()`

These methods return a new string with all characters converted to lowercase or uppercase.

```python
s = "Hello World"
print(s.lower()) # "hello world"
print(s.upper()) # "HELLO WORLD"
```

### When to use them

Use `lower()` when you need to normalize data before counting frequencies or storing them in a hash set.

```python
# Case-insensitive comparison
def is_equal_ignore_case(s1, s2):
    return s1.lower() == s2.lower()
```

---

## `casefold()` vs `lower()`

While `lower()` works perfectly for standard English ASCII characters, it is not aggressive enough for Unicode comparisons in some languages (e.g., German, Greek).

`casefold()` is a more aggressive version of `lower()` that is intended specifically for **caseless matching**.

For example, in German, the letter "ß" is equivalent to "ss".
- `"ß".lower()` remains `"ß"`.
- `"ß".casefold()` becomes `"ss"`.

```python
s1 = "straße"
s2 = "strasse"

print(s1.lower() == s2.lower())       # False
print(s1.casefold() == s2.casefold()) # True
```

### When to use `casefold()`
In most DSA coding interviews, the input is restricted to lowercase English letters, so `lower()` is perfectly fine. However, if you are asked a system design or robust parsing question where Unicode is involved, mentioning `casefold()` demonstrates deep Python knowledge.

---

## Checking Case

Python also provides boolean methods to check the current casing of a string.

- `islower()`: Returns `True` if all cased characters are lowercase.
- `isupper()`: Returns `True` if all cased characters are uppercase.

```python
print("hello".islower()) # True
print("Hello".islower()) # False
```
*(Note: Non-cased characters like numbers and spaces are ignored as long as there is at least one cased character).*

---

## Time and Space Complexity

- **Time Complexity**: $O(N)$ where $N$ is the length of the string.
- **Space Complexity**: $O(N)$ to allocate the new cased string.

---

## Summary
- Use `lower()` for standard case-insensitive comparisons in interviews.
- Know about `casefold()` as a trivia point for robust Unicode caseless matching.
- Remember that these methods allocate a new string.
