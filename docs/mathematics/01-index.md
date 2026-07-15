# Mathematics

## Introduction

Mathematics is not heavily tested in typical software engineering interviews, but there are a few core concepts that occasionally appear (especially in quantitative finance firms or specific LeetCode problems).

You do not need an advanced degree in Math to pass coding interviews, but you should be familiar with a few fundamental algorithms.

---

## What you need to know

The mathematics expected in interviews usually revolves around:
1. **Number Theory:** Prime numbers, Greatest Common Divisor (GCD), Least Common Multiple (LCM).
2. **Modular Arithmetic:** Preventing integer overflow (in languages other than Python) or dealing with circular arrays.
3. **Combinatorics:** Permutations, Combinations, and calculating probabilities.

---

## The Good News About Python

Python is arguably the best language for math-heavy interview questions because:
- **Infinite Precision:** Python handles massive integers seamlessly without throwing overflow errors. You never have to worry about `int` vs `long` or manually implementing string multiplication just because a number exceeds $2^{31}-1$.
- **The `math` module:** The standard library contains optimized, C-level implementations for almost everything you need, including `math.gcd()`, `math.lcm()`, `math.comb()`, and `math.factorial()`.

---

## Related Topics

- [GCD and LCM](02-gcd-and-lcm.md)
- [Prime Numbers](03-prime-numbers.md)
- [Modular Arithmetic](05-modular-arithmetic.md)
- [Math Built-ins](../standard-library/06-math.md)
