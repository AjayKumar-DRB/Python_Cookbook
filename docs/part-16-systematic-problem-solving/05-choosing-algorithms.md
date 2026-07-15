# Choosing Algorithms

> Connecting the pattern to the implementation.

---

## Introduction

Once you have identified the core pattern and the correct data structures, choosing the specific algorithm is usually straightforward. 

However, you must be able to verbalize *why* you are choosing a specific algorithm over an alternative to demonstrate engineering maturity.

---

## The "Trade-off" Conversation

Interviewers love to hear candidates discuss trade-offs before they write code. If you just jump to the optimal algorithm without explaining why the naive algorithm is bad, you lose points.

### 1. Time vs Space

The most common trade-off in computer science is spending more memory to save execution time.

**Scenario:** You need to find if two numbers sum to $X$.
- **Brute Force (No extra space):** Nested loops take $O(N^2)$ time and $O(1)$ space.
- **Optimal (Using space):** A Hash Map takes $O(N)$ time, but costs $O(N)$ extra space.
- **What to say:** *"The naive approach is $O(N^2)$ time, but we can optimize this to $O(N)$ time if we are willing to spend $O(N)$ space using a Hash Map."*

### 2. Sorting First vs HashMap

Often, a problem can be solved by sorting the array first, or by using a Hash Map.

- **Sorting:** Takes $O(N \log N)$ time, but usually $O(1)$ space (depending on the sorting algorithm).
- **HashMap:** Takes $O(N)$ time, but $O(N)$ space.
- **What to say:** *"If memory is extremely constrained, we could sort the array first and use two pointers in $O(N \log N)$ time and $O(1)$ space. However, if we have enough memory, the Hash Map approach is faster at $O(N)$ time."*

### 3. BFS vs DFS

Both algorithms traverse a graph, but they have completely different use cases.

- **BFS:** Explores level by level. Uses a Queue. Guarantees the shortest path in an unweighted graph. Space complexity depends on the maximum width of the graph (can be huge).
- **DFS:** Explores as deep as possible. Uses a Stack (or recursion). Good for finding *any* path, cycle detection, or exploring all combinations. Space complexity depends on the maximum depth of the graph.
- **What to say:** *"Since we need the shortest path, we must use BFS. DFS might find a longer, meandering path before finding the short one."*

---

## Writing the Pseudo-code

Before you write actual Python code, you should write a 3-4 line pseudo-code plan as comments. This proves to the interviewer that you have a solid plan and aren't just "winging it".

```python
def findTarget(nums, target):
    # 1. Initialize a hash map to store {value: index}
    # 2. Iterate through nums
    # 3. If target - num is in map, return the indices
    # 4. Otherwise, add num to map
    pass
```

---

## Key Takeaways

- Always verbally acknowledge the naive Brute Force solution first, and explain its time complexity.
- Explain the trade-offs (Time vs Space) of your chosen optimal algorithm.
- Write 3-4 lines of plain English pseudo-code before writing Python syntax.

---

## Related Topics

- [Identifying Patterns](03-identifying-patterns.md)
- [Complexity Analysis](06-complexity-analysis.md)
