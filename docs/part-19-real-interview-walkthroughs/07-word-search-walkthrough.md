# Walkthrough: Word Search

> **Difficulty:** Medium (Often considered Hard)
> **Pattern:** Backtracking / Matrix DFS

---

## The Prompt

**Interviewer:** "Given an $M \times N$ grid of characters `board` and a string `word`, return `true` if `word` exists in the grid. The word can be constructed from letters of sequentially adjacent cells (horizontal or vertical). The same letter cell may not be used more than once in a word."

## Step 1: Understand & Clarify

**Candidate:** "Okay, so we are searching for a specific path of letters. We can move up, down, left, right, but we can't revisit a cell we've already used for the *current* word."

**Interviewer:** "Correct."

**Candidate:** "Can the board contain duplicates of the same letter?"

**Interviewer:** "Yes, it can be a board full of 'A's."

**Candidate:** "Okay. Since we can't reuse a cell in the same path, I'll need a way to track visited cells. I can use a `path` Set."

## Step 2: Match & Plan

**Candidate:** "This sounds like **Backtracking**. We can scan the board. Whenever we find a character that matches the first letter of our `word`, we trigger a DFS. The DFS will explore paths, adding coordinates to a `path` Set. If a path fails (we hit a wrong letter or out of bounds), we backtrack—we return `False` and remove the coordinate from the `path` Set so it can be used by other potential paths."

**Interviewer:** "What is the Time Complexity?"

**Candidate:** "We scan the board, which is $O(M \times N)$. In the worst case, from every cell, we explore a tree with 3 branches (we don't go backwards), and the depth is the length of the word $L$. So it's $O(M \times N \times 3^L)$."

**Interviewer:** "That's correct. Let's write it."

## Step 3: Implement

**Candidate:** "I'll grab the dimensions and initialize my set."

```python
def exist(board: list[list[str]], word: str) -> bool:
    ROWS, COLS = len(board), len(board[0])
    path = set()
```

**Candidate:** "Now the DFS helper. It needs the current row `r`, current column `c`, and the `i`-th character of the word we are looking for."

```python
    def dfs(r, c, i):
        # Base Case 1: We found all characters!
        if i == len(word):
            return True
            
        # Base Case 2: Out of bounds, wrong letter, or already visited
        if (r < 0 or c < 0 or 
            r >= ROWS or c >= COLS or
            word[i] != board[r][c] or 
            (r, c) in path):
            return False
```

**Candidate:** "If we pass the base cases, it means we found a valid character! We add it to our path."

```python
        path.add((r, c))
```

**Candidate:** "Then we recursively check all 4 neighbors for the NEXT character `i + 1`. If ANY of them return True, we found the word."

```python
        res = (dfs(r + 1, c, i + 1) or
               dfs(r - 1, c, i + 1) or
               dfs(r, c + 1, i + 1) or
               dfs(r, c - 1, i + 1))
```

**Candidate:** "CRITICAL STEP: We must backtrack. We remove the cell from our path so other branches can potentially use it later. Then we return the result."

```python
        path.remove((r, c))
        return res
```

**Candidate:** "Now the outer loop. We just scan the board for the first letter and trigger DFS."

```python
    for r in range(ROWS):
        for c in range(COLS):
            if dfs(r, c, 0): return True
            
    return False
```

## Step 4: Hints & Discussion

**Interviewer:** "Excellent structure. The `path` set takes $O(L)$ space. Can we do this in $O(1)$ extra space?"

**Candidate:** "Yes! Instead of using a Set, we can mutate the board. When we visit a cell, we temporarily change `board[r][c]` to something invalid like `'#'`. After the recursive calls finish (the backtrack step), we restore it back to `word[i]`. This avoids the Hash Set overhead entirely."

**Interviewer:** "Perfect optimization."

---

## Interviewer Rubric Notes

- **Problem Solving:** Clean Backtracking logic.
- **Coding:** Handled the `path.add()` and `path.remove()` perfectly around the recursive calls. This is where most candidates fail.
- **Communication:** Correctly stated the complex time complexity $O(N \cdot 3^L)$, noting that we don't branch back the way we came.
