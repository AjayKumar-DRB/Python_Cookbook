# The Online Assessment (OA)

> The automated gatekeeper.

---

## Introduction

Before you ever speak to a human engineer, you must pass the Online Assessment (OA). This is an automated coding test sent via platforms like HackerRank, CodeSignal, or LeetCode Assessments.

The OA is a brutal, binary filter. If you don't pass all the test cases, you usually get an automated rejection email.

---

## How the OA differs from a live interview

In a live interview, an $O(N)$ algorithm with a minor off-by-one bug can still result in a "Hire" if you communicated well.

In an OA, **communication does not matter, only passing test cases matters.**
- You must write code that compiles and executes perfectly.
- You must handle extreme edge cases.
- You must write highly optimal code, or you will hit a "Time Limit Exceeded" (TLE) error on the hidden test cases.

---

## Strategies for Passing the OA

### 1. Write the Brute Force immediately
If you have 60 minutes for 2 questions, do not spend 25 minutes staring at a blank screen trying to invent an $O(N)$ solution. Write the $O(N^2)$ brute force solution in 5 minutes. 
It might pass 6/10 test cases. Earning 60% points is infinitely better than earning 0%. Once the brute force is passing some cases, copy it, comment it out, and start working on the optimal solution.

### 2. Print Debugging is your only friend
Since you don't have an interviewer to give you hints, you must rely on `print()` statements to debug. If a hidden test case is failing, you won't know the input. Print the length of the input, or print extreme values to deduce what the hidden case is testing.

### 3. Watch for Integer Overflow (in other languages)
If you are coding in Java or C++, OAs are notorious for having test cases where the answer exceeds $2^{31}-1$. You must use `long`. 
*(Note: Python handles arbitrarily large integers automatically, giving you a massive advantage here).*

### 4. CodeSignal Specifics
CodeSignal uses a global score (out of 600 or 850). It usually consists of 4 questions in 70 minutes:
- Q1 & Q2: Very easy arrays/strings. (Do these in 10 mins).
- Q3: Matrix traversal or Hash Maps. (Do this in 20 mins).
- Q4: Very hard Trees, DP, or complex logic. (Use the remaining 40 mins).

---

## Common Pitfalls

- **Leaving a question blank:** Always write *something*, even if it only passes the base case. Partial credit exists.
- **Wasting time on syntax:** You cannot Google syntax during an OA (it is proctored/recorded). You must have standard Python methods (`.split()`, `.sort()`, `collections.Counter`) memorized.

---

## Key Takeaways

- The OA is a strict, automated test where only passing test cases matters.
- Always write a brute force solution first to secure partial credit.
- Python is highly advantageous for OAs because it prevents integer overflow errors.

---

## Related Topics

- [Coding Round](02-coding-round.md)
