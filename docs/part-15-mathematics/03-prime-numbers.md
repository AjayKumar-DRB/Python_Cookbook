# Prime Numbers

> Numbers greater than 1 that have no divisors other than 1 and themselves.

---

## Introduction

Checking if a number is prime, or finding all prime factors of a number, is a classic math problem. 

The naive way to check if $N$ is prime is to loop from $2$ up to $N - 1$ and check if $N \% i == 0$. However, this is too slow ($O(N)$). You must know the optimized $O(\sqrt{N})$ approach.

---

## Primality Test (Checking if a number is prime)

If a number $N$ is not prime, it can be factored into two numbers $a$ and $b$ (where $N = a \times b$).
If both $a$ and $b$ were greater than $\sqrt{N}$, then $a \times b$ would be greater than $N$, which is impossible.
Therefore, at least one of the factors must be less than or equal to $\sqrt{N}$.

Because of this mathematical fact, **we only need to check for divisors up to $\sqrt{N}$**.

```python
import math

def is_prime(n: int) -> bool:
    if n <= 1:
        return False
        
    # We only check up to the square root of n!
    limit = int(math.sqrt(n))
    for i in range(2, limit + 1):
        if n % i == 0:
            return False
            
    return True
```

| Time Complexity | Space Complexity |
|-----------------|------------------|
| $O(\sqrt{N})$ | $O(1)$ |

---

## Finding Prime Factors

Sometimes a problem requires you to break a number down into its prime components.
For example, the prime factors of $12$ are $[2, 2, 3]$ (since $2 \times 2 \times 3 = 12$).

We use a similar $\sqrt{N}$ approach. We divide by $2$ as many times as possible, then check all odd numbers up to $\sqrt{N}$.

```python
import math

def prime_factors(n: int) -> list[int]:
    factors = []
    
    # 1. Divide out all 2s
    while n % 2 == 0:
        factors.append(2)
        n //= 2
        
    # 2. Check odd numbers up to sqrt(n)
    limit = int(math.sqrt(n))
    for i in range(3, limit + 1, 2):
        while n % i == 0:
            factors.append(i)
            n //= i
            
    # 3. If n is still > 2, it is a prime number itself!
    if n > 2:
        factors.append(n)
        
    return factors
```

---

## Key Takeaways

- To check if a number is prime, loop up to `int(math.sqrt(n))`.
- The time complexity for a primality test is $O(\sqrt{N})$.
- `1` is NOT a prime number. `2` is the only even prime number.

---

## Related Topics

- [Sieve of Eratosthenes](04-sieve-of-eratosthenes.md)
