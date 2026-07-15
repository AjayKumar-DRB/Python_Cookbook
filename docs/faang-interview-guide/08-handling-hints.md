# Handling Hints

> How to take feedback without getting defensive.

---

## Introduction

A technical interview is not a solitary exam; it is a collaboration. It is perfectly normal to receive hints during an interview. In fact, receiving a hint and immediately incorporating it into your solution is a strong positive signal.

However, many candidates ruin their chances by reacting poorly when given a hint.

---

## The "Ego" Trap

When an interviewer says: *"Are you sure that `while` loop condition is correct?"*

**The Wrong Response:** *"Yes, because if I don't use `<=`, it won't check the last element."* (Defensive, arguing).

**The Right Response:** *"Let me double-check that. Ah, you're right. Because I'm using `len(nums) - 1`, the `<=` would cause an out-of-bounds error on the next line. Good catch, I'll change it to `<`."*

Interviewers are testing how you receive code reviews. If you argue with them during an interview, they assume you will be a nightmare to work with on a real engineering team.

---

## Types of Hints

### 1. The Direct Bug Pointer
*Example:* "Take another look at line 42."
*Action:* Immediately assume line 42 has a critical bug. Stop everything you are doing and dry run line 42.

### 2. The Algorithmic Nudge
*Example:* "This $O(N^2)$ solution works, but can we optimize the lookup step?"
*Action:* Acknowledge the hint. "You're right, the lookup is currently $O(N)$. If I use a Hash Map, I can reduce that to $O(1)$."

### 3. The Edge Case Check
*Example:* "What happens if the input array is empty?"
*Action:* Trace the empty array through your code. If it breaks, add a guard clause (`if not nums: return 0`) at the top.

---

## What if you don't understand the hint?

Sometimes, the interviewer gives a vague hint, and you still have no idea what to do.

Do not pretend to understand and blindly guess code. Ask for clarification.

*"I understand that we need to optimize the space complexity, and you mentioned avoiding extra arrays. Does this mean we should try modifying the input array in-place?"*

---

## Key Takeaways

- Never argue with an interviewer's hint. Assume they are correct.
- A hint is not a failure; it is a collaboration test.
- If a hint points to a bug, thank them, fix it, and move on.

---

## Related Topics

- [Communicating Thinking](07-communicating-thinking.md)
- [Debugging Under Pressure](08-debugging-under-pressure.md)
