# Fast Exponentiation

> Calculating $x^n$ in $O(\log n)$ time.

---

## Introduction

If an interview problem asks you to calculate $x^n$ (e.g. LeetCode 50: `Pow(x, n)`), the naive approach is to multiply $x$ by itself $n$ times using a `for` loop.

This takes $O(N)$ time, which will result in a Time Limit Exceeded error if $N$ is something huge like $2^{31} - 1$. 

We must use **Fast Exponentiation** (also known as Exponentiation by Squaring) to compute this in $O(\log N)$ time.

---

## The Concept

Notice that $2^{10}$ can be broken down:
$2^{10} = (2^5)^2$
$2^5 = 2 \times (2^2)^2$
$2^2 = (2^1)^2$
$2^1 = 2 \times (2^0)^2$

This recursive property means we can cut the power $N$ in half at every step!
- If $n$ is EVEN: $x^n = (x^{n/2})^2 = (x^2)^{n/2}$
- If $n$ is ODD: $x^n = x \times x^{n-1}$

By doing this, computing $x^{1000}$ takes roughly 10 steps instead of 1000 steps.

---

## Implementation (Iterative)

The iterative approach is widely considered the best because it avoids any recursive call stack overhead ($O(1)$ space).

```python
def myPow(x: float, n: int) -> float:
    # Handle negative powers: x^-n is (1/x)^n
    if n < 0:
        x = 1 / x
        n = -n
        
    res = 1.0
    while n > 0:
        if n % 2 == 1:
            # If odd, multiply current result by x
            res *= x
        # Square the base
        x *= x
        # Divide the power by 2
        n //= 2
        
    return res
```

| Time Complexity | Space Complexity |
|-----------------|------------------|
| $O(\log N)$ | $O(1)$ |

---

## Python's Built-in Power

In the real world, you would never write this yourself. Python has an incredibly powerful built-in `pow()` function that uses this exact C-level optimized logic under the hood.

```python
# Computes x^n
ans = pow(x, n)

# Computes (x^n) % M efficiently (Modular Fast Exponentiation)
ans = pow(x, n, M) 
```

**Interview Tip:** If the problem is literally "Implement Pow(x, n)", you must write the $O(\log N)$ algorithm out manually. If exponentiation is just a small step in a larger problem, simply use the built-in `pow(x, n)`.

---

## Key Takeaways

- Fast Exponentiation computes powers in $O(\log N)$ time instead of $O(N)$.
- It works by squaring the base and halving the exponent.
- Negative exponents are solved by inverting the base `x = 1 / x` and making the exponent positive `n = -n`.

---

## Related Topics

- [Modular Arithmetic](05-modular-arithmetic.md)
