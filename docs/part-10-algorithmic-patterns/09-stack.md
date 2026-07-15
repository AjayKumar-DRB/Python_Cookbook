# Stack

## Introduction

A Stack is a LIFO (Last-In, First-Out) data structure. The last element added to the stack will be the first one removed.

In Python, you do not need a special class or module to implement a stack. A standard Python `list` is already highly optimized for stack operations.

---

## How to Recognize It

Use a Stack when:
- You need to parse or evaluate nested structures (e.g., Valid Parentheses, basic calculators).
- You need to reverse the order of items.
- You need to track a history of states and be able to "undo" or step back (e.g., Browser History, DFS).

---

## The Pythonic Implementation

Simply use a standard `list`.
- **Push**: `list.append(x)`
- **Pop**: `list.pop()`
- **Peek**: `list[-1]`

```python
stack = []

# Push elements (O(1))
stack.append("A")
stack.append("B")
stack.append("C")

# Peek at the top element without removing it (O(1))
top = stack[-1] # "C"

# Pop elements (O(1))
print(stack.pop()) # "C"
print(stack.pop()) # "B"
```

---

## Valid Parentheses (The Classic Question)

The most famous stack question asks you to validate if a string of brackets is properly closed.

```python
def is_valid(s):
    stack = []
    mapping = {")": "(", "}": "{", "]": "["}
    
    for char in s:
        # If it's a closing bracket
        if char in mapping:
            # Pop the top element if stack isn't empty, else assign a dummy value
            top_element = stack.pop() if stack else '#'
            
            # If the popped element doesn't match the corresponding opening bracket
            if mapping[char] != top_element:
                return False
        else:
            # It's an opening bracket, push to stack
            stack.append(char)
            
    # Valid if the stack is completely empty at the end
    return not stack
```

---

## Time and Space Complexity

- **Time Complexity**: $O(1)$ for `append()`, `pop()`, and peek `[-1]`.
- **Space Complexity**: $O(N)$ where $N$ is the maximum number of items on the stack.

---

## Summary
- In Python, a stack is just a `list`.
- Use `append()` to push, `pop()` to remove, and `[-1]` to peek.
- Use stacks for nested parsing (parentheses, calculators) and tracking history.
