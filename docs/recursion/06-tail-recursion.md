# Tail Recursion

> A specific form of recursion where the recursive call is the very last operation in the function.

---

## Introduction

In many programming languages (like C++, Java, or functional languages like Haskell), tail recursion is a highly sought-after optimization. Interviewers with backgrounds in these languages might ask if your recursive solution can be converted to a "tail-recursive" one.

However, if you are interviewing in Python, you must know a critical detail: **Python does NOT support Tail Call Optimization (TCO).**

---

## What is Tail Recursion?

A function is tail-recursive if the recursive call is the absolute final action executed before returning. There can be no computation performed *after* the recursive call returns.

### Non-Tail Recursive (Standard)

```python
def factorial(n: int) -> int:
    if n <= 1:
        return 1
    # NOT tail recursive. 
    # The multiplication (n * result) happens AFTER the recursive call returns.
    return n * factorial(n - 1) 
```

### Tail Recursive

To make this tail recursive, we must pass the accumulated result as an argument to the recursive call, so there is no work left to do when the function returns.

```python
def tail_factorial(n: int, accumulator: int = 1) -> int:
    if n <= 1:
        return accumulator
    # TAIL recursive. 
    # The recursive call is the absolute last step. No further work is done.
    return tail_factorial(n - 1, n * accumulator)
```

---

## Tail Call Optimization (TCO)

In languages that support TCO, the compiler recognizes that the current stack frame is no longer needed (because no work happens after the recursive call). Instead of pushing a new frame onto the Call Stack, the compiler simply reuses the current frame.

This effectively turns the space complexity of a tail-recursive function from $O(N)$ into $O(1)$! It acts exactly like an iterative `while` loop under the hood.

---

## Python and TCO

**Python deliberately does not implement Tail Call Optimization.**

Guido van Rossum (the creator of Python) rejected TCO for a few reasons:
1. It ruins stack traces for debugging (frames are overwritten, so you lose the history of how an error occurred).
2. It encourages writing recursive code in scenarios where a simple `while` or `for` loop would be more "Pythonic".

### Why this matters in interviews

If an interviewer asks: *"Your recursion uses $O(N)$ space. Can we optimize this to $O(1)$ using tail recursion?"*

Your answer should be:
*"In languages like C++, we could use tail recursion to achieve $O(1)$ space. However, Python does not support Tail Call Optimization. To achieve $O(1)$ space in Python, we must rewrite this algorithm iteratively using a `while` loop."*

This demonstrates deep domain knowledge of both general computer science concepts and Python-specific internals.

---

## Key Takeaways

- Tail recursion occurs when the recursive call is the last executed statement.
- Languages with TCO can run tail-recursive functions in $O(1)$ space.
- Python **does not** support TCO.
- To achieve $O(1)$ space in Python, you must use an iterative loop.

---

## Related Topics

- [Recursion vs Iteration](07-recursion-vs-iteration.md)
- [Call Stack](05-call-stack.md)
