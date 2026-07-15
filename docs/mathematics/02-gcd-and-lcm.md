# GCD and LCM

> Greatest Common Divisor and Least Common Multiple.

---

## Introduction

The Greatest Common Divisor (GCD) of two integers is the largest positive integer that perfectly divides both numbers without a remainder.

The Least Common Multiple (LCM) is the smallest positive integer that is perfectly divisible by both numbers.

---

## Finding GCD (Euclidean Algorithm)

While you could iterate down from the smaller number until you find a divisor, that would take $O(\min(A, B))$ time. The **Euclidean Algorithm** finds the GCD in $O(\log(\min(A, B)))$ time.

The Euclidean Algorithm states:
$GCD(A, B) = GCD(B, A \% B)$

### Recursive Implementation
```python
def gcd(a: int, b: int) -> int:
    if b == 0:
        return a
    return gcd(b, a % b)
```

### Iterative Implementation
```python
def gcd_iterative(a: int, b: int) -> int:
    while b:
        a, b = b, a % b
    return a
```

---

## Finding LCM

Once you have the GCD, calculating the LCM is incredibly simple using this mathematical formula:

$LCM(A, B) = \frac{A \times B}{GCD(A, B)}$

```python
def lcm(a: int, b: int) -> int:
    return (a * b) // gcd(a, b)
```

---

## Python's Built-in Methods

You almost never have to implement these manually in an interview unless the interviewer explicitly asks you to write the Euclidean Algorithm from scratch.

Python's standard library `math` module provides highly optimized C implementations for both.

```python
import math

# Python 3.5+
print(math.gcd(12, 18)) # 6

# Python 3.9+
print(math.lcm(12, 18)) # 36
```

---

## Common Interview Questions

- **Water Jug Problem (LeetCode 365):** Can be solved instantly if you realize it's a math problem: you can measure $Z$ liters if $Z$ is a multiple of $GCD(X, Y)$.
- **Fraction Addition and Subtraction (LeetCode 592):** Requires finding the LCM of the denominators.

---

## Key Takeaways

- Know the `a, b = b, a % b` iterative loop for GCD in case you are asked to implement it manually.
- Know the formula $LCM = (A \times B) / GCD$.
- In a real interview, import and use `math.gcd()` and `math.lcm()` unless instructed otherwise.

---

## Related Topics

- [Math Module](../standard-library/06-math.md)
