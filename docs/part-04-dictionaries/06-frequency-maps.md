# Frequency Maps

## Introduction

A Frequency Map (or count dictionary) is the single most common use case for dictionaries in coding interviews. 

It is used to count the occurrences of elements in a sequence. You will use it to solve problems related to Anagrams, Majority Elements, Top K Frequent Elements, and Palindrome Permutations.

---

## Building a Frequency Map Manually

To build a frequency map, iterate over the sequence. If the element is already in the dictionary, increment its count. If it is not, add it with a count of 1.

### The Verbose Way (Avoid)
```python
nums = [1, 2, 2, 3, 3, 3]
counts = {}

for num in nums:
    if num in counts:
        counts[num] += 1
    else:
        counts[num] = 1
```

### The `get()` Way (Better)
Using the `get()` method with a default value of `0` makes this a clean one-liner inside the loop.

```python
counts = {}
for num in nums:
    counts[num] = counts.get(num, 0) + 1
```

---

## The Pythonic Way: `collections.Counter`

While building a frequency map manually using `get()` is fine, the most Pythonic and efficient way is to use the built-in `Counter` class from the `collections` module.

```python
from collections import Counter

nums = [1, 2, 2, 3, 3, 3]
counts = Counter(nums)

print(counts) # Counter({3: 3, 2: 2, 1: 1})
```

`Counter` is a subclass of `dict`, meaning it supports all standard dictionary operations, but it comes with specialized methods.

### Finding the Most Frequent Elements

If a problem asks for the "Top K" elements, `Counter` provides the `most_common(k)` method, which returns a list of `(element, count)` tuples.

```python
print(counts.most_common(2)) 
# [(3, 3), (2, 2)]
```

---

## When NOT to use a Dictionary

If the problem explicitly states that the input consists *only of lowercase English letters*, you should generally use a 26-element array instead of a dictionary.

```python
# Optimal frequency map for lowercase letters
counts = [0] * 26
for char in "hello":
    counts[ord(char) - ord('a')] += 1
```

**Why?**
A dictionary has a small memory overhead for the hash table structure. An array of fixed size 26 is strictly $O(1)$ space and avoids hashing entirely, making it slightly faster and more space-efficient.

---

## Time and Space Complexity

Building a frequency map (using `Counter` or `get()`):
- **Time Complexity**: $O(N)$ to iterate through the input sequence.
- **Space Complexity**: $O(U)$ where $U$ is the number of **unique** elements in the sequence. In the worst case (all elements unique), this is $O(N)$.

---

## Summary
- Frequency counting is a core interview pattern.
- Use `counts[num] = counts.get(num, 0) + 1` to count manually.
- Use `collections.Counter(nums)` for the cleanest and most Pythonic code.
- Use `Counter.most_common(k)` to quickly find the top frequencies.
- If input is strictly lowercase English letters, consider a 26-element array instead.
