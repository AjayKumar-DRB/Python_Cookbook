# Walkthrough: Median from Data Stream

> **Difficulty:** Hard
> **Pattern:** Heaps

---

## The Prompt

**Interviewer:** "The median is the middle value in an ordered integer list. Implement the `MedianFinder` class:
- `MedianFinder()` initializes the object.
- `void addNum(int num)` adds the integer `num` from the data stream to the data structure.
- `double findMedian()` returns the median of all elements so far.

You must design an algorithm where `addNum` runs in $O(\log N)$ time."

## Step 1: Understand & Clarify

**Candidate:** "To find the median, the numbers theoretically need to be sorted. If the list has an odd number of elements, the median is the exact middle. If it's even, it's the average of the two middle elements."

**Interviewer:** "Correct."

**Candidate:** "If we use a standard list, `addNum` could append in $O(1)$, but then we'd have to sort it to find the median, taking $O(N \log N)$. Or we could insert it in sorted order using Binary Search, but inserting into a list still requires shifting elements, taking $O(N)$."

## Step 2: Match & Plan

**Candidate:** "To get $O(\log N)$ insertion, we must use a **Heap** (Priority Queue). But a single heap only gives us access to one extreme (the min or the max), not the middle."

**Interviewer:** "How can we get the middle?"

**Candidate:** "We can use TWO heaps. A Max Heap to store the *smaller* half of the numbers, and a Min Heap to store the *larger* half of the numbers.
The median will always be either the root of the Max Heap, the root of the Min Heap, or the average of both. We just need to make sure the heaps are always balanced in size."

**Interviewer:** "What happens if a new number belongs in the small half, but the small half is already full?"

**Candidate:** "We push it to the small half, then immediately pop the largest element from the small half and push it into the large half. This shifts the boundaries dynamically."

**Interviewer:** "Perfect. Let's code it."

## Step 3: Implement

**Candidate:** "In Python, `heapq` only implements a Min Heap. To simulate a Max Heap, we have to push the negative of the number."

```python
import heapq

class MedianFinder:
    def __init__(self):
        # Two heaps, large (min heap) and small (max heap)
        self.small = [] # Max Heap (we push -val)
        self.large = [] # Min Heap
```

**Candidate:** "For `addNum`, by default I will always push to `small` first. Then I will balance the values."

```python
    def addNum(self, num: int) -> None:
        # 1. Push to small (Max Heap, so multiply by -1)
        heapq.heappush(self.small, -num)
        
        # 2. Make sure every element in small is <= every element in large
        if self.small and self.large and (-self.small[0] > self.large[0]):
            val = -heapq.heappop(self.small)
            heapq.heappush(self.large, val)
```

**Candidate:** "Now I need to balance the sizes. I'll define a rule: the sizes can differ by at most 1. If `small` gets too big, I move an element to `large`. If `large` gets too big, I move an element to `small`."

```python
        # 3. Balance sizes
        if len(self.small) > len(self.large) + 1:
            val = -heapq.heappop(self.small)
            heapq.heappush(self.large, val)
            
        if len(self.large) > len(self.small) + 1:
            val = heapq.heappop(self.large)
            heapq.heappush(self.small, -val)
```

**Candidate:** "For `findMedian`, if the lengths are odd, the median is the root of whichever heap is larger. If they are even, it's the average of the two roots."

```python
    def findMedian(self) -> float:
        if len(self.small) > len(self.large):
            return -self.small[0]
        if len(self.large) > len(self.small):
            return self.large[0]
            
        # Even length
        return (-self.small[0] + self.large[0]) / 2.0
```

## Step 4: Hints & Discussion

**Interviewer:** "Can you trace `addNum(3)`, `addNum(1)`, `addNum(2)`?"

**Candidate:** "Sure.
- `addNum(3)`: Pushed to `small` as `-3`.
- `addNum(1)`: Pushed to `small` as `-1`. Now `small = [-3, -1]`. Wait, `-3` is at the top of the Max Heap, which represents `3`. The size difference is 2, so the size balancing triggers. We pop `-3` (which is `3`), and push it to `large`. `small = [-1]`, `large = [3]`.
- `addNum(2)`: Pushed to `small` as `-2`. `small = [-2, -1]`. We check if top of `small` (`2`) is > top of `large` (`3`). No. Size difference is 1, which is fine.
- `findMedian()`: `small` is larger, so we return `-small[0]`, which is `2`. The median of `[1, 2, 3]` is `2`. It works perfectly."

**Interviewer:** "Excellent handling of Python's Min Heap limitations. Very clean code."

---

## Interviewer Rubric Notes

- **Problem Solving:** Instantly recognized the Two Heap pattern to maintain dynamic median bounds.
- **Coding:** Perfect handling of Python's lack of a Max Heap by negating values.
- **Verification:** Successfully traced the dynamic shifting of elements between the two heaps.
