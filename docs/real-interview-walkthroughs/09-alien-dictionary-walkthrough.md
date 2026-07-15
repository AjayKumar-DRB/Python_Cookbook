# Walkthrough: Alien Dictionary

> **Difficulty:** Hard
> **Pattern:** Graph / Topological Sort

---

## The Prompt

**Interviewer:** "There is a new alien language that uses the English alphabet. However, the order of the letters is unknown to you. You are given a list of strings `words` from the alien language's dictionary, where the strings in `words` are sorted lexicographically by the rules of this new language. Return a string of the unique letters in the new alien language sorted in lexicographically increasing order. If there is no valid ordering, return `""`."

## Step 1: Understand & Clarify

**Candidate:** "Okay, so the words are sorted. This means if I have `words = ["wrt", "wrf"]`, because they share the prefix `wr`, the first differing character tells me the order. Here, `t` must come before `f` in this alphabet."

**Interviewer:** "Exactly."

**Candidate:** "What if a longer word comes before a shorter prefix? Like `["abcd", "abc"]`?"

**Interviewer:** "That would be an invalid dictionary according to normal lexicographical rules, so you should return `""`."

## Step 2: Match & Plan

**Candidate:** "This is about determining the order of items based on dependencies (`t` must come before `f`). This is the classic signature of a **Topological Sort** on a Directed Graph."

**Interviewer:** "How will you build the graph?"

**Candidate:** "The nodes are the unique characters. The directed edges are the dependencies. I'll compare adjacent words. I find the first character that differs, and add a directed edge `char1 -> char2`. Then I can use Depth-First Search (DFS) with a cycle detection mechanism to do the topological sort. If I detect a cycle (e.g., `a -> b -> c -> a`), there is no valid ordering, and I return `""`."

**Interviewer:** "Complexity?"

**Candidate:** "Time Complexity is $O(C)$ where $C$ is the total number of characters in all words combined, because we iterate through the words to build the graph, and the graph has at most 26 nodes and edges. Space is $O(1)$ since the alphabet size is bounded to 26 characters."

## Step 3: Implement

**Candidate:** "First, I'll initialize my Adjacency List for the graph, ensuring every unique character has an entry."

```python
def alienOrder(words: list[str]) -> str:
    adj = {c: set() for w in words for c in w}
```

**Candidate:** "Now I'll build the graph by comparing adjacent words."

```python
    for i in range(len(words) - 1):
        w1, w2 = words[i], words[i + 1]
        min_len = min(len(w1), len(w2))
        
        # Edge case: invalid dictionary like ["abcd", "abc"]
        if len(w1) > len(w2) and w1[:min_len] == w2[:min_len]:
            return ""
            
        # Find the first differing character
        for j in range(min_len):
            if w1[j] != w2[j]:
                adj[w1[j]].add(w2[j])
                break # Only the first difference matters!
```

**Candidate:** "Now for the Topological Sort using DFS. I need to track nodes as `visited` (added to result) and `visiting` (currently in the recursion stack, to detect cycles)."

```python
    visited = {} # char -> bool (False = visited, True = visiting cycle)
    res = []
    
    def dfs(char):
        if char in visited:
            return visited[char] # Returns True if cycle detected
            
        visited[char] = True # Mark as currently visiting
        
        for neighbor in adj[char]:
            if dfs(neighbor):
                return True # Cycle detected downstream
                
        visited[char] = False # Finished visiting
        res.append(char) # Add to post-order result
        return False
```

**Candidate:** "Finally, I'll call DFS on every unvisited node. If any call returns True (cycle), I return `""`. Since DFS builds a post-order traversal, I need to reverse the result at the end."

```python
    for char in adj:
        if dfs(char):
            return ""
            
    res.reverse()
    return "".join(res)
```

## Step 4: Discussion

**Interviewer:** "Beautiful. The cycle detection logic using `visited = True/False` is very clean. Could we have used Kahn's Algorithm (BFS with In-Degrees) instead?"

**Candidate:** "Yes. We would calculate the in-degree of every character. We put all characters with `in-degree == 0` in a Queue. We pop them, add them to the result, and decrement the in-degree of their neighbors. If a neighbor hits `0`, we add it to the Queue. At the end, if the length of the result string doesn't equal the number of unique characters, we know there was a cycle."

**Interviewer:** "Spot on. Excellent work."

---

## Interviewer Rubric Notes

- **Problem Solving:** Recognized Topological Sort. Handled the `["abcd", "abc"]` edge case perfectly.
- **Coding:** Very clean 3-state DFS for cycle detection.
- **Communication:** Able to clearly explain the alternative BFS (Kahn's) approach when prompted.
