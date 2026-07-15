# String Interview Recipes

## Introduction

Many string problems in coding interviews share the exact same foundational logic. Instead of re-inventing the wheel during an interview, you should memorize these standard "recipes" or templates.

---

## Recipe 1: Checking for a Palindrome

A palindrome reads the same forwards and backwards.

### Pythonic Way (Using Slicing)
If space complexity is not strictly constrained, slicing is the fastest and most readable way to check for a palindrome.

```python
def is_palindrome_pythonic(s):
    return s == s[::-1]
```
- **Time**: $O(N)$
- **Space**: $O(N)$ (creates a reversed copy)

### Optimal Way (Two Pointers)
If you must use $O(1)$ space, use two pointers meeting in the middle.

```python
def is_palindrome_optimal(s):
    left, right = 0, len(s) - 1
    
    while left < right:
        if s[left] != s[right]:
            return False
        left += 1
        right -= 1
        
    return True
```
- **Time**: $O(N)$
- **Space**: $O(1)$

---

## Recipe 2: Frequency Counting (Anagrams)

Many problems require you to count character frequencies (e.g., Valid Anagram, Longest Palindrome).

### Pythonic Way (Using `Counter`)
`collections.Counter` is incredibly powerful and handles frequency counting automatically.

```python
from collections import Counter

def is_anagram(s, t):
    return Counter(s) == Counter(t)
```
- **Time**: $O(N)$
- **Space**: $O(U)$ where $U$ is the number of unique characters.

### Array Way (Lowercase ASCII only)
If the problem specifies "lowercase English letters only," using an array of size 26 is technically more efficient and often preferred by strict interviewers.

```python
def is_anagram_array(s, t):
    if len(s) != len(t):
        return False
        
    counts = [0] * 26
    
    for i in range(len(s)):
        counts[ord(s[i]) - ord('a')] += 1
        counts[ord(t[i]) - ord('a')] -= 1
        
    for count in counts:
        if count != 0:
            return False
            
    return True
```
- **Time**: $O(N)$
- **Space**: $O(1)$ (array is always size 26)

---

## Recipe 3: Reversing Words in a Sentence

Given a sentence `"hello world"`, reverse it to `"world hello"`.

### Pythonic Way
Leverage `split()` and `join()`.

```python
def reverse_words(s):
    words = s.split()
    return " ".join(reversed(words))
```
- **Time**: $O(N)$
- **Space**: $O(N)$

---

## Recipe 4: Removing Unwanted Characters

Given a string with punctuation and mixed casing, clean it for processing.

### Using a List Comprehension
```python
def clean_string(s):
    return "".join([char.lower() for char in s if char.isalnum()])
```
- **Time**: $O(N)$
- **Space**: $O(N)$

---

## Summary
- Use `s == s[::-1]` for quick palindrome checks.
- Use `collections.Counter` for character frequency maps.
- Use `ord(char) - ord('a')` with a 26-element array for $O(1)$ space character counting on lowercase strings.
- Master `"".join()` combined with list comprehensions for fast and readable string cleaning.
