# `iter()` and `next()`

## Introduction

Every time you write a `for` loop in Python, it uses `iter()` and `next()` under the hood. 

While you rarely need to call them manually in standard algorithmic questions, they are critical for object-oriented design questions, specifically when asked to "Design an Iterator" (e.g., LeetCode 284: Peeking Iterator or LeetCode 173: Binary Search Tree Iterator).

---

## How Iteration Works

When you run `for item in sequence:`, Python does two things:
1. It calls `iter(sequence)` to get an **iterator object**.
2. It repeatedly calls `next(iterator)` to get elements until a `StopIteration` exception is raised.

### Manual Iteration
You can do this manually:

```python
nums = [1, 2, 3]

# Get the iterator
iterator = iter(nums)

# Advance manually
print(next(iterator)) # 1
print(next(iterator)) # 2
print(next(iterator)) # 3

# print(next(iterator)) # Raises StopIteration
```

---

## Providing a Default to `next()`

If you call `next()` and the iterator is empty, it raises `StopIteration`. 

To prevent the exception and instead return a default value, pass a second argument to `next()`.

```python
iterator = iter([])

# Avoids exception, returns None
val = next(iterator, None)
print(val) # None
```

---

## Interview Application: Designing an Iterator

If an interviewer asks you to build a custom iterator, you must implement the `__iter__` and `__next__` magic methods.

```python
class EvenNumbers:
    def __init__(self, limit):
        self.limit = limit
        self.current = 0
        
    def __iter__(self):
        # Must return the iterator object itself
        return self
        
    def __next__(self):
        if self.current > self.limit:
            raise StopIteration
            
        result = self.current
        self.current += 2
        return result

# Now we can use our custom class in a for loop!
evens = EvenNumbers(6)
for num in evens:
    print(num)
# 0, 2, 4, 6
```

---

## Summary
- `iter(obj)` gets an iterator from an iterable.
- `next(iterator, default)` fetches the next item, raising `StopIteration` (or returning the default) when exhausted.
- To design a custom iterable object, implement `__iter__` and `__next__`.
