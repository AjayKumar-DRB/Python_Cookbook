# Walkthrough: Number of Islands

> **Difficulty:** Medium
> **Pattern:** Graphs (Matrix DFS/BFS)

---

## The Prompt

**Interviewer:** "Given an $M \times N$ 2D binary grid `grid` which represents a map of `'1'`s (land) and `'0'`s (water), return the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically."

## Step 1: Understand & Clarify

**Candidate:** "Okay, so we're looking for connected components of `1`s. Diagonal connections don't count, right?"

**Interviewer:** "Correct, only horizontal and vertical."

**Candidate:** "And the edges of the grid are assumed to be surrounded by water?"

**Interviewer:** "Yes."

**Candidate:** "Got it. Can the grid be empty?"

**Interviewer:** "It's possible, so you should handle it."

## Step 2: Match & Plan

**Candidate:** "This is a classic Graph Traversal problem on a matrix. The algorithm would be to iterate through every cell in the grid. If we find a `'1'`, that's a new island. We increment our island count, and then we need to 'explore' that entire island so we don't double count it."

**Interviewer:** "How do you explore it?"

**Candidate:** "We can trigger a Depth-First Search (DFS) or Breadth-First Search (BFS) starting from that `'1'`. As we visit the connected `'1'`s, we need to mark them as visited. We could use a `visited` Set, or, to save space, we could just mutate the input grid and change the `'1'`s to `'0'`s (or another character like `'#'`) as we visit them."

**Interviewer:** "Mutating the input grid is a good optimization. Let's do that. What's the complexity?"

**Candidate:** "Time Complexity is $O(M \times N)$ because we visit every cell, and our DFS only visits cells that are `'1'`s once. Space Complexity is $O(M \times N)$ in the worst case (if the entire grid is one giant island) due to the recursive Call Stack."

**Interviewer:** "Sounds good. Please write it."

## Step 3: Implement

**Candidate:** "First, the edge case."

```python
def numIslands(grid: list[list[str]]) -> int:
    if not grid or not grid[0]:
        return 0
```

**Candidate:** "I'll get the dimensions of the grid and initialize my island counter."

```python
    rows, cols = len(grid), len(grid[0])
    islands = 0
```

**Candidate:** "Now I'll define the DFS helper function. It will take a row `r` and column `c`."

```python
    def dfs(r, c):
        # Base case: check out of bounds, or if the current cell is water
        if (r < 0 or r >= rows or 
            c < 0 or c >= cols or 
            grid[r][c] == "0"):
            return
```

**Candidate:** "If it's a valid land cell, we mark it as visited by sinking it (turning it to `'0'`)."

```python
        grid[r][c] = "0"
```

**Candidate:** "Then we recursively call DFS in all four directions: up, down, left, right."

```python
        dfs(r + 1, c) # down
        dfs(r - 1, c) # up
        dfs(r, c + 1) # right
        dfs(r, c - 1) # left
```

**Candidate:** "Now for the main loop. We iterate through every cell in the matrix."

```python
    for r in range(rows):
        for c in range(cols):
            # If we find land, we found a new island!
            if grid[r][c] == "1":
                islands += 1
                # Trigger the DFS to sink the rest of the island
                dfs(r, c)
                
    return islands
```

## Step 4: Hints & Discussion

**Interviewer:** "Code looks great. What if the interviewer asked you NOT to mutate the input array? Say this grid is being used by other threads in our system."

**Candidate:** "In that case, I would create a `visited` Set to track the coordinates `(r, c)` of cells we've already explored. In the DFS base case, I'd check `if (r, c) in visited: return`. The Space Complexity would still be bounded by $O(M \times N)$."

**Interviewer:** "Perfect. And what if the grid is massive, like 10,000 by 10,000, and it's mostly land?"

**Candidate:** "Ah, in Python, the recursive DFS might hit the recursion limit and throw a `RecursionError`. If we expect massive grids, I would rewrite the DFS using an iterative Stack, or use BFS with a `collections.deque` to avoid the call stack overhead."

**Interviewer:** "Awesome answers. Strong Hire."

---

## Interviewer Rubric Notes

- **Problem Solving:** Standard DFS matrix pattern.
- **Coding:** Very clean nested DFS function, nice use of closure to access `grid`, `rows`, and `cols` without passing them explicitly.
- **Verification:** Handled edge cases immediately.
- **Communication:** Correctly identified the dangers of mutating shared state and Python's recursion limit.
