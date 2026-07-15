# Binary Numbers

> How computers represent data at the lowest level.

---

## Introduction

Before manipulating bits, you must thoroughly understand how numbers are represented in binary. Everything in a computer—strings, images, audio, and code—is ultimately stored as a sequence of 0s and 1s.

---

## What is it?

In our everyday Base-10 (Decimal) system, each digit represents a power of 10.
$145 = 1 \times 10^2 + 4 \times 10^1 + 5 \times 10^0$

In Base-2 (Binary), each digit (called a "bit") represents a power of 2.
$1001_2 = 1 \times 2^3 + 0 \times 2^2 + 0 \times 2^1 + 1 \times 2^0$
$1001_2 = 8 + 0 + 0 + 1 = 9_{10}$

---

## Binary Representation in Python

You can easily convert between decimal strings, binary strings, and integers in Python.

### `bin()`

The built-in `bin()` function converts an integer to its binary string representation. Python prefixes binary strings with `0b`.

```python
x = 9
print(bin(x))  # "0b1001"
```

### `int(string, base)`

You can parse a binary string back into an integer by specifying `base=2`.

```python
s = "1001"
print(int(s, 2))  # 9
```

---

## Python's Infinite Precision

In languages like C++ or Java, an `int` is strictly 32 bits. This means the highest bit (the 32nd bit) is used as the **sign bit** to represent negative numbers (Two's Complement).

**Python integers have arbitrary precision.** They grow as large as your computer's RAM allows. 
Because there is no fixed "highest bit", Python does not naturally represent negative numbers using Two's Complement. Instead, Python stores the sign separately and just prints a minus sign in front of the binary string.

```python
print(bin(9))   # "0b1001"
print(bin(-9))  # "-0b1001"
```

### Forcing 32-bit Two's Complement

In coding interviews (especially on LeetCode), problems often expect you to treat numbers as 32-bit integers.
To simulate a 32-bit unsigned integer in Python, you must manually apply a bitmask using `0xFFFFFFFF`.

```python
x = -9

# Get the 32-bit Two's Complement representation
# 0xFFFFFFFF is 32 ones: 11111111111111111111111111111111
unsigned_32bit = x & 0xFFFFFFFF
print(bin(unsigned_32bit)) # "0b11111111111111111111111111110111"
```

---

## Common Pitfalls

- **Forgetting the `0b` prefix:** When you use `bin()`, the string returned is like `"0b101"`. If you are iterating over the string to count the number of `1`s, make sure you ignore the first two characters.
- **Handling negatives in Python:** If a LeetCode problem involves negative numbers and bit manipulation (like "Sum of Two Integers"), Python solutions are notoriously much more difficult than Java/C++ solutions due to the infinite precision.

---

## Key Takeaways

- Binary is Base-2, where each digit represents a power of 2.
- Use `bin(x)` to get the binary string of an integer.
- Use `int("101", 2)` to parse a binary string.
- Python integers do not have a fixed bit length (no automatic Two's complement overflow).
- Mask with `0xFFFFFFFF` to simulate a 32-bit integer.

---

## Related Topics

- [Bitwise Operators](03-bitwise-operators.md)
- [Two's Complement Trick](../part-14-bit-manipulation/04-xor-tricks.md)
