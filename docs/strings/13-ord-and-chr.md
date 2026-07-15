# `ord()` and `chr()`

## Introduction

Python provides two built-in functions for converting between a character and its corresponding integer code point: `ord()` and `chr()`.

You will use these functions frequently in string manipulation problems, especially those involving ciphers, character shifting, or array-based frequency counting.

---

## `ord()`: Character to Integer

The `ord()` function takes a string of length 1 and returns its integer Unicode code point.

```python
print(ord('a')) # 97
print(ord('A')) # 65
print(ord('0')) # 48
```

### When to use `ord()`

Use `ord()` when you need to calculate the distance between two characters or map a character to an array index.

```python
# Finding the distance between 'a' and 'd'
distance = ord('d') - ord('a')
print(distance) # 3
```

---

## `chr()`: Integer to Character

The `chr()` function is the inverse of `ord()`. It takes an integer and returns the corresponding character.

```python
print(chr(97)) # 'a'
print(chr(65)) # 'A'
print(chr(48)) # '0'
```

### When to use `chr()`

Use `chr()` when you need to construct a string from integer values, such as when implementing a Caesar Cipher or shifting characters.

```python
# Shift a character by 3 positions
original_char = 'a'
shifted_int = ord(original_char) + 3
shifted_char = chr(shifted_int)

print(shifted_char) # 'd'
```

---

## Interview Pattern: Shifting Letters with Wraparound

A common interview question asks you to shift a letter by $k$ positions, wrapping around from 'z' back to 'a'.

To do this correctly:
1. Normalize the character to a `0-25` index by subtracting `ord('a')`.
2. Add the shift amount $k$.
3. Use the modulo operator `% 26` to handle wraparound.
4. Convert back to an ASCII integer by adding `ord('a')`.
5. Use `chr()` to get the new character.

### Example: Caesar Cipher

```python
def shift_char(char, k):
    if not char.islower():
        return char # Ignore non-lowercase characters
        
    # Step 1: Normalize to 0-25
    zero_indexed = ord(char) - ord('a')
    
    # Step 2 & 3: Shift and wrap around
    shifted_zero_indexed = (zero_indexed + k) % 26
    
    # Step 4: Convert back to ASCII range
    shifted_ascii = shifted_zero_indexed + ord('a')
    
    # Step 5: Convert to character
    return chr(shifted_ascii)

print(shift_char('y', 3)) # 'b'
```

---

## Common Interview Mistakes

### Mistake: Forgetting to handle wraparound properly
If you simply do `chr(ord(char) + k)`, shifting `'z'` by `1` will result in `'{'` (ASCII 123) instead of `'a'`. Always normalize to `0-25`, use modulo, and add `ord('a')` back.

### Mistake: Passing multi-character strings to `ord()`
`ord()` only accepts strings of length 1. 

```python
# This raises a TypeError
ord("abc") 
```

---

## Time and Space Complexity

- **Time Complexity**: $O(1)$ for both `ord()` and `chr()`.
- **Space Complexity**: $O(1)$ for both `ord()` and `chr()`.

---

## Summary
- `ord(c)` converts a character to its integer code.
- `chr(i)` converts an integer back to its character.
- Always normalize to a `0-25` index when shifting letters to easily handle wraparounds using modulo arithmetic.
