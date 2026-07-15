# `replace()`

## Introduction

The `replace()` method replaces occurrences of a substring with another substring. Since strings are immutable, `replace()` returns a completely new string.

It is useful for data cleaning, formatting, and simple character substitutions.

---

## How `replace()` Works

The method takes two required arguments: the `old` substring and the `new` substring.

```python
text = "I love Java"
new_text = text.replace("Java", "Python")

print(new_text) # "I love Python"
```

### The `count` Parameter

You can provide a third argument to limit the number of replacements.

```python
text = "apple apple apple"

# Replace only the first two occurrences
print(text.replace("apple", "orange", 2))
# "orange orange apple"
```

---

## When to use `replace()`

Use `replace()` when you need to swap entire substrings or remove specific characters (by replacing them with `""`).

```python
phone = "(555) 123-4567"

# Removing formatting
clean = phone.replace("(", "").replace(")", "").replace(" ", "").replace("-", "")
print(clean) # "5551234567"
```
*(Note: If you are replacing many different characters, regular expressions or list comprehensions might be cleaner).*

---

## Common Interview Mistakes

### Mistake: Forgetting that strings are immutable
Because strings are immutable, `replace()` does not modify the string in-place. If you don't reassign the result, nothing happens.

**Incorrect:**
```python
s = "hello"
s.replace("h", "j")
print(s) # "hello"
```

**Correct:**
```python
s = "hello"
s = s.replace("h", "j")
print(s) # "jello"
```

### Mistake: Overlapping replacements
`replace()` does not perform overlapping replacements. It processes the string from left to right.

```python
text = "aaaa"
# The first "aa" is replaced, then the second "aa" is replaced.
print(text.replace("aa", "b")) # "bb"
```

---

## Time and Space Complexity

- **Time Complexity**: $O(N)$ where $N$ is the length of the string.
- **Space Complexity**: $O(N)$ to create the new string.

---

## Summary
- `s.replace(old, new, [count])` returns a new string with replacements made.
- Remember to reassign the result because strings are immutable.
- Use it to easily remove unwanted substrings by replacing them with `""`.
