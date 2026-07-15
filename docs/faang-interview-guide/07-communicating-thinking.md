# Communicating Thinking

> Making your brain visible to the interviewer.

---

## Introduction

The primary reason you are asked to solve algorithms live is so the company can evaluate your thought process. 

If you solve a problem silently in 10 minutes, the interviewer has zero data on *how* you solved it. Did you memorize it? Are you a genius? They don't know, and "I don't know" usually translates to a rejection.

---

## The "Think Out Loud" Framework

You must maintain a steady stream of relevant consciousness.

### 1. Acknowledging the Naive
Always state the brute force first. It shows you understand the baseline complexity.
- *"The simplest way is to compare every element with every other element, which takes $O(N^2)$ time."*

### 2. Exploring Avenues
When trying to find the optimal solution, narrate your internal decision tree.
- *"I know I need $O(N)$ time. This usually means a Hash Map or Two Pointers."*
- *"If I use Two Pointers, the array needs to be sorted. But sorting takes $O(N \log N)$, so that won't work."*
- *"So I must use a Hash Map. Let's see what I can store as the key..."*

### 3. Explaining Trade-offs
When you make a choice, justify it.
- *"I could use recursion here, but since the input can be up to 10^5, we might hit the Python recursion limit. So I'll use an iterative stack instead."*

### 4. Announcing Intent While Coding
When you start typing, don't read the code verbatim. Announce the *purpose* of the block you are writing.
- **Don't say:** *"For i in range length of nums..."*
- **Do say:** *"Now I'm iterating through the array to populate the frequency map."*

---

## Handling the "Blank Mind" Panic

Everyone freezes at some point in an interview. The worst thing you can do is sit in silence for 5 minutes.

If your mind goes completely blank, **narrate your confusion**.
- *"I'm currently stuck. I see that a Hash Map won't work because we need contiguous subarrays, but I'm struggling to see how to apply a Sliding Window when there are negative numbers."*

By saying this, the interviewer knows exactly where your roadblock is. They can now give you a targeted hint to unblock you. 

---

## Key Takeaways

- Silence is your enemy.
- Narrate your decision tree (why you chose X over Y).
- If you freeze, explain exactly *what* you are stuck on.

---

## Related Topics

- [Handling Hints](08-handling-hints.md)
- [Systematic Problem Solving](../systematic-problem-solving/09-communicating-your-solution.md)
