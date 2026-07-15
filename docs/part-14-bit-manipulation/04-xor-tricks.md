# XOR Tricks

> Exclusive OR (`^`) is the most heavily tested bitwise operator in technical interviews.

---

## Introduction

XOR is incredibly powerful because it is commutative, associative, and acts as its own inverse. This makes it the perfect tool for finding missing numbers or isolating unique elements in an array.

---

## The Core Properties of XOR

You must memorize these three fundamental properties to solve XOR interview questions:

1. **Identity:** XORing a number with 0 returns the number itself.
   - `x ^ 0 = x`
2. **Self-Inverse:** XORing a number with itself returns 0 (it cancels itself out).
   - `x ^ x = 0`
3. **Commutative & Associative:** The order of operations does not matter.
   - `a ^ b ^ a = (a ^ a) ^ b = 0 ^ b = b`

---

## DSA Example 1: Single Number

**Problem (LeetCode 136):** Given a non-empty array of integers `nums`, every element appears twice except for one. Find that single one. You must implement a solution with a linear runtime complexity and use only constant extra space.

**Naive Approach:** Use a HashSet to track seen numbers. Takes $O(N)$ space.
**Optimal Approach:** XOR all the numbers together. 

Because of the Self-Inverse and Commutative properties, every number that appears twice will cancel itself out to `0`. The only number left standing will be the one that appears once!

```python
def singleNumber(nums: list[int]) -> int:
    result = 0
    for num in nums:
        result ^= num
    return result

# Execution on [4, 1, 2, 1, 2]:
# result = 0 ^ 4 ^ 1 ^ 2 ^ 1 ^ 2
# result = 4 ^ (1 ^ 1) ^ (2 ^ 2)
# result = 4 ^ 0 ^ 0
# result = 4
```

| Time Complexity | Space Complexity |
|-----------------|------------------|
| $O(N)$ | $O(1)$ |

---

## DSA Example 2: Missing Number

**Problem (LeetCode 268):** Given an array `nums` containing `n` distinct numbers in the range `[0, n]`, return the only number in the range that is missing from the array.

**Optimal Approach:** We can use XOR to find the missing number. We XOR all the indices `[0..n]` and all the values in the array. Every number present will appear twice (once as an index, once as a value) and cancel out. The missing number will only appear once (as an index) and will be left in `result`.

```python
def missingNumber(nums: list[int]) -> int:
    n = len(nums)
    result = n # Start with n, since the loop only goes up to n-1
    
    for i in range(n):
        result ^= i
        result ^= nums[i]
        
    return result
```

*(Note: This can also be solved using Gauss's Math formula: `Sum(0..n) - Sum(nums)`, but the XOR approach prevents potential integer overflow in languages with fixed-size integers like Java/C++).*

---

## Two's Complement Trick (Isolating the rightmost 1-bit)

A very common sub-problem in bit manipulation is isolating the rightmost `1` bit of a number.

```python
rightmost_one = x & -x
```

**Why does this work?**
Because of Two's Complement representation, `-x` is exactly `(~x) + 1`. 
When you add 1 to `~x`, it flips all the trailing 1s back to 0s, and carries the 1 over to exactly where the rightmost 1-bit was in the original `x`. Thus, `x & -x` leaves only that single bit as a `1`.

*This trick is heavily used in advanced data structures like the Fenwick Tree (Binary Indexed Tree).*

---

## Common Interview Questions

- Single Number (LeetCode 136)
- Missing Number (LeetCode 268)
- Single Number III (LeetCode 260) - *Requires isolating the rightmost 1-bit!*

---

## Key Takeaways

- `x ^ x = 0` (Pairs cancel out).
- `x ^ 0 = x`.
- Use XOR to find a single unique element among pairs in $O(1)$ space.
- Use `x & -x` to isolate the rightmost 1-bit.

---

## Related Topics

- [Bitwise Operators](03-bitwise-operators.md)
- [Bit Masks](05-bit-masks.md)
