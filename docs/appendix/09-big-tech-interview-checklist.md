# Big Tech Interview Checklist

## Before Writing Code
- [ ] **Clarify the Requirements:** Repeat the question back in your own words.
- [ ] **Define the Edge Cases:** Empty inputs? Negative numbers? Duplicates? Extreme limits?
- [ ] **Propose a Brute Force Solution:** Briefly state the naïve approach and its time/space complexity to establish a baseline.
- [ ] **Brainstorm Optimizations:** Can we use a hash map? Sorting? Two pointers? DP?
- [ ] **Agree on an Approach:** Walk through your optimized algorithm logically before writing code.
- [ ] **State the Complexities:** Declare the Time and Space complexity of your planned approach *before* coding.

## While Writing Code
- [ ] **Modularity:** Break complex logic into smaller, clearly named helper functions.
- [ ] **Naming:** Use descriptive variable names (`max_profit`, `current_node`). Avoid `x`, `y`, `temp`.
- [ ] **Think Out Loud:** Explain your logic as you type. Silence is the enemy.
- [ ] **Leave Space:** If writing on a whiteboard, leave room between lines for edits. (Less applicable for online pads).

## After Writing Code
- [ ] **Manual Trace:** Pick a small, non-trivial example and trace through your code line by line.
- [ ] **Check Edge Cases Again:** Does your code crash on an empty array? A single element?
- [ ] **Review Complexities:** Double-check if your actual implementation matches the Time/Space complexity you promised.
- [ ] **Clean Up:** Remove debugging print statements or unnecessary comments.
