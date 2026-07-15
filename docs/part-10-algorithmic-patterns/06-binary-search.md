# Binary Search

## Introduction

Binary Search is the ultimate optimization pattern. It allows you to search a sorted sequence in $O(\log N)$ time by repeatedly halving the search space.

---

## How to Recognize It

Use Binary Search when:
- The input array is **sorted** (or can be sorted, and $O(N \log N)$ is acceptable).
- The problem asks for an $O(\log N)$ time complexity.
- You are searching for a specific value, a boundary, or the "first bad version".
- **Advanced**: The answer must fall within a specific numeric range, and you can easily check if a guess is valid ("Binary Search on Answer").

---

## The Standard Template

Binary search is prone to off-by-one errors and infinite loops. Memorize this exact template to avoid them.

```python
def binary_search(nums, target):
    left = 0
    right = len(nums) - 1
    
    while left <= right:
        # Prevents integer overflow in languages like Java/C++, 
        # though Python handles arbitrarily large integers automatically.
        mid = left + (right - left) // 2 
        
        if nums[mid] == target:
            return mid
        elif nums[mid] < target:
            # Target is in the right half
            left = mid + 1
        else:
            # Target is in the left half
            right = mid - 1
            
    return -1 # Not found
```

---

## Pattern 1: Finding Boundaries

What if the array has duplicates, and you need to find the *first* occurrence of a target? (e.g., Python's `bisect_left`).

You do not return immediately upon finding the target. Instead, you keep searching the left half to see if there is an earlier occurrence.

```python
def find_first(nums, target):
    left = 0
    right = len(nums) - 1
    result = -1
    
    while left <= right:
        mid = left + (right - left) // 2
        
        if nums[mid] == target:
            # Record the result, but keep searching left!
            result = mid
            right = mid - 1
        elif nums[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
            
    return result
```

---

## Pattern 2: Binary Search on Answer

This is the most difficult variation and frequently appears in Hard interviews (e.g., Koko Eating Bananas).

Instead of searching through a given array, you binary search through a **range of possible answers**.

1. Identify the minimum possible answer (`left`).
2. Identify the maximum possible answer (`right`).
3. Write a helper function `is_valid(guess)` that checks if a guessed answer works.
4. Binary search between `left` and `right`.

```python
def min_eating_speed(piles, h):
    # Minimum speed is 1 banana/hr, Max is the largest pile
    left = 1
    right = max(piles)
    
    def can_eat_all(speed):
        hours = 0
        for pile in piles:
            # Math trick for ceiling division: (a + b - 1) // b
            hours += (pile + speed - 1) // speed 
        return hours <= h
        
    result = right
    
    while left <= right:
        mid = left + (right - left) // 2
        
        if can_eat_all(mid):
            # It works, but can we do it slower?
            result = mid
            right = mid - 1
        else:
            # Too slow, must eat faster
            left = mid + 1
            
    return result
```

---

## Time and Space Complexity

- **Time Complexity**: $O(\log N)$ where $N$ is the size of the search space.
- **Space Complexity**: $O(1)$.

---

## Summary
- Use `while left <= right:` and `mid = left + (right - left) // 2`.
- If searching for boundaries, record the `mid` and continue shrinking the search space instead of returning immediately.
- If the problem asks for a "minimum capacity" or "maximum speed", consider Binary Searching the answer range.
