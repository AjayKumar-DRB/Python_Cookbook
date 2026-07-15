# Sorting Interview Recipes

## Introduction

Sorting is the gateway to $O(N \log N)$ solutions. These recipes cover the most common interview patterns that rely on Python's sorting capabilities.

---

## Recipe 1: Merge Intervals

This is one of the most frequently asked questions in FAANG interviews (e.g., LeetCode 56). Always sort the intervals by their start time first.

```python
def merge_intervals(intervals):
    if not intervals:
        return []
        
    # Sort by start time
    intervals.sort(key=lambda x: x[0])
    
    merged = [intervals[0]]
    
    for current in intervals[1:]:
        last_merged = merged[-1]
        
        # If the current interval overlaps with the last merged
        if current[0] <= last_merged[1]:
            # Merge them by updating the end time
            last_merged[1] = max(last_merged[1], current[1])
        else:
            # No overlap, add to results
            merged.append(current)
            
    return merged
```
- **Time Complexity**: $O(N \log N)$ (dominated by the sort).
- **Space Complexity**: $O(N)$ for Timsort overhead and the output array.

---

## Recipe 2: Grouping Anagrams

Two strings are anagrams if they are identical when sorted. You can use `sorted()` to create a normalized key for a dictionary.

```python
from collections import defaultdict

def group_anagrams(strs):
    groups = defaultdict(list)
    
    for s in strs:
        # sorted() returns a list, must convert to tuple for dict key
        key = tuple(sorted(s))
        groups[key].append(s)
        
    return list(groups.values())
```
- **Time Complexity**: $O(N \times K \log K)$ where $N$ is strings, $K$ is max string length.

---

## Recipe 3: Kth Largest Element (Without Heap)

While a Min-Heap is usually optimal ($O(N \log K)$), simply sorting the array and grabbing the Kth element from the end is perfectly acceptable and takes exactly 1 line of code ($O(N \log N)$).

```python
def find_kth_largest(nums, k):
    nums.sort()
    return nums[-k]
```

---

## Recipe 4: Sorting a Dictionary by Value

Dictionaries are inherently ordered by keys (insertion order). If you need to sort a dictionary's items by their *values*, use `sorted()` on the `.items()`.

```python
counts = {"apple": 5, "banana": 2, "cherry": 10}

# items() returns (key, value) tuples. We sort by index 1 (the value).
sorted_counts = sorted(counts.items(), key=lambda x: x[1], reverse=True)

print(sorted_counts) 
# [('cherry', 10), ('apple', 5), ('banana', 2)]
```

---

## Summary
- **Intervals**: `intervals.sort(key=lambda x: x[0])`
- **Anagrams**: `tuple(sorted(string))` as a dictionary key.
- **Dict Values**: `sorted(my_dict.items(), key=lambda x: x[1])`.
