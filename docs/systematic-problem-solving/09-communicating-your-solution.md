# Communicating Your Solution

> Thinking out loud without overthinking.

---

## Introduction

A coding interview is not a math test; it is a collaborative work session. The interviewer is evaluating what it would be like to have you on their team. 

If you sit in absolute silence for 20 minutes, write perfect code, and say "Done", you might still fail the interview because they have no idea how you communicate.

---

## 1. The Initial Thoughts

After reading the problem, immediately start talking. 
- Mention the Brute Force solution first.
- *"The naive approach here would be to use nested loops to check every pair, which would take $O(N^2)$ time."*

This establishes a baseline and proves you can solve it, even if sub-optimally.

---

## 2. Thinking Out Loud (The Right Way)

You do not need to narrate every keystroke. ("Now I'm typing `def`, now I'm typing `for i in range`..."). That is annoying.

Instead, narrate your **intent**.
- *"I'm going to initialize a hash map to keep track of the frequencies."*
- *"Now I need to iterate through the array, and for each element, I'll check if its complement exists in the map."*
- *"If it does, we found our answer, so I'll return the indices."*

---

## 3. Getting Stuck

If you don't know the answer, **say so, but explain what you are trying to do.**

*"I know I need to reduce this $O(N^2)$ time to $O(N)$. Usually, that involves a Hash Map or Two Pointers. Since the array isn't sorted, Two Pointers won't work well here. So I'm trying to think of how to map these values to a Dictionary to get $O(1)$ lookups..."*

By verbalizing this, the interviewer knows exactly where your head is at. They can now give you a micro-hint: *"Yes, a Hash Map is the right path. What exactly would you store as the key?"*

If you were silent, they wouldn't know if you were stuck on the Hash Map, or if you had completely given up.

---

## 4. Handling Silence

If the interviewer is completely silent while you code, that is normal. They are taking notes. Do not let the silence panic you. Just keep coding and occasionally narrating your broad intent.

---

## Key Takeaways

- Establish the Brute Force baseline immediately.
- Narrate your intent, not your keystrokes.
- If you get stuck, explain your thought process and the options you are weighing. Acknowledge your roadblocks out loud.

---

## Related Topics

- [Choosing Algorithms](05-choosing-algorithms.md)
- [FAANG Interview Guide](../faang-interview-guide/01-index.md)
