# Easy Capstone: Valid Palindrome II

> **Time Limit:** 30 Minutes
> **Patterns:** Two Pointers, Strings

---

## The Prompt

Given a string `s`, return `True` if the `s` can be palindrome after deleting **at most one** character from it.

**Example 1:**
```
Input: s = "aba"
Output: true
```

**Example 2:**
```
Input: s = "abca"
Output: true
Explanation: You could delete the character 'c'.
```

**Example 3:**
```
Input: s = "abc"
Output: false
```

**Constraints:**
- `1 <= s.length <= 10^5`
- `s` consists of lowercase English letters.

---

*Stop scrolling. Set a 30-minute timer and write your solution before checking the answer below.*

---

## The Solution Walkthrough

### 1. Understand & Match
The constraints say `N = 10^5`. An $O(N^2)$ solution will fail. We need an $O(N)$ solution.
Checking for a palindrome naturally suggests the **Two Pointers** pattern (one at the start, one at the end, moving inwards).

### 2. Plan
If the characters at `left` and `right` match, we move both pointers inwards. 
What happens when they *don't* match? The prompt says we can delete *at most one* character. 

This means we have two parallel universes to check:
1. Universe A: We delete the character at `left` (so we check if the substring from `left + 1` to `right` is a palindrome).
2. Universe B: We delete the character at `right` (so we check if the substring from `left` to `right - 1` is a palindrome).

If either of those remaining substrings is a perfect palindrome, we return `True`. Otherwise, we return `False`.

### 3. Implement

```python
class Solution:
    def validPalindrome(self, s: str) -> bool:
        # Helper function to check if a specific slice is a perfect palindrome
        def check_palindrome(l, r):
            while l < r:
                if s[l] != s[r]:
                    return False
                l += 1
                r -= 1
            return True

        left, right = 0, len(s) - 1
        
        while left < right:
            if s[left] != s[right]:
                # Mismatch found! We use our 1 allowed deletion.
                # Check Universe A (skip left) or Universe B (skip right)
                skip_left = check_palindrome(left + 1, right)
                skip_right = check_palindrome(left, right - 1)
                
                return skip_left or skip_right
                
            left += 1
            right -= 1
            
        # If we made it through the whole string without mismatches, it's already a palindrome
        return True
```

### 4. Complexity Analysis
- **Time Complexity:** $O(N)$. We iterate through the string with the two pointers. When a mismatch is found, we trigger `check_palindrome` twice, which scans the remaining characters at most once. The total operations scale linearly with the length of the string.
- **Space Complexity:** $O(1)$. We only use a few integer pointers (`left`, `right`, `l`, `r`). No extra arrays or recursion stacks are created.

*(Note: In Python, doing `s[left+1:right+1] == s[left+1:right+1][::-1]` is a very common shortcut, but it creates a copy of the substring, making the Space Complexity $O(N)$. Using the pointer helper function ensures strict $O(1)$ space).*
