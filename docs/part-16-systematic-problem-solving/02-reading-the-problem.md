# Reading the Problem

> Step 1: Understand.

---

## Introduction

The very first thing you do in an interview is read the prompt. 
Candidates often skim the prompt, look at the first example, and immediately start talking. **This is a massive mistake.**

Interview prompts are dense. Every single word matters.

---

## What is it?

"Reading the problem" means actively dissecting the prompt to extract constraints, edge cases, and hidden hints. 

You must translate the English description into technical constraints before you even think about an algorithm.

---

## 1. Extracting Constraints

Pay extreme attention to the **Constraints** section at the bottom of the prompt (or ask the interviewer if it's a verbal prompt). Constraints often give away the expected time complexity!

| Constraint ($N$) | Expected Time Complexity | Expected Algorithm |
|------------------|--------------------------|--------------------|
| $N \le 10$ | $O(N!)$ or $O(2^N)$ | Backtracking, Permutations |
| $N \le 20$ | $O(2^N)$ | Backtracking, Bitmask Subsets |
| $N \le 100$ | $O(N^3)$ or $O(N^4)$ | 3D Dynamic Programming, Matrix operations |
| $N \le 1,000$ | $O(N^2)$ | 2D Dynamic Programming, Nested Loops |
| $N \le 10^5$ | $O(N \log N)$ or $O(N)$ | Sorting, Two Pointers, Sliding Window, Greedy |
| $N \le 10^9$ | $O(\log N)$ or $O(1)$ | Binary Search, Math, Bit Manipulation |

If a problem says `nums.length <= 10^5`, you instantly know that a nested `for` loop ($O(N^2)$) will fail, saving you 10 minutes of writing the wrong code.

---

## 2. Clarifying Edge Cases

Before you write code, ask out loud:
- *"Can the input array be empty?"*
- *"Are there negative numbers? What about zero?"*
- *"Are duplicates allowed?"*
- *"Is the array already sorted?"*
- *"Does the string contain uppercase, lowercase, spaces, or special characters?"*

**Example:**
If the prompt says "Find the maximum subarray sum", and you don't ask if there are negative numbers, you might write an algorithm that only works for positive numbers and fail the interview.

---

## 3. Tracing the Examples

Never assume you understand the problem just from reading the text. Look at **Example 1**. 
Can you manually trace the input to the output in your head? If not, trace it on the whiteboard.

Look at **Example 2** and **Example 3** (which are usually edge cases). Why does this specific input produce this specific output?

---

## Best Practices

- Read the prompt twice.
- Look at the constraints to determine the target Time Complexity.
- Write down 2-3 edge case inputs as comments at the top of your editor.
- Verbally confirm your understanding with the interviewer: *"So just to confirm, if I receive `[0, 0]`, the expected output should be `X`, correct?"*

---

## Key Takeaways

- Constraints give away the algorithm.
- Do not write a single line of code until you have clarified edge cases.
- Always manually trace the provided examples.

---

## Related Topics

- [Identifying Patterns](03-identifying-patterns.md)
- [Complexity Analysis](06-complexity-analysis.md)
