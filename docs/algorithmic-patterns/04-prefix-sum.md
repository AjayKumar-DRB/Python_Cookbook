# Prefix Sum

## Introduction

The Prefix Sum pattern involves precomputing the cumulative sum of an array up to each index. 

This allows you to calculate the sum of **any subarray in $O(1)$ time** after an initial $O(N)$ precomputation phase.

---

## How to Recognize It

Use Prefix Sum when:
- The problem asks you to calculate the sum, product, or XOR of a subarray multiple times (range queries).
- The array elements are static (they do not change during the queries).
- You are dealing with "Subarray Sum Equals K" style problems.

---

## The Core Concept

If you want the sum of elements from index $i$ to $j$ inclusive, it is mathematically equal to:
`Sum(0 to j) - Sum(0 to i-1)`

To do this, we build a `prefix` array where `prefix[k]` contains the sum of elements from index $0$ to $k-1$.

```python
def build_prefix(nums):
    prefix = [0] * (len(nums) + 1)
    
    for i in range(len(nums)):
        prefix[i + 1] = prefix[i] + nums[i]
        
    return prefix

# Given nums =   [1, 2,  3,  4]
# Prefix array = [0, 1,  3,  6, 10]
```
*(Note: We make the prefix array 1 element larger and start with `0`. This makes calculating the sum from index 0 extremely clean without needing `if` statements).*

### $O(1)$ Range Query
```python
def range_query(prefix, left, right):
    # Sum of nums[left] through nums[right] inclusive
    return prefix[right + 1] - prefix[left]
```

---

## Subarray Sum Equals K

A classic FAANG question asks you to find the number of contiguous subarrays that sum to $K$.

Because arrays can have negative numbers, Sliding Window will not work (shrinking the window doesn't guarantee a smaller sum). You must use Prefix Sum combined with a Dictionary (Hash Map).

```python
def subarray_sum(nums, k):
    # Map: prefix_sum -> frequency
    # Initialize with 0:1 because a prefix sum of exactly K 
    # means (current_sum - K) == 0.
    counts = {0: 1} 
    
    current_sum = 0
    result = 0
    
    for num in nums:
        current_sum += num
        
        # If (current_sum - k) exists in the map, it means 
        # there is a subarray ending here that sums to k
        if (current_sum - k) in counts:
            result += counts[current_sum - k]
            
        # Add current sum to map
        counts[current_sum] = counts.get(current_sum, 0) + 1
        
    return result
```

---

## Time and Space Complexity

- **Time Complexity**: $O(N)$ to build the prefix array or map. $O(1)$ per query afterward.
- **Space Complexity**: $O(N)$ to store the prefix array or the dictionary.

---

## Summary
- Use Prefix Sums for $O(1)$ range queries on static arrays.
- `Sum(i to j) = Prefix[j+1] - Prefix[i]`.
- For "Subarray Sums Equal K" (including arrays with negative numbers), store the running prefix sums in a dictionary to find `current_sum - k`.
