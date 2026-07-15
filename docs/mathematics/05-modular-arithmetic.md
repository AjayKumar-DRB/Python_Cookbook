# Modular Arithmetic

> Dealing with wrap-around arrays and preventing integer overflow.

---

## Introduction

Modular arithmetic (using the modulo operator `%`) is the math of remainders. It acts like a clock: when you pass 12, you wrap back around to 1. 

In coding interviews, the modulo operator is heavily used in two specific scenarios:
1. Accessing arrays circularly (wrap-around).
2. Preventing numbers from growing too large (often required in Competitive Programming / LeetCode Hard math problems, where the answer must be returned `modulo 10^9 + 7`).

---

## 1. Circular Arrays (Wrap-Around)

If you are at index `i` in an array of length `N`, and you want to move forward `k` steps, you might fall out of bounds (`i + k >= N`).

To safely wrap around to the beginning of the array, use the modulo operator:
```python
new_index = (i + k) % N
```

**What about moving backwards?**
In Python, the modulo operator handles negative numbers gracefully.
`-1 % 5 == 4` (Python wraps correctly to the end).
In C++ or Java, `-1 % 5` is `-1`, which causes an `IndexOutOfBounds` error. 

If you are coding in Python, `(i - k) % N` works perfectly. If you want a language-agnostic approach, use:
```python
new_index = (i - k + N) % N
```

---

## 2. Modulo Arithmetic Rules

When a problem tells you to "Return the answer modulo $10^9 + 7$", it's because the final answer is too large to fit in a 32-bit integer, and the authors want to test your knowledge of modular properties.

*(Note: In Python, integers have infinite precision, so you don't actually get integer overflows. However, computing extremely large numbers like $2^{10000}$ takes significant time and memory. Therefore, applying the modulo at every step is still required to keep the numbers small and fast).*

You must know these algebraic properties:

1. **Addition:** `(a + b) % M = ((a % M) + (b % M)) % M`
2. **Multiplication:** `(a * b) % M = ((a % M) * (b % M)) % M`

**Example:**
If we are computing $5!$ modulo $7$:
```python
MOD = 7
res = 1
for i in range(1, 6):
    # Apply modulo at EVERY step to keep 'res' small!
    res = (res * i) % MOD 
```

---

## What about Division? (Modular Inverse)

You CANNOT do `(a / b) % M = ((a % M) / (b % M)) % M`. This is mathematically invalid!

To divide under a modulo, you must multiply by the **Modular Multiplicative Inverse**. 
If the modulo $M$ is a prime number (like $10^9 + 7$), you can use Fermat's Little Theorem:

$a^{-1} \equiv a^{M-2} \pmod M$

In Python, the built-in `pow()` function calculates this instantly:
```python
# Instead of doing (a / b) % M
# You do: (a * modular_inverse(b)) % M
inverse_b = pow(b, M - 2, M)
result = (a * inverse_b) % M
```

*(Note: Python 3.8+ introduced an even simpler way. You can directly pass a negative power if you provide the modulo!)*
```python
# Python 3.8+ only
inverse_b = pow(b, -1, M) 
```

---

## Key Takeaways

- Use `(i + k) % len` to traverse arrays circularly.
- Python handles negative modulo natively (`-1 % 5 == 4`).
- If an answer must be returned modulo $M$, apply `% M` at *every* addition or multiplication step to prevent the integer from growing huge and slowing down the script.
- Never divide under a modulo. Use `pow(b, -1, M)` to find the inverse and multiply instead.
