# Mathematics Interview Recipes

> A quick-reference guide to standard math algorithms.

---

## 1. Fast Prime Checking

Check if a single number is prime in $O(\sqrt{N})$ time.

```python
import math

def is_prime(n: int) -> bool:
    if n <= 1: return False
    for i in range(2, int(math.sqrt(n)) + 1):
        if n % i == 0:
            return False
    return True
```

---

## 2. Sieve of Eratosthenes

Generate all primes less than $N$ in $O(N \log \log N)$ time.

```python
def get_primes(n: int) -> list[int]:
    if n <= 2: return []
    is_prime = [True] * n
    is_prime[0] = is_prime[1] = False
    
    for i in range(2, int(n ** 0.5) + 1):
        if is_prime[i]:
            for multiple in range(i * i, n, i):
                is_prime[multiple] = False
                
    return [i for i, prime in enumerate(is_prime) if prime]
```

---

## 3. Fast Exponentiation (Iterative)

Calculate $x^n$ in $O(\log n)$ time. (If the interviewer doesn't let you use the built-in `pow()`).

```python
def myPow(x: float, n: int) -> float:
    if n < 0:
        x = 1 / x
        n = -n
        
    res = 1.0
    while n > 0:
        if n % 2 == 1:
            res *= x
        x *= x
        n //= 2
    return res
```

---

## 4. Fisher-Yates Shuffle

Shuffle an array uniformly in $O(N)$ time.

```python
import random

def shuffle(nums: list[int]):
    for i in range(len(nums) - 1, 0, -1):
        j = random.randint(0, i)
        nums[i], nums[j] = nums[j], nums[i]
```

---

## 5. Reservoir Sampling

Pick a random item from a linked list / stream uniformly in $O(N)$ time and $O(1)$ space.

```python
import random

def get_random(head):
    chosen = head.val
    curr = head.next
    i = 2
    while curr:
        if random.randint(1, i) == 1:
            chosen = curr.val
        curr = curr.next
        i += 1
    return chosen
```

---

## Key Takeaways

- Import the `math` module heavily (`math.gcd`, `math.lcm`, `math.comb`).
- Be careful with `0` and `1` not being prime numbers.
- Always use `// 2` or `int(math.sqrt())` to avoid precision issues with floats.
