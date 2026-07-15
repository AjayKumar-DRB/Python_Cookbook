# Counting Bits

> Finding the "Hamming Weight" of a binary number.

---

## Introduction

Counting the number of `1` bits in an integer (also known as the "Hamming Weight") is a classic interview question (LeetCode 191: Number of 1 Bits). 

While you can technically solve this by converting the integer to a binary string and counting the `'1'` characters, interviewers expect a pure bit manipulation approach.

---

## Approach 1: Bit Shifting (The Naive Way)

We can check if the rightmost bit is a `1` by ANDing the number with `1`. Then, we shift the number to the right by 1 bit (`>> 1`) and repeat until the number becomes `0`.

```python
def hammingWeight(n: int) -> int:
    count = 0
    while n:
        count += n & 1
        n = n >> 1
    return count
```

| Time Complexity | Space Complexity |
|-----------------|------------------|
| $O(32)$ or $O(1)$ | $O(1)$ |

This loop runs exactly 32 times (in a 32-bit integer system) in the worst case, because we must shift past all leading zeros.

---

## Approach 2: Brian Kernighan's Algorithm (The Optimal Way)

Instead of iterating through every single bit, what if we only iterated *for as many `1` bits as there are in the number?*

As we learned in the [Powers of Two](06-checking-powers-of-two.md) lesson, `n & (n - 1)` perfectly erases the rightmost `1` bit of a number!

If we repeatedly apply `n = n & (n - 1)` inside a loop, the number of times the loop runs will be exactly equal to the number of `1` bits. 

```python
def hammingWeight_optimal(n: int) -> int:
    count = 0
    while n:
        n &= (n - 1) # Erase the rightmost 1-bit
        count += 1
    return count
```

| Time Complexity | Space Complexity |
|-----------------|------------------|
| $O(K)$ | $O(1)$ |

Where $K$ is the number of `1` bits. If a 32-bit number is `100...000` (only a single 1 bit), this loop runs exactly 1 time, whereas Approach 1 would run 32 times.

---

## Built-in Python Alternative

In production code, you should never write your own bit-counting function. Python integers have a highly optimized built-in method:

```python
count = (5).bit_count() # Available in Python 3.10+
print(count) # 2 (since 5 is 101)
```

**Interview Tip:** Always mention `bit_count()` to the interviewer to show you know modern Python, but immediately offer to write Brian Kernighan's algorithm to prove you understand the low-level logic.

---

## Key Takeaways

- Checking bits iteratively by shifting right (`>> 1`) takes $O(32)$ time.
- Brian Kernighan's Algorithm `n &= (n - 1)` takes $O(K)$ time, where $K$ is the number of set bits.
- Mention `int.bit_count()` in Python 3.10+.

---

## Related Topics

- [Checking Powers of Two](06-checking-powers-of-two.md)
- [Bitwise Operators](03-bitwise-operators.md)
