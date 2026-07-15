# Python Complexity Reference

> *"Choosing the right data structure is often more important than choosing the right algorithm."*

### Introduction

One of the fastest ways to improve your coding interview performance is to memorize the time and space complexity of Python's most commonly used operations.

Many interview questions can be optimized simply by replacing one data structure with another.

This reference serves as a quick lookup guide for the operations you'll encounter throughout this cookbook.

---

## Complexity Notation

| Symbol | Meaning |
|---------|----------|
| O(1) | Constant Time |
| O(log n) | Logarithmic Time |
| O(n) | Linear Time |
| O(n log n) | Efficient Sorting |
| O(n²) | Quadratic Time |
| O(2ⁿ) | Exponential Time |

---

## Python Lists

| Operation | Average | Worst |
|------------|---------|--------|
| Index (`nums[i]`) | O(1) | O(1) |
| Assignment | O(1) | O(1) |
| Append | O(1) | O(n) |
| Pop Last | O(1) | O(1) |
| Pop Front (`pop(0)`) | O(n) | O(n) |
| Insert Beginning | O(n) | O(n) |
| Insert Middle | O(n) | O(n) |
| Remove Value | O(n) | O(n) |
| Membership (`x in list`) | O(n) | O(n) |
| Copy | O(n) | O(n) |
| Slice | O(k) | O(k) |
| Reverse | O(n) | O(n) |
| Sort | O(n log n) | O(n log n) |

---

## Strings

| Operation | Complexity |
|------------|------------|
| Index | O(1) |
| Slice | O(k) |
| Concatenation (`+`) | O(n) |
| `"".join()` | O(n) |
| Membership | O(n) |
| `replace()` | O(n) |
| `split()` | O(n) |
| `strip()` | O(n) |
| `find()` | O(n) |
| `count()` | O(n) |
| `startswith()` | O(k) |
| `endswith()` | O(k) |
| `lower()` | O(n) |
| `upper()` | O(n) |

---

## Tuples

| Operation | Complexity |
|------------|------------|
| Index | O(1) |
| Membership | O(n) |
| Slice | O(k) |
| Copy | O(1) (reference) |

---

## Dictionaries

| Operation | Average | Worst |
|------------|---------|--------|
| Lookup | O(1) | O(n) |
| Insert | O(1) | O(n) |
| Delete | O(1) | O(n) |
| Membership (keys) | O(1) | O(n) |
| Membership (values) | O(n) | O(n) |
| Get | O(1) | O(n) |
| Pop | O(1) | O(n) |

---

## Sets

| Operation | Average | Worst |
|------------|---------|--------|
| Add | O(1) | O(n) |
| Remove | O(1) | O(n) |
| Membership | O(1) | O(n) |
| Union | O(len(a)+len(b)) | |
| Intersection | O(min(len(a), len(b))) | |
| Difference | O(len(a)) | |

---

## Deque (`collections.deque`)

| Operation | Complexity |
|------------|------------|
| Append Right | O(1) |
| Append Left | O(1) |
| Pop Right | O(1) |
| Pop Left | O(1) |
| Index | O(n) |
| Membership | O(n) |

---

## Heap (`heapq`)

| Operation | Complexity |
|------------|------------|
| `heapify()` | O(n) |
| `heappush()` | O(log n) |
| `heappop()` | O(log n) |
| Peek (`heap[0]`) | O(1) |

---

## Bisect

| Operation | Complexity |
|------------|------------|
| `bisect_left()` | O(log n) |
| `bisect_right()` | O(log n) |
| `insort_left()` | O(n) |
| `insort_right()` | O(n) |

> Searching is logarithmic, but insertion into a Python list still requires shifting elements.

---

## Counter

| Operation | Complexity |
|------------|------------|
| Build Counter | O(n) |
| Lookup Frequency | O(1) |
| Increment | O(1) |
| `most_common()` | O(n log n) |

---

## defaultdict

| Operation | Complexity |
|------------|------------|
| Lookup | O(1) |
| Insert | O(1) |
| Missing Key | O(1) |

---

## Sorting

| Function | Complexity |
|-----------|------------|
| `sorted()` | O(n log n) |
| `list.sort()` | O(n log n) |

Python uses **Timsort**, which is stable and highly optimized for partially sorted data.

---

## Built-in Functions

| Function | Complexity |
|-----------|------------|
| `len()` | O(1) |
| `min()` | O(n) |
| `max()` | O(n) |
| `sum()` | O(n) |
| `any()` | O(n) |
| `all()` | O(n) |
| `enumerate()` | O(1) to create |
| `zip()` | O(1) to create |
| `reversed()` | O(1) to create |

---

## Membership Summary

| Structure | Complexity |
|------------|------------|
| List | O(n) |
| Tuple | O(n) |
| String | O(n) |
| Set | O(1) Average |
| Dict Keys | O(1) Average |
| Dict Values | O(n) |

---

## Sorting Summary

| Algorithm | Complexity |
|------------|------------|
| Timsort (Python) | O(n log n) |
| Best Case | O(n) |
| Stable | ✅ |
| In-place | Mostly |

---

## Memory Usage (Approximate)

| Structure | Extra Memory |
|------------|--------------|
| List Copy | O(n) |
| Set | O(n) |
| Dictionary | O(n) |
| Heap | O(n) |
| Counter | O(n) |

---

## Most Important Complexities to Memorize

If you only remember ten operations, remember these:

| Operation | Complexity |
|------------|------------|
| List Index | O(1) |
| List Append | O(1) |
| List Pop(0) | O(n) |
| Set Lookup | O(1) |
| Dict Lookup | O(1) |
| Heap Push | O(log n) |
| Heap Pop | O(log n) |
| Binary Search | O(log n) |
| Sorting | O(n log n) |
| String Join | O(n) |

---

## Interview Tips

✅ Prefer `set` over `list` for repeated lookups.

✅ Use `deque` instead of `list.pop(0)`.

✅ Use `heapq` instead of sorting repeatedly.

✅ Convert repeated string concatenation into `"".join()`.

✅ Know the difference between **search complexity** and **insertion complexity**.

---

## Related Topics

- Lists
- Strings
- Dictionaries
- Sets
- Heap
- Deque
- Sorting
- Binary Search

---

## Summary

Mastering these complexity tables allows you to reason about algorithm performance before writing code.

During interviews, selecting the correct data structure is often the biggest optimization you can make. Keep this page bookmarked and revisit it frequently as you progress through the cookbook.
