# Recursion vs Iteration

> The debate between function calls and loops.

---

## Introduction

Anything that can be solved recursively can also be solved iteratively (and vice versa). During an interview, choosing which approach to use often dictates how easily you will solve the problem.

---

## The Core Difference

- **Iteration** uses loops (`for` or `while`) and explicit data structures (like a `list` acting as a stack or queue) to repeat actions.
- **Recursion** uses function calls to repeat actions, relying implicitly on the operating system's Call Stack to maintain state.

---

## Time and Space Complexity

| Approach | Time Complexity | Space Complexity |
|----------|-----------------|------------------|
| **Recursion** | Often the same as iteration. | $O(N)$ due to the Call Stack overhead. |
| **Iteration** | Often the same as recursion. | $O(1)$ if no manual stack/queue is used. |

Because Python does not support Tail Call Optimization, recursive solutions are almost always inherently worse in space complexity than their iterative equivalents. They also carry a slight performance penalty due to the overhead of pushing and popping stack frames.

---

## When to use Recursion

Despite the space and performance overhead, recursion is heavily preferred for problems involving non-linear data structures or branching logic. The recursive code is often drastically shorter, more readable, and easier to reason about.

**Use Recursion for:**
- Tree Traversals (DFS, Preorder, Inorder, Postorder)
- Graph Traversals (DFS)
- Backtracking (Permutations, Combinations, Sudoku Solver)
- Divide and Conquer Algorithms (Merge Sort, Quick Sort)
- Dynamic Programming (Top-Down Memoization)

**Example: Inorder Tree Traversal**
```python
# Recursive - 4 lines of clean code
def inorder(root):
    if not root: return
    inorder(root.left)
    print(root.val)
    inorder(root.right)
```

---

## When to use Iteration

Iteration should be your default choice for linear data structures. If a problem is easily solved with a simple `while` loop, forcing recursion will look like a "code smell" to an interviewer.

**Use Iteration for:**
- Array and String manipulation (Two Pointers, Sliding Window)
- Linked List traversal (Reversing a Linked List is better done iteratively)
- Breadth-First Search (BFS MUST be done iteratively using a Queue)
- Dynamic Programming (Bottom-Up Tabulation)

**Example: Linked List Traversal**
```python
# Iterative - Clean, O(1) space, no recursion limit risk
def traverse(head):
    curr = head
    while curr:
        print(curr.val)
        curr = curr.next
```

---

## Common Interview Pitfalls

### Pitfall 1: Using recursion for a massive array or linked list
Because Python has a default recursion limit of 1000, running a recursive function on a Linked List with 5,000 nodes will crash the program. Always use a `while` loop for simple linear traversal.

### Pitfall 2: Trying to write BFS recursively
Breadth-First Search requires exploring level by level. The Call Stack is inherently LIFO (Last-In, First-Out), making it a Depth-First structure. BFS relies on a FIFO Queue. While it is technically possible to hack together a recursive BFS by passing queues around, it is incredibly messy and interviewers will flag it. Use an iterative `while` loop with `collections.deque`.

---

## Key Takeaways

- Iteration is more memory efficient and avoids recursion limits.
- Recursion is significantly easier to write and read for branching logic (Trees, Graphs, Backtracking).
- Do not use recursion for simple linear iterations.
- Never use recursion for BFS.

---

## Related Topics

- [Call Stack](05-call-stack.md)
- [Tail Recursion](06-tail-recursion.md)
- [Trees](../algorithmic-patterns/14-trees.md)
