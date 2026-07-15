# Dictionary Interview Recipes

## Introduction

Dictionaries are the primary tool for optimizing algorithms. Memorizing these dictionary-based recipes will allow you to quickly reduce $O(N^2)$ algorithms to $O(N)$.

---

## Recipe 1: Two Sum (Trading Space for Time)

If a problem asks you to find two numbers in an array that add up to a target, use a dictionary to store the numbers you have seen so far.

```python
def two_sum(nums, target):
    # Map: value -> index
    seen = {}
    
    for i, num in enumerate(nums):
        complement = target - num
        
        if complement in seen:
            return [seen[complement], i]
            
        seen[num] = i
        
    return []
```
- **Time Complexity**: $O(N)$
- **Space Complexity**: $O(N)$

---

## Recipe 2: Grouping Elements (Anagrams)

When asked to group similar elements together (like grouping strings that are anagrams of each other), use a dictionary where the **key is a normalized version of the element**, and the **value is a list of matching elements**.

```python
import collections

def group_anagrams(strs):
    # Map: sorted_tuple -> list of original strings
    groups = collections.defaultdict(list)
    
    for s in strs:
        # Normalize the string (sort it)
        # Must be a tuple because lists are not hashable!
        key = tuple(sorted(s))
        groups[key].append(s)
        
    return list(groups.values())
```
- **Time Complexity**: $O(N \times K \log K)$ where $N$ is number of strings, $K$ is max length.
- **Space Complexity**: $O(N \times K)$

---

## Recipe 3: Memoization (Caching Results)

In Dynamic Programming or recursive tree traversals, use a dictionary to cache the results of expensive function calls to avoid recalculating them.

```python
def fibonacci(n, memo=None):
    if memo is None:
        memo = {}
        
    if n in memo:
        return memo[n]
        
    if n <= 1:
        return n
        
    # Compute and store in memo before returning
    memo[n] = fibonacci(n-1, memo) + fibonacci(n-2, memo)
    return memo[n]
```
*(Note: Python provides `@functools.lru_cache` which does this automatically, but interviewers often want to see you implement it manually).*

---

## Recipe 4: Frequency Counting

When asked to find the most common element or check if two arrays are permutations, use `collections.Counter`.

```python
from collections import Counter

def top_k_frequent(nums, k):
    counts = Counter(nums)
    
    # most_common(k) returns a list of (element, frequency)
    return [elem for elem, freq in counts.most_common(k)]
```
- **Time Complexity**: $O(N \log K)$ (internal heap logic).
- **Space Complexity**: $O(N)$

---

## Summary
- **Two Sum Pattern**: Store `seen[value] = index` while iterating.
- **Grouping**: Use a normalized, immutable key (like a sorted tuple) to group items in a `defaultdict(list)`.
- **Memoization**: Pass a dictionary through recursive calls to cache `memo[state] = result`.
- **Top K**: Use `Counter(nums).most_common(k)`.
