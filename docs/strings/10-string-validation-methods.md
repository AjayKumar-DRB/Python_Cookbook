# String Validation Methods

## Introduction

During interviews, you will often need to parse strings and validate their contents. For example, a problem might ask you to extract all numbers from a mixed string, or verify if a string is a valid alphanumeric palindrome.

Python strings come with a suite of `is...()` methods that return `True` or `False`. Knowing these methods saves you from writing complex regular expressions or manual ASCII range checks.

---

## The Core Validation Methods

Here are the most important methods for coding interviews:

### `isalnum()`
Returns `True` if all characters are alphanumeric (letters and numbers) and the string is not empty.
```python
print("Python3".isalnum()) # True
print("Python 3!".isalnum()) # False (contains space and !)
```

### `isalpha()`
Returns `True` if all characters are alphabetic (letters only).
```python
print("Python".isalpha()) # True
print("Python3".isalpha()) # False (contains a number)
```

### `isdigit()`
Returns `True` if all characters are digits (`0-9`).
```python
print("12345".isdigit()) # True
print("123.45".isdigit()) # False (contains a decimal)
print("-123".isdigit()) # False (contains a minus sign)
```

---

## Interview Pattern: Valid Palindrome

A very common problem is checking if a string is a palindrome, ignoring casing and non-alphanumeric characters. 

You can use `isalnum()` to easily filter the string.

```python
def is_palindrome(s):
    # Filter out non-alphanumeric characters and lowercase the rest
    filtered = [char.lower() for char in s if char.isalnum()]
    
    # Check if the list reads the same forwards and backwards
    return filtered == filtered[::-1]

print(is_palindrome("A man, a plan, a canal: Panama")) # True
```

*(Note: In an actual interview, you might be asked to solve this in $O(1)$ space using two pointers, where `isalnum()` is still incredibly useful).*

```python
def is_palindrome_two_pointers(s):
    l, r = 0, len(s) - 1
    
    while l < r:
        if not s[l].isalnum():
            l += 1
        elif not s[r].isalnum():
            r -= 1
        elif s[l].lower() != s[r].lower():
            return False
        else:
            l += 1
            r -= 1
            
    return True
```

---

## Other Useful Methods

While less common, these might appear in specific parsing problems:

- `isspace()`: `True` if all characters are whitespace (spaces, tabs, newlines).
- `islower()` / `isupper()`: Checks if all cased characters match the case.
- `startswith(prefix)`: `True` if the string starts with the prefix.
- `endswith(suffix)`: `True` if the string ends with the suffix.

---

## Time Complexity

All of these validation methods iterate through the string character by character.
- **Time Complexity**: $O(N)$
- **Space Complexity**: $O(1)$ (they just return a boolean).

---

## Summary
- Use `isalnum()` heavily in palindrome and parsing problems to ignore punctuation.
- Use `isdigit()` to verify if a substring can be safely cast to an `int` (but beware of negative numbers and decimals).
- These methods are much faster and easier to read than writing `if 'a' <= char <= 'z':` or using regular expressions.
