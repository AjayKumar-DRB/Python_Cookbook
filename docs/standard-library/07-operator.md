# `operator` Module

## Introduction

The `operator` module exports a set of efficient functions corresponding to the intrinsic operators of Python (like `+`, `-`, `*`, `==`). 

In interviews, this module is mainly used as a cleaner alternative to writing `lambda` functions when you need to pass an operation as an argument to another function (like `sort()` or `reduce()`).

---

## Standard Math Operators

Instead of writing `lambda x, y: x + y`, you can pass `operator.add`.

```python
import operator
from functools import reduce

nums = [1, 2, 3, 4]

# Using lambda
sum1 = reduce(lambda x, y: x + y, nums)

# Using operator (cleaner and slightly faster)
sum2 = reduce(operator.add, nums)
```

Common mathematical operators:
- `operator.add` (`+`)
- `operator.sub` (`-`)
- `operator.mul` (`*`)
- `operator.truediv` (`/`)
- `operator.floordiv` (`//`)

---

## Item Getters

The most common use of the `operator` module in interviews is `itemgetter`. 

When sorting a list of tuples or dictionaries, you often need to sort by a specific index or key. `itemgetter` creates a fast, C-optimized callable that fetches that item.

```python
from operator import itemgetter

inventory = [
    ('apple', 3, 100),
    ('banana', 1, 50),
    ('orange', 2, 75)
]

# Sort by the 2nd element (quantity)
# Equivalent to: key=lambda x: x[1]
inventory.sort(key=itemgetter(1))
print(inventory)
# [('banana', 1, 50), ('orange', 2, 75), ('apple', 3, 100)]

# Sort by the 3rd element, then the 1st
inventory.sort(key=itemgetter(2, 0))
```

### When to use `itemgetter` vs `lambda`
For simple indices, `itemgetter(1)` is preferred because it is faster (executed entirely in C) and cleaner than `lambda x: x[1]`. However, if you need to perform any math or complex logic on the element before sorting, you must use a `lambda`.

---

## Summary
- Use `operator.add`, `mul`, etc., as arguments to `reduce()`.
- Use `operator.itemgetter(idx)` as the `key` function for sorting lists of tuples/lists.
- `itemgetter` is generally faster and cleaner than writing a `lambda` for simple index fetching.
