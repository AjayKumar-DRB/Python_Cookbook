# Custom Sorting (`key` argument)

## Introduction

By default, Python sorts numbers ascending and strings alphabetically. 

However, interview questions frequently require complex sorting logic (e.g., sorting intervals by their start time, or strings by their length). Python handles this elegantly via the `key` argument.

---

## The `key` Argument

Both `list.sort()` and `sorted()` accept a `key` keyword argument. 

You provide a function (usually a `lambda`) to this argument. Python will call this function on every element and sort the elements based on the **return value** of that function.

### Example: Sorting by Length
```python
words = ["banana", "apple", "kiwi", "pear"]

# Sort by the length of the string
words.sort(key=len)
print(words) # ['kiwi', 'pear', 'apple', 'banana']
```

---

## Sorting Objects and Sub-Arrays

When given an array of arrays (like intervals) or tuples, you often need to sort by a specific index.

### Example: Merge Intervals
```python
intervals = [[1, 3], [8, 10], [2, 6], [15, 18]]

# Sort by the start time (index 0)
intervals.sort(key=lambda x: x[0])

print(intervals) # [[1, 3], [2, 6], [8, 10], [15, 18]]
```
*(Note: You can also use `operator.itemgetter(0)` which is slightly faster than the lambda, but the lambda is universally understood).*

---

## Multi-Criteria Sorting

If you need to sort by a primary condition, and then a secondary condition (in case of a tie), your `key` function should return a **tuple**.

Python sorts tuples element by element. 

### Example: Sorting Students
Sort students by Grade (A is better than B), and if grades tie, sort by Age (younger first).

```python
students = [
    {"name": "Alice", "grade": "B", "age": 20},
    {"name": "Bob", "grade": "A", "age": 22},
    {"name": "Charlie", "grade": "A", "age": 19}
]

students.sort(key=lambda s: (s["grade"], s["age"]))

# Charlie comes before Bob because they tie on 'A', but 19 < 22
print(students)
```

### Reversing Specific Criteria
What if you want descending grades, but ascending ages? 

For numbers, you simply negate the value (`-`).
```python
# Sort Age descending, Grade ascending
students.sort(key=lambda s: (s["grade"], -s["age"]))
```

For strings, negation doesn't work. Instead of complex `cmp_to_key` workarounds, you can take advantage of Python's **stable sorting** (explained in the next section) by sorting twice!

---

## Summary
- Use `key=lambda x: ...` to customize sort order.
- To sort by multiple criteria, return a tuple: `key=lambda x: (x.primary, x.secondary)`.
- Negate numbers `-x` to reverse the sort order for a specific criteria within a tuple.
