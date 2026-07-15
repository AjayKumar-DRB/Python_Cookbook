# Subsets Using Bits

> Generating all possible subsets without using recursion or backtracking!

---

## Introduction

In the Recursion module, we learned how to generate all subsets of an array using Backtracking.

However, there is an incredibly elegant, non-recursive way to generate subsets using Bit Masks. This method is often cleaner to write and avoids recursion limit overhead.

---

## The Concept

An array of length $N$ has exactly $2^N$ possible subsets.

If $N = 3$, there are $2^3 = 8$ subsets.
Let's count from 0 to 7 in binary:

```
0: 000 (Empty Subset)
1: 001 (Include only nums[0])
2: 010 (Include only nums[1])
3: 011 (Include nums[1], nums[0])
4: 100 (Include only nums[2])
5: 101 (Include nums[2], nums[0])
6: 110 (Include nums[2], nums[1])
7: 111 (Include nums[2], nums[1], nums[0])
```

Notice a pattern? The binary representation of every number from $0$ to $2^N - 1$ PERFECTLY maps to exactly one subset combination! 
A `1` means "include this element", and a `0` means "exclude this element".

---

## Implementation

We can loop from $0$ to $2^N - 1$. For each number (mask), we check which bits are set to `1` and include the corresponding elements from the array.

```python
def subsets(nums: list[int]) -> list[list[int]]:
    n = len(nums)
    res = []
    
    # 1 << n is exactly 2^n
    for mask in range(1 << n):
        current_subset = []
        
        # Check every bit position from 0 to n-1
        for i in range(n):
            # If the i-th bit is set to 1, include nums[i]
            if mask & (1 << i):
                current_subset.append(nums[i])
                
        res.append(current_subset)
        
    return res
```

| Time Complexity | Space Complexity |
|-----------------|------------------|
| $O(N \cdot 2^N)$ | $O(N \cdot 2^N)$ |

The time complexity is identical to Backtracking ($2^N$ subsets, and copying a subset takes $O(N)$). 

---

## Why use this over Backtracking?

- **Pros:** It's entirely iterative, meaning no Call Stack overhead and no risk of hitting a Recursion Limit. It's also slightly easier to reason about if you are comfortable with bitmasks.
- **Cons:** It only works for up to $\approx 31$ elements (though in Python, integers have infinite precision, so you could technically do more, but a $2^{31}$ loop would take minutes to run anyway). Backtracking is often easier to adapt to complex rules (like filtering out duplicates).

---

## Key Takeaways

- The numbers $0$ to $2^N - 1$ in binary directly represent all possible subsets of an array of size $N$.
- Use `1 << N` to calculate $2^N$.
- Use `mask & (1 << i)` to check if the $i$-th element should be included.

---

## Related Topics

- [Bit Masks](05-bit-masks.md)
- [Backtracking vs Recursion](../part-13-recursion/08-backtracking-vs-recursion.md)
