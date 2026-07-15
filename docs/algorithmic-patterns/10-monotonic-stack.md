# Monotonic Stack

## Introduction

A Monotonic Stack is a stack whose elements are strictly increasing or strictly decreasing.

It is a specialized pattern used to solve "Next Greater Element" or "Next Smaller Element" problems in $O(N)$ time.

---

## How to Recognize It

Use a Monotonic Stack when:
- The problem asks for the **next greater** or **next smaller** element for every item in an array.
- The problem involves finding boundaries, like in the "Daily Temperatures" or "Largest Rectangle in Histogram" problems.
- A brute-force nested loop solution ($O(N^2)$) exists where the inner loop scans ahead to find a larger/smaller value.

---

## The Core Concept

Imagine finding the "Next Greater Element". 
You iterate through the array. If the current element is *smaller* than the top of the stack, you push it onto the stack (maintaining a decreasing order).

If the current element is *larger* than the top of the stack, it means you have found the "next greater element" for the item at the top of the stack. You `pop()` that item off, record the answer, and check the new top of the stack.

### Example: Daily Temperatures
Given a list of daily temperatures, return a list such that `answer[i]` is the number of days you have to wait after the $i^{th}$ day to get a warmer temperature.

```python
def daily_temperatures(temperatures):
    n = len(temperatures)
    result = [0] * n
    
    # The stack will store INDICES, not the actual temperatures!
    # This is crucial for calculating distances.
    stack = [] 
    
    for i, current_temp in enumerate(temperatures):
        
        # While stack is not empty AND the current temp is strictly 
        # greater than the temp at the index stored at the top of the stack
        while stack and current_temp > temperatures[stack[-1]]:
            
            # We found a warmer day!
            prev_index = stack.pop()
            
            # Calculate the distance
            result[prev_index] = i - prev_index
            
        # Push the current index onto the stack
        stack.append(i)
        
    return result
```

---

## Storing Indices vs Values

In 90% of Monotonic Stack problems, you should store the **indices** of the array in the stack, not the actual values. 

Storing indices allows you to:
1. Calculate the distance between elements (e.g., `i - stack[-1]`).
2. Easily look up the actual value anytime using `nums[stack[-1]]`.

---

## Time and Space Complexity

- **Time Complexity**: $O(N)$. Even though there is a `while` loop inside the `for` loop, every element is pushed onto the stack exactly once and popped exactly once. Therefore, the inner loop runs a maximum of $N$ times across the *entire* execution of the algorithm.
- **Space Complexity**: $O(N)$ to store the stack.

---

## Summary
- Use a Monotonic Stack for "Next Greater/Smaller" problems.
- Store **indices** on the stack, not values.
- If finding the next *greater* element, maintain a *decreasing* stack (pop when you see a larger value).
- If finding the next *smaller* element, maintain an *increasing* stack (pop when you see a smaller value).
