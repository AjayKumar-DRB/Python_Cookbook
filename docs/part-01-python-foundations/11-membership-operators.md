# Membership Operators (`in` and `not in`)

> *"The fastest code is the code you don't have to execute."*

### Introduction

The membership operators `in` and `not in` are among the most frequently used operators in Python.

At first glance, they appear simple—they check whether a value exists in a collection.

However, what many candidates overlook is that **the performance of `in` depends entirely on the underlying data structure**.

Understanding this distinction can be the difference between an accepted solution and a Time Limit Exceeded (TLE) error.

---

## Syntax

```python
value in collection

value not in collection
```

The expression returns a boolean.

```python
nums = [1, 2, 3]

print(2 in nums)
```

Output

```python
True
```

---

## Membership in Lists

Lists perform a **linear search**.

```python
nums = [5, 10, 15, 20]

print(15 in nums)
```

Python checks each element one by one until it finds a match.

Time Complexity

| Case | Complexity |
|------|------------|
| Best | O(1) |
| Average | O(n) |
| Worst | O(n) |

---

### Why?

Suppose the element is at the end.

```
[5] → [10] → [15] → [20]
```

Python must inspect every previous element first.

---

## Membership in Strings

Strings also perform a linear search.

```python
text = "interview"

print("view" in text)
```

Output

```python
True
```

Time Complexity

| Case | Complexity |
|------|------------|
| Average | O(n) |
| Worst | O(n) |

---

## Membership in Tuples

Tuples behave similarly to lists.

```python
point = (10, 20, 30)

20 in point
```

Time Complexity

```
O(n)
```

---

## Membership in Sets

Sets are implemented using **hash tables**.

```python
visited = {2, 5, 8}

print(5 in visited)
```

Time Complexity

| Case | Complexity |
|------|------------|
| Average | O(1) |
| Worst | O(n) |

Average lookup is extremely fast because Python computes a hash and jumps directly to the expected location.

---

## Membership in Dictionaries

By default, membership checks **keys**, not values.

```python
student = {
    "name": "Alice",
    "age": 20
}

print("name" in student)
```

Output

```python
True
```

---

This does **not** search the values.

```python
20 in student
```

Output

```python
False
```

To search values:

```python
20 in student.values()
```

---

Time Complexity

| Operation | Complexity |
|-----------|------------|
| Key Lookup | O(1) Average |
| Value Lookup | O(n) |

---

## Complexity Comparison

| Data Structure | Average Time |
|---------------|--------------|
| List | O(n) |
| Tuple | O(n) |
| String | O(n) |
| Set | O(1) |
| Dictionary Keys | O(1) |
| Dictionary Values | O(n) |

This table alone is worth memorizing for interviews.

---

## Common Interview Pattern

Instead of

```python
for num in nums:
    if num in seen_list:
        return True

    seen_list.append(num)
```

Time Complexity

```
O(n²)
```

---

Use a set.

```python
seen = set()

for num in nums:
    if num in seen:
        return True

    seen.add(num)
```

Time Complexity

```
O(n)
```

This optimization appears in dozens of LeetCode problems.

---

## Converting a List to a Set

Sometimes the fastest solution is simply:

```python
lookup = set(nums)
```

Now every lookup becomes approximately O(1).

Example

```python
nums = [4, 8, 10, 15]

lookup = set(nums)

print(10 in lookup)
```

---

## When Not to Use a Set

A set is not always the best choice.

Avoid it when:

- Order matters
- Duplicate values are required
- Index-based access is needed

Use a list instead.

---

## Common Interview Problems

Membership testing appears in:

- Contains Duplicate
- Two Sum
- Happy Number
- Longest Consecutive Sequence
- Valid Sudoku
- Word Break
- Graph Traversal
- DFS
- BFS

---

## Common Mistakes

### Mistake 1

Using a list for repeated lookups.

```python
if target in nums:
```

inside a loop often results in O(n²) time.

---

### Mistake 2

Forgetting that dictionary membership checks keys.

```python
5 in scores
```

checks keys, **not values**.

---

### Mistake 3

Creating a set inside a loop.

```python
for num in nums:
    lookup = set(nums)
```

This repeatedly rebuilds the hash table and destroys performance.

Create it once before the loop.

---

### Mistake 4

Using a set when duplicates matter.

```python
set([1, 1, 2, 2])
```

Output

```python
{1, 2}
```

Duplicates are removed.

---

## Best Practices

- Prefer sets for frequent membership checks.
- Remember that dictionaries check keys by default.
- Convert lists to sets when many lookups are required.
- Avoid rebuilding sets inside loops.
- Choose the data structure based on the required operations, not habit.

---

## Key Takeaways

- `in` behaves differently depending on the data structure.
- List, tuple, and string membership are linear.
- Set and dictionary key lookups are constant time on average.
- Converting a list to a set is a common interview optimization.
- Understanding lookup complexity is more important than memorizing syntax.

---

## Related Topics

- Dictionaries
- Sets
- Hash Tables
- Time Complexity
- Common Interview Patterns

---

## Practice Questions

1. Why is `target in nums` slower for a list than for a set?
2. What does `"age" in person` check?
3. Why is `20 in person` different from `20 in person.values()`?
4. When should you convert a list into a set?
5. Why can using a list for repeated membership checks lead to O(n²) solutions?

---

## Summary

The `in` operator may look simple, but its efficiency depends entirely on the underlying data structure.

Choosing the right collection for membership testing is one of the easiest ways to optimize an interview solution. Whenever you find yourself performing repeated lookups, pause and ask:

> **"Would a set or dictionary make this faster?"**

That single question can often reduce an algorithm from **O(n²)** to **O(n)**.
