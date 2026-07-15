# Difference Array (Line Sweep)

## Introduction

While Prefix Sums are used for fast $O(1)$ **reads** (range queries), the Difference Array pattern is used for fast $O(1)$ **writes** (range updates).

If a problem asks you to add a value to all elements from index $i$ to $j$, a brute force loop takes $O(N)$. A Difference Array allows you to record this update in $O(1)$ time, applying all updates at the very end in a single $O(N)$ pass.

---

## How to Recognize It

Use Difference Array when:
- The problem asks you to increment/decrement elements across multiple overlapping ranges (e.g., Corporate Flight Bookings, Car Pooling).
- You only need to know the final state of the array after all updates are processed.

---

## The Core Concept

Instead of adding a value `V` to every element between `left` and `right`, we only update two bounds in a tracking array:
1. Add `V` at index `left`. (This says: "From this point forward, add V").
2. Subtract `V` at index `right + 1`. (This says: "From this point forward, stop adding V").

After applying all $O(1)$ updates, we run a single prefix sum pass to calculate the final values.

```python
def range_updates(length, updates):
    # Create an array of zeros, 1 element larger to handle the right+1 bounds
    diff = [0] * (length + 1)
    
    for left, right, value in updates:
        # Start adding value at left
        diff[left] += value
        
        # Stop adding value after right
        diff[right + 1] -= value
        
    # Apply prefix sum to resolve the final array
    result = []
    current = 0
    for i in range(length):
        current += diff[i]
        result.append(current)
        
    return result
```

---

## Meeting Rooms / Car Pooling (Line Sweep Variation)

A very common variation involves checking if a capacity is exceeded at any point in time. 

Instead of a standard array index, the indices represent timestamps. This is often called the **Line Sweep** algorithm.

```python
def car_pooling(trips, capacity):
    # Assuming max location is 1000
    timeline = [0] * 1001 
    
    for num_passengers, start, end in trips:
        timeline[start] += num_passengers
        timeline[end] -= num_passengers # Passengers get off at end
        
    current_passengers = 0
    for p in timeline:
        current_passengers += p
        if current_passengers > capacity:
            return False
            
    return True
```

If the timestamp range is massive (e.g., $10^9$), you cannot use an array. Instead, use a dictionary to store the updates, sort the keys, and sweep through them.

---

## Time and Space Complexity

- **Time Complexity**: $O(U + N)$ where $U$ is the number of updates and $N$ is the length of the array. If using a dictionary and sorting (Line Sweep), it becomes $O(U \log U)$.
- **Space Complexity**: $O(N)$ to store the difference array.

---

## Summary
- Use Difference Arrays for fast $O(1)$ range updates.
- `diff[left] += val` and `diff[right + 1] -= val`.
- Resolve the final values using a running sum.
- Used for overlapping intervals, meeting rooms, and capacity problems.
