# Bit Manipulation Interview Recipes

> A quick-reference guide to the standard bit manipulation techniques you need to memorize.

---

## 1. Finding a Single Missing / Unique Element

If you need to find an element that appears an odd number of times (usually once) in an array where all other elements appear an even number of times (usually twice).

```python
def singleNumber(nums: list[int]) -> int:
    res = 0
    for num in nums:
        res ^= num
    return res
```

---

## 2. Brian Kernighan's Algorithm (Counting or Removing 1s)

If you need to count the number of `1` bits, or check if a number is a power of 2, always use `n & (n - 1)`.

```python
# Check if power of 2
def isPowerOfTwo(n: int) -> bool:
    return n > 0 and (n & (n - 1)) == 0

# Count set bits
def hammingWeight(n: int) -> int:
    count = 0
    while n:
        n &= (n - 1)
        count += 1
    return count
```

---

## 3. Masking (Getting, Setting, Clearing Bits)

If you are using an integer as a DP state or tracking seen elements.

```python
# SET the i-th bit to 1
mask = mask | (1 << i)

# CLEAR the i-th bit to 0
mask = mask & ~(1 << i)

# CHECK if the i-th bit is 1
if mask & (1 << i):
    pass

# TOGGLE the i-th bit
mask = mask ^ (1 << i)
```

---

## 4. Subsets Generation via Bitmasks

If you need to generate all subsets (Power Set) iteratively.

```python
def subsets(nums: list[int]) -> list[list[int]]:
    res = []
    n = len(nums)
    
    for mask in range(1 << n):
        subset = [nums[i] for i in range(n) if mask & (1 << i)]
        res.append(subset)
        
    return res
```

---

## 5. Isolating the Rightmost 1-bit

Used in advanced algorithms like Fenwick Trees, or finding two missing numbers in an array.

```python
rightmost_one = n & -n
```

---

## Key Takeaways

- Most bit manipulation questions on LeetCode can be solved with these exact 5 templates.
- If you see a problem with extreme memory constraints (e.g. $O(1)$ space required to track states), think of Bit Masks.
- If you see a problem asking to find a single unique number, think of XOR.
