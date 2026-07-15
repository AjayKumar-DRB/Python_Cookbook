# Sieve of Eratosthenes

> Finding all prime numbers up to $N$ incredibly fast.

---

## Introduction

If you need to check if a *single* number is prime, you use the $O(\sqrt{N})$ `is_prime()` function. 

However, if an interview problem asks you to find or count *all* prime numbers strictly less than $N$ (LeetCode 204: Count Primes), calling `is_prime()` in a loop will take $O(N \sqrt{N})$ time, which results in a Time Limit Exceeded (TLE) error.

To generate a list of primes efficiently, you must use the **Sieve of Eratosthenes**.

---

## The Concept

The Sieve of Eratosthenes works by elimination. 

1. Create a boolean array `is_prime` of size $N+1$, initially all `True`.
2. Mark `0` and `1` as `False` (since they aren't prime).
3. Start iterating from `2` up to $\sqrt{N}$.
4. If a number $P$ is marked as `True`, it is a prime! 
5. Cross off (mark as `False`) all multiples of $P$ starting from $P^2$ (i.e. $P^2$, $P^2+P$, $P^2+2P$, etc.).

Why start crossing off from $P^2$? Because any smaller multiple of $P$ (like $P \times 2$ or $P \times 3$) would have already been crossed off when we processed the smaller prime factors $2$ and $3$.

---

## Implementation

```python
import math

def countPrimes(n: int) -> int:
    # If n is 0 or 1, there are no strictly smaller primes.
    if n <= 2:
        return 0
        
    is_prime = [True] * n
    is_prime[0] = is_prime[1] = False
    
    # We only need to check up to sqrt(n)
    limit = int(math.sqrt(n))
    for i in range(2, limit + 1):
        if is_prime[i]:
            # Cross off all multiples starting from i^2
            for multiple in range(i * i, n, i):
                is_prime[multiple] = False
                
    return sum(is_prime)
```

| Time Complexity | Space Complexity |
|-----------------|------------------|
| $O(N \log(\log N))$ | $O(N)$ |

The time complexity $O(N \log(\log N))$ is effectively $O(N)$ for any realistic integer size. It is much, much faster than $O(N \sqrt{N})$.

---

## Common Pitfalls

- **Looping to `n` instead of `sqrt(n)`:** The outer loop only needs to go up to $\sqrt{N}$. If you loop all the way to $N$, the algorithm will still work but will be significantly slower.
- **Starting the inner loop at `i * 2`:** Starting the multiple crossing at `i * i` is a crucial optimization.

---

## Key Takeaways

- Use `is_prime(n)` for a single number ($O(\sqrt{N})$).
- Use the **Sieve of Eratosthenes** for a range of numbers ($O(N \log \log N)$).
- Start marking multiples at `i * i`.

---

## Related Topics

- [Prime Numbers](03-prime-numbers.md)
