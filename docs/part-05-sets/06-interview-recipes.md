# Set Interview Recipes

## Introduction

Sets are straightforward but incredibly powerful. These recipes demonstrate how converting data into a set allows you to instantly optimize lookups or find overlapping elements.

---

## Recipe 1: $O(1)$ Lookups (Trading Space for Time)

If you have a list of valid or invalid items that you need to check against repeatedly in a loop, always convert that list to a set first.

```python
def count_vowels(s):
    # Convert string to a set for O(1) lookups
    vowels = set("aeiouAEIOU")
    count = 0
    
    for char in s:
        # O(1) check
        if char in vowels: 
            count += 1
            
    return count
```
- **Time Complexity**: $O(N)$ (where $N$ is string length). If `vowels` remained a string, the check would be $O(V)$, making total time $O(N \times V)$.
- **Space Complexity**: $O(V)$ (where $V$ is number of vowels).

---

## Recipe 2: Removing Duplicates

If a problem asks you to return the unique elements of an array and the order does not matter, use a set.

```python
def get_unique_elements(nums):
    return list(set(nums))
```
- **Time Complexity**: $O(N)$ to build the set and $O(U)$ to convert back to a list.
- **Space Complexity**: $O(U)$ where $U$ is unique elements.

---

## Recipe 3: Graph Traversal `visited` Set

In any BFS or DFS traversal on a general graph (or a matrix where you can move in 4 directions), use a `visited` set to prevent infinite loops. Always store tuples (coordinates), not lists.

```python
def bfs_grid(grid):
    R, C = len(grid), len(grid[0])
    visited = set()
    queue = [(0, 0)] # start at origin
    visited.add((0, 0))
    
    while queue:
        r, c = queue.pop(0)
        
        # Check neighbors
        for dr, dc in [(0, 1), (1, 0), (0, -1), (-1, 0)]:
            nr, nc = r + dr, c + dc
            
            # If valid and not visited
            if 0 <= nr < R and 0 <= nc < C and (nr, nc) not in visited:
                visited.add((nr, nc))
                queue.append((nr, nc))
```
- **Space Complexity**: $O(R \times C)$ to store coordinates.

---

## Recipe 4: Finding Common Elements

If asked to find elements that exist in two different arrays, convert the smaller array to a set, or use the `&` operator.

```python
def common_elements(arr1, arr2):
    # Convert both to sets and use Intersection
    return list(set(arr1) & set(arr2))
```
- **Time Complexity**: $O(N + M)$ to build sets.
- **Space Complexity**: $O(N + M)$

---

## Summary
- **$O(1)$ Lookups**: Always convert a list of "targets" into a set before doing repeated `in` checks.
- **Deduplication**: `list(set(nums))` instantly removes duplicates.
- **Visited Paths**: Use a `set` containing tuples to track visited coordinates in graphs/grids.
- **Intersection**: Use `set1 & set2` to find common elements efficiently.
