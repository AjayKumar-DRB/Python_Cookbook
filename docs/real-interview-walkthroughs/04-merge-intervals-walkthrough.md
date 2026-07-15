# Walkthrough: Merge Intervals

> **Difficulty:** Medium
> **Pattern:** Intervals / Sorting

---

## The Prompt

**Interviewer:** "Given an array of `intervals` where `intervals[i] = [start_i, end_i]`, merge all overlapping intervals, and return an array of the non-overlapping intervals that cover all the intervals in the input."

## Step 1: Understand & Clarify

**Candidate:** "Okay, so if we have overlapping time blocks, we combine them into a single larger block. For example, if the input is `[[1,3], [2,6], [8,10]]`, the output should be `[[1,6], [8,10]]` because `[1,3]` and `[2,6]` overlap."

**Interviewer:** "Exactly."

**Candidate:** "Are the intervals guaranteed to be sorted by their start times?"

**Interviewer:** "No, you should assume they are in random order."

**Candidate:** "Got it. And can an interval be a single point in time, like `[1, 1]`?"

**Interviewer:** "Yes, `start_i <= end_i`."

## Step 2: Match & Plan

**Candidate:** "Since the intervals are unsorted, comparing every interval to every other interval to check for overlaps would take $O(N^2)$ time. That feels too slow."

**Interviewer:** "Agreed."

**Candidate:** "If we sort the intervals based on their start times first, then any overlapping intervals will be strictly adjacent to each other in the array."

**Interviewer:** "How do you know two adjacent intervals overlap?"

**Candidate:** "If the start time of the *next* interval is less than or equal to the end time of the *current* interval, they overlap. In that case, we merge them by taking the maximum of their end times."

**Candidate:** "The Time Complexity would be $O(N \log N)$ for the initial sort, and then a single pass $O(N)$ through the array, making the overall time $O(N \log N)$. Space complexity would be $O(N)$ to store the merged result (or $O(N)$ for the sorting algorithm itself in Python)."

**Interviewer:** "That approach is perfectly optimal. Let's write the code."

## Step 3: Implement

**Candidate:** "First, I'll handle the edge case where the list is empty, though based on constraints it might not be necessary."

```python
def merge(intervals: list[list[int]]) -> list[list[int]]:
    if not intervals:
        return []
```

**Candidate:** "Next, I'll sort the intervals in place. By default, Python's `sort()` on a list of lists sorts by the first element, which is the `start_i`. This is exactly what we want."

```python
    intervals.sort(key=lambda x: x[0])
```

**Candidate:** "I'll initialize my `merged` list with the first interval so we have something to compare against."

```python
    merged = [intervals[0]]
```

**Candidate:** "Now I'll iterate through the rest of the intervals."

```python
    for interval in intervals[1:]:
        current_start, current_end = interval
        
        # Get the reference to the last interval we added to merged
        last_added = merged[-1]
```

**Candidate:** "If the current interval overlaps with the last added interval..."

```python
        if current_start <= last_added[1]:
            # We merge them by updating the end time of the last added interval
            last_added[1] = max(last_added[1], current_end)
```

**Candidate:** "Otherwise, they don't overlap, so we just append the current interval to the result."

```python
        else:
            merged.append(interval)
            
    return merged
```

## Step 4: Dry Run & Hints

**Candidate:** "Let me trace this with the example `[[1,3], [2,6], [8,10]]`. It's already sorted."
- `merged = [[1, 3]]`
- First iteration: `interval = [2, 6]`. `current_start = 2`, `last_added = [1, 3]`.
- Is `2 <= 3`? Yes. We update `last_added[1] = max(3, 6) = 6`. `merged` is now `[[1, 6]]`.
- Second iteration: `interval = [8, 10]`. `current_start = 8`, `last_added = [1, 6]`.
- Is `8 <= 6`? No. We append `[8, 10]`. `merged` is now `[[1, 6], [8, 10]]`.

**Interviewer:** "What if the input was `[[1, 4], [2, 3]]`?"

**Candidate:** "Ah, good check. An interval completely engulfed by another.
- `merged = [[1, 4]]`
- `interval = [2, 3]`. `current_start = 2`, `last_added = [1, 4]`.
- Is `2 <= 4`? Yes. Update `last_added[1] = max(4, 3) = 4`.
- `merged` remains `[[1, 4]]`. It works perfectly because of the `max()` check."

**Interviewer:** "Excellent. One final question: Python's `sort()` modifies the input array in place. In a real production system, is it a good idea to mutate an input argument?"

**Candidate:** "That's a great point. Usually, it's considered bad practice to mutate inputs without the caller expecting it because it can cause side effects elsewhere in the application. If this were production code, I would probably do `sorted_intervals = sorted(intervals)` to avoid mutating the original array, though that requires $O(N)$ extra space."

**Interviewer:** "Great answer. We're done here."

---

## Interviewer Rubric Notes

- **Problem Solving:** Recognized that sorting unlocks the optimal solution.
- **Coding:** Clean array destructuring (`current_start, current_end = interval`) makes the logic very readable.
- **Verification:** Handled the engulfed interval edge case perfectly.
- **Communication:** Excellent domain knowledge regarding mutating input arguments.
