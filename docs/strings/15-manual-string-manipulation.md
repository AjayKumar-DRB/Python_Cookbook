# Manual String Manipulation

## Introduction

Because Python provides so many powerful built-in string methods (`reverse()`, `replace()`, `split()`, `join()`), interviewers will often ask you to solve a problem *without* using these built-in methods. 

They want to see if you can manipulate strings manually, often by treating them as arrays of characters.

---

## Why Manual Manipulation is Difficult in Python

In languages like C++ or Java, strings (or character arrays) can often be modified in-place. 

In Python, strings are **immutable**. You cannot assign a new character to an existing string index:

```python
s = "hello"
# s[0] = "H" # TypeError: 'str' object does not support item assignment
```

To manually manipulate a string in Python, you must first convert it into a mutable list of characters, perform your modifications, and then join it back together.

---

## The Standard Pattern

If an interviewer asks you to reverse a string or swap characters without using slicing (`s[::-1]`) or `reversed()`, use this pattern:

1. Convert the string to a list of characters.
2. Use two pointers to swap elements in the list.
3. Use `"".join()` to create the final string.

### Example: Reverse a String Manually

```python
def reverse_string_manually(s):
    # Step 1: Convert to a mutable list
    chars = list(s)
    
    # Step 2: Use two pointers to swap
    left, right = 0, len(chars) - 1
    
    while left < right:
        # Swap characters
        chars[left], chars[right] = chars[right], chars[left]
        left += 1
        right -= 1
        
    # Step 3: Join back into a string
    return "".join(chars)

print(reverse_string_manually("interview")) # "weivretni"
```

---

## Appending Characters Manually

If you are asked to filter or build a string manually, **do not use `+=`**. 

Instead, append characters to a list and join them at the end.

### Example: Remove all vowels manually

```python
def remove_vowels_manually(s):
    vowels = {'a', 'e', 'i', 'o', 'u', 'A', 'E', 'I', 'O', 'U'}
    
    # Use a list to collect valid characters
    result = []
    
    for char in s:
        if char not in vowels:
            result.append(char)
            
    # Join exactly once at the end
    return "".join(result)
```

---

## Common Interview Mistakes

### Mistake: String Concatenation in a Loop
As mentioned repeatedly, using `result += char` inside a loop results in $O(N^2)$ time complexity because Python must allocate a new string and copy the contents every single time.

### Mistake: Trying to modify a string directly
Do not try to write `s[i], s[j] = s[j], s[i]`. It will immediately crash with a `TypeError`. You must use `list(s)` first.

---

## Time and Space Complexity

- **Time Complexity**: $O(N)$ for both `list(s)` and `"".join(chars)`, as well as iterating over the string.
- **Space Complexity**: $O(N)$ because `list(s)` creates a new array of characters that takes memory proportional to the string length. (In Python, manual string manipulation is never truly $O(1)$ space because of immutability).

---

## Summary
- When asked to avoid built-in string methods, convert the string to a list of characters using `list(s)`.
- Perform swaps or modifications on the list.
- Reconstruct the string using `"".join()`.
- Never use `+=` for building strings in a loop.
