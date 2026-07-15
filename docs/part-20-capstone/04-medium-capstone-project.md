# Medium Capstone: Product of Array Except Self

> **Time Limit:** 45 Minutes
> **Patterns:** Arrays, Prefix/Suffix Products

---

## The Prompt

Given an integer array `nums`, return an array `answer` such that `answer[i]` is equal to the product of all the elements of `nums` except `nums[i]`.

The product of any prefix or suffix of `nums` is **guaranteed** to fit in a 32-bit integer.

You must write an algorithm that runs in $O(N)$ time and without using the division operation.

**Example 1:**
```
Input: nums = [1,2,3,4]
Output: [24,12,8,6]
```

**Constraints:**
- `2 <= nums.length <= 10^5`
- `-30 <= nums[i] <= 30`

**Follow up:** Can you solve the problem in $O(1)$ extra space complexity? (The output array does not count as extra space for space complexity analysis.)

---

*Stop scrolling. Set a 45-minute timer and write your solution before checking the answer below.*

---

## The Solution Walkthrough

### 1. Understand & Match
The brute force way is $O(N^2)$ (nested loops to multiply everything else).
The "math" way is $O(N)$ (multiply ALL numbers together, then divide the total by `nums[i]`). But the prompt explicitly forbids division.

If we can't use division, we need to precompute products. For any element `i`, its answer is the product of everything to its **Left**, multiplied by the product of everything to its **Right**.
This matches the **Prefix / Suffix Array** pattern.

### 2. Plan (The $O(N)$ Space Approach)
We can create two arrays: `left_products` and `right_products`.
- `left_products[i]` will hold the product of all elements to the left of `i`.
- `right_products[i]` will hold the product of all elements to the right of `i`.
- Then, `answer[i] = left_products[i] * right_products[i]`.

### 3. Plan (The $O(1)$ Space Follow-up)
The prompt says the output array doesn't count towards space complexity.
So, instead of making a separate `left_products` array, we can just build the left products directly inside the `answer` array.
Then, instead of making a `right_products` array, we can iterate backwards, keeping a running total of the right product in a single integer variable (`postfix`), and multiplying it into the `answer` array on the fly.

### 4. Implement (Optimal)

```python
class Solution:
    def productExceptSelf(self, nums: list[int]) -> list[int]:
        n = len(nums)
        # The output array doesn't count towards Space Complexity
        res = [1] * n
        
        # 1. Build the Left products directly in the res array
        prefix = 1
        for i in range(n):
            res[i] = prefix
            prefix *= nums[i]
            
        # 2. Build the Right products on the fly, multiplying them into res
        postfix = 1
        # Loop backwards from n-1 down to 0
        for i in range(n - 1, -1, -1):
            res[i] *= postfix
            postfix *= nums[i]
            
        return res
```

### 5. Complexity Analysis
- **Time Complexity:** $O(N)$. We make two separate passes through the array. $O(2N)$ simplifies to $O(N)$.
- **Space Complexity:** $O(1)$ extra space. We only use two integer variables (`prefix` and `postfix`). The `res` array is the required output and does not count against the auxiliary space constraints according to standard interview rules.
