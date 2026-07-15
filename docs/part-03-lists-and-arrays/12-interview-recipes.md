# List and Array Interview Recipes

## Introduction

Array problems are the most common type of interview question. Memorizing these core array manipulation recipes will give you the foundational tools needed to solve everything from Two Sum to Trapping Rain Water.

---

## Recipe 1: Two Pointers (Opposite Ends)

When an array is sorted, or you need to process elements from the outside in (e.g., finding pairs, reversing an array), place one pointer at the start and one at the end.

```python
def two_pointers(nums):
    left = 0
    right = len(nums) - 1
    
    while left < right:
        # Do something with nums[left] and nums[right]
        
        # Move pointers based on condition
        if condition:
            left += 1
        else:
            right -= 1
```

---

## Recipe 2: Sliding Window

When asked to find a subarray, a substring, or a maximum/minimum sum over a contiguous sequence, use a sliding window.

```python
def sliding_window(nums, k):
    window_sum = 0
    max_sum = 0
    left = 0
    
    for right in range(len(nums)):
        # Expand window
        window_sum += nums[right]
        
        # Shrink window if invalid
        while window_invalid_condition:
            window_sum -= nums[left]
            left += 1
            
        # Update result
        max_sum = max(max_sum, window_sum)
        
    return max_sum
```

---

## Recipe 3: Prefix Sums

When a problem asks for the sum of elements between indices `i` and `j` multiple times, precompute the sums in an array.

```python
def build_prefix_sums(nums):
    prefix = [0] * (len(nums) + 1)
    
    for i in range(len(nums)):
        prefix[i + 1] = prefix[i] + nums[i]
        
    return prefix

# Sum from index i to j (inclusive) is:
# prefix[j + 1] - prefix[i]
```

---

## Recipe 4: Frequency Map to Array

If a problem restricts inputs to bounded integers (e.g., ages 0-100, letters a-z), use an array for $O(1)$ space frequency counting instead of a hash map.

```python
def count_frequencies(nums):
    # Assuming nums are in range 0-100
    counts = [0] * 101
    
    for num in nums:
        counts[num] += 1
        
    return counts
```

---

## Recipe 5: In-Place Modification

If a problem requires $O(1)$ space, you must modify the array in-place. Often, you can use the array itself as a hash set by negating values (if values map to indices).

**Example: Find duplicates in an array containing numbers 1 to N.**
```python
def find_duplicates(nums):
    duplicates = []
    
    for i in range(len(nums)):
        val = abs(nums[i])
        
        # If the value at index val-1 is already negative, we saw it
        if nums[val - 1] < 0:
            duplicates.append(val)
        else:
            # Mark as seen by negating
            nums[val - 1] *= -1
            
    return duplicates
```

---

## Summary
- **Two Pointers**: Used for sorted arrays or inward processing.
- **Sliding Window**: Used for contiguous subarrays.
- **Prefix Sums**: Used for fast range queries.
- **Array as Hash Map**: Used for bounded frequencies or in-place flagging.
