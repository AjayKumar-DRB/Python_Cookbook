# Bitwise Operators

> The fundamental operators for manipulating individual bits.

---

## Introduction

Python supports standard bitwise operators that operate on numbers bit by bit. These operations execute incredibly fast at the hardware level.

---

## The Operators

| Operator | Name | Symbol | Description | Example (A=5, B=3) |
|----------|------|--------|-------------|-------------------|
| **AND** | `&` | `A & B` | Returns 1 if *both* bits are 1. | `101 & 011 = 001 (1)` |
| **OR** | `\|` | `A \| B` | Returns 1 if *either* bit is 1. | `101 \| 011 = 111 (7)` |
| **XOR** | `^` | `A ^ B` | Returns 1 if the bits are *different*. | `101 ^ 011 = 110 (6)` |
| **NOT** | `~` | `~A` | Inverts all bits (flips 0 to 1 and 1 to 0). | `~101 = ...111010 (-6)` |
| **Left Shift** | `<<` | `A << 1` | Shifts bits left by $N$ places (multiplies by $2^N$). | `101 << 1 = 1010 (10)` |
| **Right Shift**| `>>` | `A >> 1` | Shifts bits right by $N$ places (integer divides by $2^N$). | `101 >> 1 = 010 (2)` |

---

## Operator Breakdown

### AND (`&`)

Used to extract or check specific bits (masking).

```python
# Check if a number is odd or even
# The last bit of an odd number is always 1, and even is 0.
x = 5 # 101
print(x & 1) # 1 (Odd)

y = 4 # 100
print(y & 1) # 0 (Even)
```

### OR (`|`)

Used to set specific bits to 1.

```python
# Set the lowest bit to 1 (making an even number odd, leaving odd unchanged)
x = 4 # 100
print(x | 1) # 101 (5)
```

### XOR (`^`)

Exclusive OR. Extremely powerful for toggle operations and finding missing elements.

```python
# XORing a number with itself always results in 0.
print(5 ^ 5) # 0

# XORing a number with 0 leaves the number unchanged.
print(5 ^ 0) # 5
```

### Shift Operators (`<<`, `>>`)

Bit shifting is a hardware-level shortcut for multiplying or dividing by powers of 2.

```python
# Multiply by 2^3 (8)
x = 5
print(x << 3) # 40

# Divide by 2^1 (2)
y = 10
print(y >> 1) # 5
```

---

## Common Pitfalls

- **Operator Precedence:** Bitwise operators have *lower* precedence than arithmetic operators, but *higher* precedence than comparison operators. This leads to extremely common bugs.
  
  ```python
  x = 5
  # BAD: Evaluates to x & (1 == 1) -> x & True -> x & 1 -> 1
  if x & 1 == 1: 
      pass
      
  # GOOD: Always use parentheses around bitwise operations!
  if (x & 1) == 1:
      pass
  ```

---

## Key Takeaways

- Use `& 1` to check if a number is odd/even.
- Use `<<` to quickly multiply by powers of 2.
- Use `>>` to quickly divide by powers of 2.
- **Always use parentheses** when combining bitwise operations with `==`, `!=`, `<`, or `>`.

---

## Related Topics

- [XOR Tricks](04-xor-tricks.md)
- [Bit Masks](05-bit-masks.md)
