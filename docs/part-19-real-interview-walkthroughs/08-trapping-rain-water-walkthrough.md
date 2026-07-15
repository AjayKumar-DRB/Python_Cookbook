# Walkthrough: Trapping Rain Water

> **Difficulty:** Hard
> **Pattern:** Two Pointers

---

## The Prompt

**Interviewer:** "Given `n` non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it can trap after raining."

## Step 1: Understand & Clarify

**Candidate:** "Okay, so the water trapped above any given bar depends on the heights of the bars to its left and right. Water will spill over the lowest side. Is that correct?"

**Interviewer:** "Exactly. Can you formalize that mathematically?"

**Candidate:** "The water trapped above block `i` is the minimum of the highest block to its left and the highest block to its right, minus the height of block `i` itself."
`Water[i] = min(max_left, max_right) - height[i]`

**Interviewer:** "Spot on."

## Step 2: Match & Plan

**Candidate:** "The brute force approach would be to iterate through the array. For every element, we scan the entire left side to find `max_left` and the entire right side to find `max_right`. This takes $O(N)$ for every element, making it $O(N^2)$ overall."

**Interviewer:** "Can we optimize it?"

**Candidate:** "Yes. We can precompute the maximums. We create an array `max_left_array` and a `max_right_array`. We do one pass left-to-right to fill the left array, and one pass right-to-left to fill the right array. Then, a final pass to calculate the water. This takes $O(N)$ time, but also $O(N)$ space."

**Interviewer:** "Can we do $O(N)$ time and $O(1)$ space?"

**Candidate:** "Yes... if we use **Two Pointers**. We can have a `left` pointer at index 0 and a `right` pointer at the end. We also maintain variables `left_max` and `right_max`. Since water is determined by the *minimum* of the two boundaries, we only care about the smaller boundary. If `left_max < right_max`, we know the water on the left side is safely bounded by `left_max`, so we can calculate it, add it to our total, and move the `left` pointer inwards. If `right_max` is smaller, we calculate the right side and move the `right` pointer inwards."

**Interviewer:** "Excellent. Write it out."

## Step 3: Implement

**Candidate:** "First, the edge case."

```python
def trap(height: list[int]) -> int:
    if not height:
        return 0
```

**Candidate:** "I'll initialize the two pointers and the max trackers."

```python
    left, right = 0, len(height) - 1
    left_max, right_max = height[left], height[right]
    res = 0
```

**Candidate:** "Now the main loop. They move towards each other until they meet."

```python
    while left < right:
        # We process whichever side has the smaller boundary
        if left_max < right_max:
            left += 1
            # Update the max
            left_max = max(left_max, height[left])
            # The water trapped is the max boundary minus the current height
            res += left_max - height[left]
        else:
            right -= 1
            right_max = max(right_max, height[right])
            res += right_max - height[right]
            
    return res
```

## Step 4: Discussion

**Interviewer:** "In the line `res += left_max - height[left]`, is it possible for that to be negative?"

**Candidate:** "No, because immediately before that line, we do `left_max = max(left_max, height[left])`. So `left_max` is guaranteed to be at least as large as `height[left]`. If `height[left]` is the new maximum, the difference is exactly `0`, meaning no water can sit on top of it. This prevents negative water."

**Interviewer:** "Perfect. Strong Hire."

---

## Interviewer Rubric Notes

- **Problem Solving:** Derived the math formula (`min(L, R) - H`) immediately. Explained the $O(N^2)$ brute force, the $O(N)$ space precomputation, and finally the $O(1)$ space Two Pointer approach.
- **Coding:** Flawless logic. Correctly updated the pointer *before* calculating the water to avoid out-of-bounds issues.
- **Communication:** Clearly explained *why* the Two Pointer approach works (we only care about the bottleneck boundary).
