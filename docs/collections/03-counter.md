# `collections.Counter`

## Introduction

`Counter` is a subclass of `dict` designed specifically for counting hashable objects. It is the definitive tool for building frequency maps in Python interviews.

---

## Creating a Counter

You can initialize a `Counter` by passing it an iterable. It automatically counts the occurrences of each element in $O(N)$ time.

```python
from collections import Counter

# Counting characters in a string
chars = Counter("hello")
print(chars) # Counter({'l': 2, 'h': 1, 'e': 1, 'o': 1})

# Counting elements in a list
nums = Counter([1, 2, 2, 3])
print(nums) # Counter({2: 2, 1: 1, 3: 1})
```

---

## Missing Keys Return 0

Unlike standard dictionaries which raise a `KeyError` if a key is missing, a `Counter` gracefully returns `0`. This makes it incredibly easy to use when checking frequencies.

```python
counts = Counter("apple")

print(counts["p"]) # 2
print(counts["z"]) # 0 (No KeyError!)
```

---

## The `most_common()` Method

If a problem asks for the "Top K" frequent elements, `Counter` has a built-in method `most_common(k)`.

It returns a list of `(element, frequency)` tuples, sorted from most to least frequent.

```python
counts = Counter("abracadabra")

# Get the top 2 most frequent characters
top_two = counts.most_common(2)
print(top_two) # [('a', 5), ('r', 2)]
```
- **Time Complexity**: $O(N \log K)$ because it uses a heap under the hood.

---

## Counter Math (Multisets)

`Counter` objects support mathematical operations, making them act like mathematical multisets. This is useful for problems involving anagrams or string building.

```python
c1 = Counter("aab")
c2 = Counter("abb")

# Addition (combines counts)
print(c1 + c2) # Counter({'a': 3, 'b': 3})

# Subtraction (removes counts, drops negative/zero values)
print(c1 - c2) # Counter({'a': 1})

# Intersection (min of counts)
print(c1 & c2) # Counter({'a': 1, 'b': 1})

# Union (max of counts)
print(c1 | c2) # Counter({'a': 2, 'b': 2})
```

---

## Time and Space Complexity

- **Time Complexity**: $O(N)$ to initialize from an iterable.
- **Space Complexity**: $O(U)$ where $U$ is the number of unique elements.

---

## Summary
- `Counter` automates frequency mapping in $O(N)$ time.
- Missing keys return `0` instead of a `KeyError`.
- Use `most_common(k)` to quickly find the top K frequent elements.
- You can add, subtract, and intersect `Counter` objects.
