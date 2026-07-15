# `filter()`

## Introduction

The `filter()` function constructs a **lazy iterator** from elements of an iterable for which a function returns `True`.

Like `map()`, `filter()` has largely been superseded by list comprehensions in modern Python, but you should know how it works in case you encounter it or need a functional programming approach.

---

## Basic Usage

`filter(function, iterable)`

```python
nums = [1, 2, 3, 4, 5, 6]

def is_even(n):
    return n % 2 == 0

# Returns a lazy iterator
evens = filter(is_even, nums)

# Wrap in list() to compute
print(list(evens)) # [2, 4, 6]
```

### Filtering Falsy Values
If you pass `None` as the function, `filter()` will automatically remove any "falsy" values (`0`, `""`, `False`, `None`, `[]`) from the iterable.

```python
data = [1, 0, 2, "", 3, None, 4]

truthy_only = list(filter(None, data))
print(truthy_only) # [1, 2, 3, 4]
```

---

## When to AVOID `filter()` in Interviews

Just like `map()`, if you have to write a `lambda` to use `filter()`, you should use a list comprehension instead. Comprehensions with `if` clauses are faster and more readable.

**Avoid this:**
```python
nums = [1, 2, 3, 4, 5, 6]
evens = list(filter(lambda x: x % 2 == 0, nums))
```

**Write this instead:**
```python
evens = [x for x in nums if x % 2 == 0]
```

---

## Time and Space Complexity

- **Time Complexity**: $O(N)$ once consumed.
- **Space Complexity**: $O(1)$ memory overhead for the iterator itself.

---

## Summary
- `filter()` creates an iterator of elements that pass a boolean function.
- `filter(None, iterable)` is a quick trick to remove falsy values.
- In almost all other cases in an interview, use a list comprehension with an `if` clause instead.
