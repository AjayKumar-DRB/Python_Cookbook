# Recursion Interview Recipes

> A quick-reference guide to the standard recursive templates you need to memorize.

---

## 1. Top-Down DFS (Global State)

Use this when you need to traverse a tree or graph and keep track of some global maximum, minimum, or sum.

```python
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        self.max_d = 0
        
        def dfs(node, depth):
            if not node:
                return
            
            self.max_d = max(self.max_d, depth)
            
            dfs(node.left, depth + 1)
            dfs(node.right, depth + 1)
            
        dfs(root, 1)
        return self.max_d
```

---

## 2. Bottom-Up DFS (Returning State)

Use this when the current node's answer depends directly on the answers from its children. This is the cleanest and most common tree template.

```python
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
            
        left_depth = self.maxDepth(root.left)
        right_depth = self.maxDepth(root.right)
        
        return 1 + max(left_depth, right_depth)
```

---

## 3. Standard Backtracking (Combinations/Subsets)

Use this when generating all possible valid combinations, permutations, or paths. Remember to `.copy()` the path when adding it to the result array.

```python
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        res = []
        path = []
        
        def backtrack(i):
            if i >= len(nums):
                res.append(path.copy())
                return
                
            # Decision 1: Include nums[i]
            path.append(nums[i])
            backtrack(i + 1)
            
            # Decision 2: Do NOT include nums[i]
            path.pop() # Backtrack!
            backtrack(i + 1)
            
        backtrack(0)
        return res
```

---

## 4. Top-Down Dynamic Programming (Memoization)

Use this when a recursive tree has overlapping subproblems (the same function arguments are evaluated multiple times).

```python
class Solution:
    def climbStairs(self, n: int) -> int:
        memo = {}
        
        def dfs(i):
            if i > n:
                return 0
            if i == n:
                return 1
            if i in memo:
                return memo[i]
                
            # Compute and store in memo
            memo[i] = dfs(i + 1) + dfs(i + 2)
            return memo[i]
            
        return dfs(0)
```

---

## Key Takeaways

- Almost all recursive interview problems use one of these four templates.
- **Top-Down DFS** passes state down.
- **Bottom-Up DFS** bubbles state up.
- **Backtracking** adds to state, recurses, and pops state.
- **Memoization** checks a cache before recursing and caches results after recursing.
