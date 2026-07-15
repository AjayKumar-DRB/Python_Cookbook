# Combinatorics

> The math of counting.

---

## Introduction

Combinatorics deals with counting permutations and combinations. In technical interviews, combinatorial math often appears in:
1. Calculating the total time complexity of a Backtracking algorithm.
2. Directly returning the *number* of ways to do something (without having to generate the actual lists).

---

## Permutations (Order Matters)

A permutation is an arrangement of items where the **order matters**. (e.g., `[1, 2, 3]` is different from `[3, 2, 1]`).

The number of ways to arrange $N$ unique items is $N!$ (N factorial).

If you are choosing $K$ items from a pool of $N$ items, the formula is:
$P(n, k) = \frac{n!}{(n - k)!}$

**Python Standard Library:**
Python 3.8+ introduced a built-in method for this.
```python
import math

print(math.perm(5, 3)) # 60 ways to arrange 3 items out of 5
```

---

## Combinations (Order Does NOT Matter)

A combination is a selection of items where the **order does not matter**. (e.g., a hand of cards, where `[Ace, King]` is exactly the same as `[King, Ace]`).

This is often referred to as "N choose K" or $\binom{n}{k}$.

The formula is:
$C(n, k) = \frac{n!}{k!(n - k)!}$

**Python Standard Library:**
Python 3.8+ introduced a built-in method for this.
```python
import math

print(math.comb(5, 3)) # 10 ways to choose 3 items out of 5
```

---

## The Stars and Bars Theorem

A niche but highly useful combinatorial trick for problems like "How many ways can I distribute $N$ identical candies to $K$ distinct children?"

The formula is:
$\binom{n + k - 1}{k - 1}$

Using Python:
```python
import math

# Distribute 5 candies to 3 children
ans = math.comb(5 + 3 - 1, 3 - 1)
print(ans) # 21
```

---

## Subsets (The Power Set)

How many possible subsets can be generated from an array of $N$ unique items?

For every item, you have exactly 2 choices: Include it, or don't include it.
Therefore, the total number of subsets is exactly $2^N$.

This is why the time complexity for generating a Power Set using Backtracking is always $O(N \cdot 2^N)$ (the $N$ multiplier comes from copying the subset array into the result list).

---

## Key Takeaways

- Use `math.perm(n, k)` when order matters (e.g., passwords, scheduling).
- Use `math.comb(n, k)` when order does NOT matter (e.g., teams, subsets of exact size).
- The total number of subsets of an array is $2^N$.
- The total number of permutations of an array is $N!$.

---

## Related Topics

- [Math Module](../standard-library/06-math.md)
- [Backtracking Pattern](../algorithmic-patterns/23-backtracking.md)
