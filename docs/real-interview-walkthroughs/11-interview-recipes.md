# Real Interview Walkthrough Recipes

> Quick tips derived from the walkthroughs.

---

## 1. Always Ask About Edge Cases First
In every successful walkthrough, the candidate paused to ask about edge cases *before* proposing an algorithm.
- "Are there negative numbers?"
- "Can the array be empty?"
- "Is the array guaranteed to be sorted?"

## 2. Start with the Brute Force
In the Two Sum and Trapping Rain Water walkthroughs, the candidate verbally acknowledged the $O(N^2)$ brute force solution. This anchors the conversation and allows the interviewer to explicitly ask, "Can we do better?", leading into the optimal approach.

## 3. Name Your Variables Well
In the LRU Cache walkthrough, the candidate abstracted pointer logic into `insert()` and `remove()` helper functions. In the Merge Intervals walkthrough, the candidate unpacked the variables `current_start, current_end = interval`. 

Clean code is not a bonus; it is a strict requirement for a "Strong Hire".

## 4. Master the `print`-less Debug
Notice that none of the candidates relied on hitting "Run" to see if their code worked. They used comments to track variable state line-by-line. 

Practicing this manual dry run on paper or in comments is the single best way to prepare for the pressure of a live interview.

## 5. Embrace the Constraints of Python
In the Median Data Stream walkthrough, the candidate explicitly acknowledged that Python does not have a Max Heap, and cleanly implemented the standard workaround (`-val`). Interviewers love candidates who know the quirks of their chosen language.
