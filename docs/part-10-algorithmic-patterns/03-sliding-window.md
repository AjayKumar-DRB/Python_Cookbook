# Sliding Window

## Introduction

The Sliding Window pattern is used to perform operations on a specific window size of a given array or linked list, such as finding the longest subarray containing all 1s, or finding a contiguous subarray with a given sum.

This pattern reduces nested loops ($O(N^2)$) to a single linear pass ($O(N)$).

---

## How to Recognize It

Use Sliding Window when the problem asks for:
- Maximum/Minimum/Longest/Shortest **contiguous subarray** or substring.
- An answer that requires maintaining a running sum, product, or frequency count over a contiguous sequence.

---

## The Pythonic Template

A sliding window uses two pointers: `left` and `right`.
The `right` pointer expands the window by moving forward in a `for` loop.
The `left` pointer shrinks the window in a `while` loop whenever a specific constraint is violated.

```python
def sliding_window(nums, k):
    left = 0
    current_state = 0
    max_length = 0
    
    for right in range(len(nums)):
        # 1. ADD nums[right] to current_state
        current_state += nums[right]
        
        # 2. SHRINK window if constraint is violated
        while current_state > k:
            current_state -= nums[left]
            left += 1
            
        # 3. UPDATE the answer based on valid window
        max_length = max(max_length, right - left + 1)
        
    return max_length
```

---

## Variations

### 1. Fixed Window Size
If the problem specifies a fixed window size `k`, you don't need a `while` loop to shrink. You simply shrink the window when `right >= k`.

```python
def fixed_window(nums, k):
    window_sum = sum(nums[:k])
    max_sum = window_sum
    
    for right in range(k, len(nums)):
        # Add incoming element, subtract outgoing element
        window_sum += nums[right] - nums[right - k]
        max_sum = max(max_sum, window_sum)
        
    return max_sum
```

### 2. Variable Window (Strings)
Often used with strings to find substrings with specific characters. You will usually combine this with a `collections.Counter` or a manual frequency dictionary.

---

## Time and Space Complexity

- **Time Complexity**: $O(N)$. Even though there is a `while` loop inside the `for` loop, both the `left` and `right` pointers only traverse the array once. They never move backwards.
- **Space Complexity**: $O(1)$ for basic sums/counts, or $O(K)$ if using a dictionary to track frequencies of characters.

---

## Summary
- Use Sliding Window for **contiguous subarrays/substrings**.
- Expand with `right` in a `for` loop.
- Shrink with `left` in a `while` loop when constraints are broken.
- Time complexity is $O(N)$ because each element is visited at most twice (once by `right`, once by `left`).
