# ASCII and Unicode

## Introduction

In many coding interviews, you will manipulate characters based on their integer values. Python supports Unicode out of the box, but many interview problems explicitly state that the input consists only of lowercase English letters (ASCII).

Understanding how characters are represented in memory is crucial for solving problems involving anagrams, frequency counting, and string shifting.

---

## What is ASCII?

ASCII is an encoding standard that maps characters to integers. 

For example:
- `'A'` is `65`
- `'a'` is `97`
- `'0'` is `48`

You do not need to memorize these exact numbers. You only need to know that characters are sequential. 
- Since `'a'` is `97`, `'b'` must be `98`, `'c'` is `99`, and so on.

---

## Unicode in Python

Python 3 strings are sequences of Unicode code points. This means Python strings can natively handle emojis, foreign alphabets, and special symbols.

```python
print(len("🐍")) # 1
```

However, in 99% of coding interviews, problems constrain the input to standard ASCII characters to simplify logic.

---

## The 26-Element Array Trick

Because English letters are sequential in ASCII, you can map the letters `'a'` through `'z'` to the indices `0` through `25` of an array.

This is a very common technique for string problems because it allows you to count character frequencies in $O(1)$ space, rather than using a hash map which carries more overhead.

### How to Map Characters to Indices

To map a lowercase letter to an index between `0` and `25`, subtract the integer value of `'a'` from the integer value of the character.

Python provides the `ord()` function to get the integer value of a character.

```python
char = 'c'
index = ord(char) - ord('a')
print(index) # 2
```

### Example: Frequency Counter

```python
def get_frequencies(s):
    # Initialize an array of size 26 with zeros
    counts = [0] * 26
    
    for char in s:
        index = ord(char) - ord('a')
        counts[index] += 1
        
    return counts
```

### Tradeoffs
- **Array of size 26**: 
  - **Pros**: $O(1)$ extra space, slightly faster than a dictionary, guarantees iteration in alphabetical order.
  - **Cons**: Only works if the character set is restricted (e.g., only lowercase English letters).
- **Dictionary/Hash Map**:
  - **Pros**: Handles any character set (Unicode, punctuation, mixed case).
  - **Cons**: Carries more memory overhead, iteration order depends on insertion order.

---

## Time and Space Complexity

When using an array of size 26 for counting:
- **Time Complexity**: $O(N)$ where $N$ is the length of the string.
- **Space Complexity**: $O(1)$ because the array size is always exactly 26, regardless of $N$.

---

## Summary
- Characters are represented as sequential integers.
- If a problem restricts input to lowercase English letters, consider using a 26-element array instead of a dictionary for $O(1)$ space frequency counting.
- Use `ord(char) - ord('a')` to map characters to `0-25`.
