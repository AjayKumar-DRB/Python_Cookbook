# Checking Powers of Two

> An ultra-fast bitwise trick to check if $x == 2^N$.

---

## Introduction

In an interview, you might be asked to verify if a given integer is a power of 2 (e.g., 1, 2, 4, 8, 16). 

The naive iterative approach involves dividing the number by 2 repeatedly until you reach 1, which takes $O(\log N)$ time. By using bit manipulation, we can accomplish this in strictly $O(1)$ time.

---

## The Trick

A number is a power of 2 if and only if it has **exactly one bit set to `1`** in its binary representation.

- $2^0 = 1$  (Binary: `0001`)
- $2^1 = 2$  (Binary: `0010`)
- $2^2 = 4$  (Binary: `0100`)
- $2^3 = 8$  (Binary: `1000`)

Notice what happens if we subtract `1` from a power of 2. It flips the highest `1` bit to `0`, and turns all the trailing `0`s into `1`s.

- $8 = 1000$
- $7 = 0111$

If we apply the Bitwise AND (`&`) operator between $x$ and $x - 1$, the result will ALWAYS be exactly `0` if $x$ is a power of 2!

```python
1000  (8)
0111  (7)
----  AND
0000  (0)
```

---

## Implementation

```python
def isPowerOfTwo(n: int) -> bool:
    # 0 and negative numbers cannot be powers of 2.
    if n <= 0:
        return False
        
    return (n & (n - 1)) == 0
```

| Time Complexity | Space Complexity |
|-----------------|------------------|
| $O(1)$ | $O(1)$ |

---

## Removing the Lowest Set Bit (Brian Kernighan's Algorithm)

The core mechanic of this trick (`n & (n - 1)`) does not just apply to powers of 2. 

**`n = n & (n - 1)` will always erase the rightmost `1` bit from `n`.**

If the number only had one `1` bit to begin with (a power of 2), erasing it leaves `0`. If the number had multiple `1` bits, erasing the rightmost one leaves the remaining bits intact.

This property is the foundation of Brian Kernighan's algorithm for counting bits, which we will cover next!

---

## Common Pitfalls

- **Forgetting `n <= 0`:** In Python, negative numbers have infinite precision, and `0` has no `1` bits. `0 & (0 - 1)` is `0`, so if you forget the `n <= 0` check, your function will incorrectly return `True` for `0`!
- **Operator Precedence:** Always wrap `(n & (n - 1))` in parentheses before comparing it to `== 0`.

---

## Key Takeaways

- A power of 2 has exactly one `1` bit.
- `n & (n - 1)` completely erases the rightmost `1` bit.
- If `(n & (n - 1)) == 0` (and `n > 0`), the number is a power of 2.

---

## Related Topics

- [Counting Bits](07-counting-bits.md)
- [Bitwise Operators](03-bitwise-operators.md)
