# Recursion

## Introduction

Recursion is one of the most fundamental concepts in computer science and technical interviews. It is the foundation for advanced algorithms like Depth-First Search (DFS), Backtracking, and Dynamic Programming.

Mastering recursion is often the biggest hurdle for candidates, but once it clicks, many complex tree and graph problems become trivial to solve.

---

## What is it?

Recursion occurs when a function calls itself to solve a smaller instance of the same problem. 

Instead of solving the entire problem at once using a loop (iteration), a recursive function breaks the problem down, solves the subproblem, and combines the results.

---

## Key Takeaways

- **Think Top-Down:** Assume the recursive call *just works* for the smaller problem. Do not mentally trace every recursive step; it will overwhelm you.
- **Always Start with the Base Case:** A recursive function without a base case is an infinite loop (which throws a `RecursionError` in Python).
- **Recursion uses the Call Stack:** Every recursive call consumes memory. Space complexity is $O(H)$, where $H$ is the maximum depth of the recursive tree.

---

## Related Topics

- [Recursion Basics](02-recursion-basics.md)
- [Call Stack](05-call-stack.md)
- [Backtracking vs Recursion](08-backtracking-vs-recursion.md)
- [Trees](../algorithmic-patterns/14-trees.md)
- [Dynamic Programming](../algorithmic-patterns/21-dynamic-programming.md)
