# Walkthrough: Two Sum

> **Difficulty:** Easy
> **Pattern:** Arrays & Hashing

---

## The Prompt

**Interviewer:** "Given an array of integers `nums` and an integer `target`, return indices of the two numbers such that they add up to `target`. You may assume that each input would have exactly one solution, and you may not use the same element twice. You can return the answer in any order."

## Step 1: Understand & Clarify

**Candidate:** "Okay, let me make sure I understand. We have an array of integers and a target sum. We need to find two distinct elements that add up to the target and return their indices. A few clarifying questions: Can the array contain negative numbers?"

**Interviewer:** "Yes, negative numbers are possible."

**Candidate:** "Got it. And you mentioned there's exactly one solution. Does that mean the array will always have at least two elements?"

**Interviewer:** "Yes, assume the array length is at least 2."

**Candidate:** "Okay, let's walk through an example. If `nums = [2, 7, 11, 15]` and `target = 9`, the answer should be `[0, 1]` because `2 + 7 = 9`."

**Interviewer:** "Spot on."

## Step 2: Match & Plan

**Candidate:** "The naive approach would be to use two nested loops. For every element `i`, we check every subsequent element `j` to see if they sum to the target. This would take $O(N^2)$ time and $O(1)$ space."

**Interviewer:** "Can we do better?"

**Candidate:** "Yes. We need to optimize the lookup time. If we are currently looking at `nums[i]`, we are trying to find if `target - nums[i]` exists in the array. If we store the elements we've seen so far in a Hash Map where the key is the number and the value is its index, we can do this lookup in $O(1)$ time."

**Interviewer:** "What would the complexity be for that?"

**Candidate:** "We'd iterate through the array once, doing $O(1)$ dictionary lookups, so the Time Complexity would be $O(N)$. However, the Space Complexity would also be $O(N)$ because in the worst case, we might store almost all elements in the dictionary before finding a match."

**Interviewer:** "That sounds like a great trade-off. Go ahead and code it."

## Step 3: Implement

*The candidate begins typing, narrating their thoughts.*

**Candidate:** "First, I'll initialize my hash map. I'll call it `seen` to map the value to its index."

```python
def twoSum(nums, target):
    seen = {} # val: index
```

**Candidate:** "Now I'll iterate through the array using `enumerate` so I have access to both the index and the number."

```python
    for i, num in enumerate(nums):
        diff = target - num
```

**Candidate:** "For each number, I calculate the `diff` we need to reach the target. If that `diff` is already in my `seen` map, we found our pair."

```python
        if diff in seen:
            return [seen[diff], i]
```

**Candidate:** "If it's not in the map, I add the current number and its index to the map, so future numbers can find it."

```python
        seen[num] = i
```

**Candidate:** "And since the problem guarantees a solution, I don't technically need a return statement outside the loop, but it's good practice, so I'll just return an empty list."

```python
    return []
```

## Step 4: Dry Run

**Candidate:** "Before we run this, let me trace it with the example `nums = [3, 2, 4]` and `target = 6`."

*Candidate adds comments to trace the variables.*

```python
# nums = [3, 2, 4], target = 6
# seen = {}
#
# i=0, num=3 | diff = 6-3=3 | 3 not in seen | seen = {3: 0}
# i=1, num=2 | diff = 6-2=4 | 4 not in seen | seen = {3: 0, 2: 1}
# i=2, num=4 | diff = 6-4=2 | 2 IS in seen! | return [seen[2], 2] -> [1, 2]
```

**Candidate:** "The trace outputs `[1, 2]`, which is correct since `nums[1] + nums[2] == 2 + 4 == 6`."

**Interviewer:** "Looks perfect. This is a Strong Hire for this round."

---

## Interviewer Rubric Notes

- **Problem Solving:** Excellent. Stated brute force quickly, moved to optimal Hash Map solution.
- **Coding:** Clean. Used `enumerate` Pythonically.
- **Verification:** Flawless manual dry run using comments.
- **Communication:** Very clear, checked edge cases (negatives, minimum length).
