# `map()`

## Introduction

The `map()` function applies a given function to every item of an iterable and returns a **lazy iterator**.

In modern Python, list comprehensions are generally preferred over `map()` because they are more readable, but `map()` is still heavily used in specific interview scenarios, particularly for parsing input.

---

## Basic Usage

`map(function, iterable)`

```python
nums = [1, 2, 3]

# Convert ints to strings
str_nums = map(str, nums)

# map() returns a lazy iterator, not a list!
print(str_nums) # <map object at 0x...>

# Wrap in list() to compute the results
print(list(str_nums)) # ['1', '2', '3']
```

---

## When to Use `map()` in Interviews

### 1. Parsing Multiple Inputs
If you are doing a HackerRank-style interview where you must read from `stdin`, `map()` is the standard way to parse a line of space-separated integers.

```python
# User inputs: "10 20 30"
line = input().split() 

# Clean, standard parsing
a, b, c = map(int, line) 
```

### 2. When the function is already defined
If you just need to apply an existing function (like `int`, `str`, or `len`), `map()` is slightly cleaner than a comprehension.

```python
words = ["apple", "banana", "cherry"]

# Using map (clean)
lengths = list(map(len, words))

# Using comprehension (fine, but slightly more verbose)
lengths = [len(w) for w in words]
```

---

## When to AVOID `map()` in Interviews

If you need to use a `lambda` inside a `map()`, you should almost always use a list comprehension instead. Python's creator, Guido van Rossum, explicitly designed comprehensions to replace `map(lambda)`.

**Avoid this:**
```python
nums = [1, 2, 3]
squares = list(map(lambda x: x**2, nums))
```

**Write this instead:**
```python
squares = [x**2 for x in nums]
```
The comprehension is faster, doesn't require a function call overhead, and is much easier to read.

---

## Time and Space Complexity

- **Time Complexity**: $O(N)$ once consumed (evaluated). $O(1)$ to create the iterator.
- **Space Complexity**: $O(1)$ memory overhead for the iterator itself.

---

## Summary
- `map()` applies a function to all items in an iterable.
- It returns a lazy iterator. You must call `list()` on it to get an array.
- Use it to cleanly parse string inputs into integers: `a, b = map(int, input().split())`.
- If you find yourself writing `map(lambda...)`, use a list comprehension instead.
