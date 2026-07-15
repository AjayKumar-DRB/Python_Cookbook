# Bit Manipulation

## Introduction

Bit manipulation is a niche but critical topic in technical interviews. It involves interacting directly with the binary representations of numbers.

While it is rarely the core focus of an entire system design or everyday application development, FAANG interviews love bit manipulation because it tests your fundamental understanding of computer architecture, data representation, and micro-optimizations.

---

## Why Learn Bit Manipulation?

1. **Extreme Performance:** Bitwise operations execute at the hardware level in a single CPU cycle, making them drastically faster than arithmetic operations like multiplication, division, or modulo.
2. **Memory Efficiency:** A single 32-bit integer can store 32 independent boolean flags.
3. **Algorithmic Shortcuts:** Certain problems (like finding a single missing number in an array) have $O(N)$ time, $O(1)$ space solutions using bit manipulation that are impossible to achieve otherwise.

---

## Key Takeaways

- You must understand the fundamental bitwise operators: `&`, `|`, `^`, `~`, `<<`, and `>>`.
- Python handles integers differently than C++ or Java. Python integers have arbitrary precision (they can grow infinitely), which means they don't have a fixed 32-bit or 64-bit boundary. This makes negative numbers tricky.
- Memorize a few "Bit Hacks" (like checking if a number is a power of 2 or isolating the rightmost 1-bit).

---

## Related Topics

- [Binary Numbers](02-binary-numbers.md)
- [Bitwise Operators](03-bitwise-operators.md)
- [XOR Tricks](04-xor-tricks.md)
