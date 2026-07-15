# Dry Running

> Step 5: Review.

---

## Introduction

You have just finished writing the last line of code. You turn to the interviewer and say: *"I'm done."*

The interviewer looks at your code and says: *"Does this work?"*

This is a trap. If you say "Yes", and there is a bug, you lose massive points. **Never say you are done until you have dry run your code.**

---

## What is a Dry Run?

A dry run (or desk check) means manually executing your code, line by line, pretending your brain is the Python interpreter. You keep track of variable states on the whiteboard or in code comments.

Interviewers grade you on your ability to catch your own bugs before hitting the "Run" button.

---

## How to Dry Run properly

1. **Pick a small, non-trivial example.**
   Do not pick `[1, 2, 3]` if the edge cases involve negative numbers. Pick something like `[-1, 2, 0]`.

2. **Write out your variables.**
   At the top of your function, write comments tracking state.
   ```python
   # nums = [2, 7, 11]
   # target = 9
   #
   # i = 0 | num = 2 | diff = 7 | map = {2: 0}
   # i = 1 | num = 7 | diff = 2 | map = {2: 0} -> RETURN [0, 1]
   ```

3. **Trace every single line.**
   Do not skip lines because "you know what it does." Literally point your finger (or cursor) at the `if` statement and ask: *"Is 7 inside the map? Yes."*

4. **Test the Edge Cases.**
   What happens if the array is empty? Trace the first line. `if not nums: return []`. Good, it caught it.

---

## Catching Bugs

If you catch a bug during your dry run, **do not panic**. This is a good thing!

Say out loud: *"Ah, wait. If I trace this here, the index goes out of bounds. Let me fix that by changing the loop condition from `len(nums)` to `len(nums) - 1`."*

Interviewers love candidates who can debug their own code calmly. Catching your own bug before execution often results in zero penalty.

---

## Key Takeaways

- Never say "I'm done" immediately after writing code.
- Always say: *"Let me walk through an example to verify this works."*
- Track variable state explicitly in comments.
- Catching your own bugs during a dry run is a major positive signal.

---

## Related Topics

- [Debugging Under Pressure](08-debugging-under-pressure.md)
