# Dictionary Comprehensions

## Introduction

Just like list comprehensions, Python supports **dictionary comprehensions**. They allow you to construct dictionaries dynamically and concisely in a single line.

In interviews, they are frequently used to quickly build reverse mappings (mapping values to keys) or to filter existing dictionaries.

---

## The Syntax

The syntax is very similar to list comprehensions, but uses curly braces `{}` and a colon `:` to separate the key and value.

`{key_expr: value_expr for item in iterable}`

### Example: Squaring Numbers
```python
nums = [1, 2, 3, 4]
squares = {n: n*n for n in nums}

print(squares) # {1: 1, 2: 4, 3: 9, 4: 16}
```

---

## Reverse Mapping (Value to Key)

A very common interview pattern is needing to reverse a mapping. For example, you might have a dictionary mapping IDs to Names, but you need to look up an ID by Name.

Assuming all values are unique, a dictionary comprehension makes this trivial.

```python
id_to_name = {101: "Alice", 102: "Bob", 103: "Charlie"}

# Reverse the dictionary
name_to_id = {name: id for id, name in id_to_name.items()}

print(name_to_id["Bob"]) # 102
```

---

## Filtering a Dictionary

You can add an `if` condition at the end of the comprehension to filter elements.

```python
scores = {"Alice": 85, "Bob": 92, "Charlie": 78}

# Keep only scores >= 85
high_scores = {name: score for name, score in scores.items() if score >= 85}

print(high_scores) # {'Alice': 85, 'Bob': 92}
```

---

## Building from Two Lists using `zip()`

You will often be given two parallel arrays and asked to process them. You can use `zip()` within a dictionary comprehension, though calling `dict(zip(...))` is usually faster and cleaner.

```python
keys = ["a", "b", "c"]
values = [1, 2, 3]

# Using a comprehension (allows for transformation/filtering)
my_dict = {k: v * 2 for k, v in zip(keys, values)}
print(my_dict) # {'a': 2, 'b': 4, 'c': 6}

# Using dict() directly (best if no transformation needed)
simple_dict = dict(zip(keys, values))
```

---

## Time and Space Complexity

- **Time Complexity**: $O(N)$ where $N$ is the number of items being iterated over.
- **Space Complexity**: $O(N)$ to allocate the new dictionary in memory.

---

## Summary
- Use `{k: v for k, v in iterable}` to build dictionaries dynamically.
- Use `{v: k for k, v in my_dict.items()}` to instantly reverse a dictionary.
- You can filter key-value pairs by adding `if condition` at the end.
