# The Coding Round

> The 45-minute crucible.

---

## Introduction

The coding round is the core of the technical interview. You will face 2 to 3 of these during an onsite loop. 

You have 45 minutes to read a problem, devise an algorithm, write the code, and prove that it works. This requires intense focus and a strict adherence to a time management framework.

---

## The 45-Minute Timeline

If you mismanage your time, you will fail, even if you know the answer. Memorize this timeline.

### Minutes 0-5: Understand & Clarify
- The interviewer pastes the prompt. Read it carefully.
- Ask clarifying questions. *"Can the array be empty?" "Are we dealing with negative numbers?"*
- Run through a small example out loud to ensure you understand the expected output.

### Minutes 5-15: Propose & Plan
- State the Brute Force solution quickly. *"The naive way is nested loops, which is $O(N^2)$."*
- Propose the optimal solution. *"We can use a Hash Map to track complements in $O(N)$ time."*
- **CRITICAL:** Wait for the interviewer's approval. If they say *"Sounds good"*, proceed. If they say *"Can we do better on space?"*, you must pivot.
- Write 3 lines of pseudo-code comments.

### Minutes 15-35: Implement
- Write the actual Python code.
- Talk through your logic as you type. *"I'm initializing the dictionary here..."*
- Use clean, descriptive variable names (`max_profit` instead of `m`).
- Do not remain completely silent for more than 2 minutes.

### Minutes 35-40: Dry Run & Debug
- Stop typing. Do not say you are done.
- Say: *"Let me dry run this with the first example."*
- Trace your variables explicitly.
- Fix any minor bugs (off-by-one errors) you find during the trace.

### Minutes 40-45: Complexity & Q&A
- State the final Big O Time and Space complexity.
- The interviewer will ask if you have any questions for them. Always have 2 prepared questions about the company or their team's tech stack.

---

## Common Pitfalls

- **Coding too early:** If you start writing code at Minute 3 without agreeing on an algorithm, the interviewer might stop you 20 minutes later and say your approach is fundamentally flawed. You will not have time to recover.
- **Silent coding:** If you don't talk, the interviewer can't give you hints.
- **Defensiveness:** If the interviewer points out a bug, immediately accept it. Do not argue that it "should work".

---

## Key Takeaways

- The coding round is a test of communication and time management, not just algorithms.
- Always get verbal approval for your algorithm before writing code.
- Dry run your code before declaring you are finished.

---

## Related Topics

- [Systematic Problem Solving](../systematic-problem-solving/01-index.md)
- [Communicating Your Solution](../systematic-problem-solving/09-communicating-your-solution.md)
