# Systematic Problem Solving Recipes

> A summary of the UMPIRE framework.

---

## The Ultimate Interview Checklist

Memorize this flow and apply it strictly during your 45-minute interviews.

### 1. Understand (0-5 minutes)
- Read the prompt carefully.
- Read the constraints (determine time complexity).
- Clarify edge cases (Empty? Negatives? Duplicates?).
- Walk through Example 1 and Example 2 out loud.

### 2. Match (5-10 minutes)
- Identify the core pattern (e.g., "This is a Top K problem").
- State the naive Brute Force solution and its time complexity.
- Propose the optimal Data Structure and Algorithm.
- Discuss the Time vs Space trade-offs with the interviewer.

### 3. Plan (10-15 minutes)
- Write 3-4 lines of plain English pseudo-code as comments.
- Get verbal agreement from the interviewer: *"Does this approach sound good to you?"*

### 4. Implement (15-30 minutes)
- Write the Python code.
- Narrate your intent, not your keystrokes.
- Keep the code clean and use meaningful variable names.

### 5. Review (30-35 minutes)
- DO NOT SAY "I'm done".
- Say: *"Let me dry run this code with an example."*
- Trace the variables using code comments.
- Fix any off-by-one errors or bugs you find.

### 6. Evaluate (35-40 minutes)
- State the final Time Complexity.
- State the final Space Complexity.
- Discuss how you might optimize it further if you had more time (or if the constraints changed).

---

## Key Takeaways

If you follow this strict checklist, you will avoid the most common reasons candidates fail:
1. Writing code before understanding the problem.
2. Guessing the wrong algorithm.
3. Having a bug because they didn't dry run.
4. Not knowing their complexity.
