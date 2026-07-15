# Walkthrough: Valid Parentheses

> **Difficulty:** Easy
> **Pattern:** Stack

---

## The Prompt

**Interviewer:** "Given a string `s` containing just the characters `'(', ')', '{', '}', '['` and `']'`, determine if the input string is valid. An input string is valid if open brackets are closed by the same type of brackets, and they are closed in the correct order."

## Step 1: Understand & Clarify

**Candidate:** "Okay, so we need to ensure every opening bracket has a matching closing bracket in the right order. Let's look at some examples. `s = "()[]{}"` would be valid. `s = "([)]"` would be invalid because the parenthesis closes before the square bracket does."

**Interviewer:** "Correct."

**Candidate:** "A few questions. Can the string be empty?"

**Interviewer:** "No, assume `1 <= s.length <= 10^4`."

**Candidate:** "Got it. Can the string contain other characters like letters or numbers?"

**Interviewer:** "No, strictly just those 6 bracket characters."

## Step 2: Match & Plan

**Candidate:** "Because of the 'Last-In, First-Out' nature of nested brackets—where the most recently opened bracket must be the first one closed—this strongly suggests using a **Stack**."

**Interviewer:** "How would the stack work?"

**Candidate:** "I'll iterate through the string. If I see an opening bracket, I push it onto the stack. If I see a closing bracket, I check the top of the stack. If the stack is empty, or the top of the stack isn't the matching opening bracket, it's invalid. If it matches, I pop it off the stack. Finally, if the string is valid, the stack should be empty at the end."

**Interviewer:** "What is the time and space complexity?"

**Candidate:** "Time complexity is $O(N)$ since we iterate through the string once. Pushing and popping from a list in Python is $O(1)$. Space complexity is $O(N)$ in the worst case, like `"((((("`, where all characters are opening brackets and get pushed to the stack."

**Interviewer:** "Makes sense. Let's code it."

## Step 3: Implement

**Candidate:** "To make the matching clean and avoid a giant `if/elif` block, I'll create a dictionary mapping closing brackets to their corresponding opening brackets."

```python
def isValid(s: str) -> bool:
    bracket_map = {")": "(", "}": "{", "]": "["}
    stack = []
```

**Candidate:** "Now I'll iterate through the characters in the string."

```python
    for char in s:
        # If it's a closing bracket
        if char in bracket_map:
```

**Candidate:** "I need to check the top of the stack. But I have to be careful—the stack might be empty if we start with a closing bracket like `"]"`. So I'll check that first."

```python
            top_element = stack.pop() if stack else '#'
            
            # If the popped element doesn't match the required opening bracket
            if bracket_map[char] != top_element:
                return False
```

**Candidate:** "If the character is an opening bracket, we just push it onto the stack."

```python
        else:
            stack.append(char)
```

**Candidate:** "At the end, if the string was valid, all pairs should have popped, leaving the stack empty."

```python
    return not stack
```

## Step 4: Dry Run

**Candidate:** "Let's dry run this with an invalid example, `s = "(]"`.
- `char = '('`. It's not in `bracket_map` (it's an opener), so we append to `stack`. `stack = ['(']`.
- `char = ']'`. It IS in `bracket_map`. `top_element = stack.pop()` makes `top_element = '('`. `stack` is now empty.
- We check `bracket_map[']'] != top_element`. `bracket_map[']']` is `'['`. So `'[' != '('`. This is True, so we `return False`."

**Interviewer:** "What if the string is just `"["`?"

**Candidate:** "Good edge case. Let's trace it.
- `char = '['`. Append to stack. `stack = ['[']`.
- Loop ends. We evaluate `return not stack`. `stack` is not empty, so `not stack` evaluates to `False`. It correctly returns `False`."

**Interviewer:** "Great job. Very clean solution."

---

## Interviewer Rubric Notes

- **Problem Solving:** Instantly recognized the Stack pattern. Avoided messy if/else chains by using a HashMap.
- **Coding:** Very clean. Good handling of the empty stack edge case (`if stack else '#'` is a nice Pythonic touch, though a simple `if not stack` check is also fine).
- **Verification:** Dry ran the code perfectly and handled an edge case proposed by the interviewer.
