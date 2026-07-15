# Base Case

> The stopping condition of a recursive function that prevents an infinite loop.

---

## Introduction

Every recursive function MUST have at least one base case. If you forget to include a base case, or if your recursive step never progresses toward the base case, your function will run forever until the program crashes.

---

## What is it?

The base case is the simplest, smallest instance of a problem that can be answered immediately without making any further recursive calls.

When the base case is reached, the function simply `return`s a known value, causing the recursion to start unrolling back up the call stack.

---

## Identifying the Base Case

To find the base case for an interview problem, ask yourself:
*"What is the absolute simplest, most trivial input this function could receive?"*

Here are common base cases in DSA:

| Data Structure / Problem | Typical Base Case | Example |
|--------------------------|-------------------|---------|
| **Arrays / Strings** | The array is empty or has length 1. | `if not nums: return 0` |
| **Pointers (Two Pointers)** | The pointers cross. | `if left > right: return` |
| **Binary Trees** | The current node is `None` (a null pointer). | `if not root: return 0` |
| **Graphs / Grid Search** | The current cell is out of bounds or already visited. | `if r < 0 or r >= ROWS: return` |
| **Math / Factorial** | The number reaches `0` or `1`. | `if n <= 1: return 1` |

---

## Multiple Base Cases

A function can (and often does) have multiple base cases. 

For example, when validating if a string is a palindrome recursively, we might have two base cases:
1. Valid base case: The string is empty or has length 1 (it is a palindrome).
2. Invalid base case: The first and last characters don't match (it is not a palindrome).

```python
def is_palindrome(s: str) -> bool:
    # Base Case 1: Trivial success
    if len(s) <= 1:
        return True
        
    # Base Case 2: Trivial failure
    if s[0] != s[-1]:
        return False
        
    # Recursive Step
    return is_palindrome(s[1:-1])
```

---

## Common Pitfalls

### Pitfall 1: Unreachable Base Case
If your recursive step doesn't actively move closer to the base case, the base case will never hit.

```python
def countdown(n: int):
    if n <= 0: # Base case
        return
    print(n)
    # BUG: n is not decremented. The base case is never reached!
    countdown(n) 
```

### Pitfall 2: Base Case Placed After Work
Always place your base case at the very top of the function. If you try to access data before checking the base case, you will hit an `IndexError` or `AttributeError`.

```python
def sum_array(nums, i):
    # BUG: Accessing nums[i] before checking if i is in bounds!
    val = nums[i] 
    
    if i == len(nums): # Base case is too late
        return 0
        
    return val + sum_array(nums, i + 1)
```

---

## Key Takeaways

- Define your base case *before* writing the recursive step.
- Place the base case at the very top of the function body.
- Ensure your recursive step shrinks the input so it eventually hits the base case.

---

## Related Topics

- [Recursion Basics](02-recursion-basics.md)
- [Call Stack](05-call-stack.md)
