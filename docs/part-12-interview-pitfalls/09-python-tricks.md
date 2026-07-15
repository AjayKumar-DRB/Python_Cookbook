# Python Tricks

## 1. Multiple Assignment (Swapping)

In most languages, swapping two variables requires a temporary variable. In Python, you can do it in one line using tuple packing and unpacking.

```python
# The Old Way
temp = a
a = b
b = temp

# The Pythonic Way
a, b = b, a
```
*Application*: In-place array reversals, QuickSort partition functions, or swapping pointers in a Linked List.

---

## 2. Unpacking with `*`

You can use the `*` operator to unpack the "rest" of an iterable into a list. This is amazing for dealing with variable-length data.

```python
record = ("Alice", "alice@test.com", "555-1234", "555-9876")

name, email, *phone_numbers = record

print(name)          # Alice
print(phone_numbers) # ['555-1234', '555-9876']
```

---

## 3. Simultaneous Loop Iteration

If you need to iterate through two arrays at the same time, never use an index loop. Use `zip`.

```python
names = ["Alice", "Bob"]
scores = [90, 85]

for name, score in zip(names, scores):
    print(f"{name}: {score}")
```
*Application*: Comparing two arrays element-by-element (e.g., checking if two strings are isomorphic).

---

## 4. Chained Comparisons

Python allows you to chain comparison operators, exactly how you would write them in mathematics.

```python
# The Old Way
if x > 0 and x < 10:
    pass

# The Pythonic Way
if 0 < x < 10:
    pass
```
*Application*: Boundary checking in matrices or ensuring values fall within a specific range.

---

## 5. Default Dictionary Values (`.get()`)

When counting frequencies, trying to increment a key that doesn't exist throws a `KeyError`. Instead of writing an `if/else` block, use `.get()`.

```python
counts = {}

for char in "hello":
    # If char isn't in dict, return 0, then add 1
    counts[char] = counts.get(char, 0) + 1
```
*(Note: Using `collections.Counter` or `collections.defaultdict(int)` is usually better, but if the interviewer restricts you to standard dictionaries, use `.get()`).*

---

## 6. Slicing Magic

Python's slicing syntax `[start:stop:step]` is incredibly powerful.

```python
nums = [1, 2, 3, 4, 5]

# Reverse a list or string
print(nums[::-1]) # [5, 4, 3, 2, 1]

# Copy a list (Crucial for Backtracking!)
copy_nums = nums[:] 

# Get every other element (Even indices)
print(nums[::2]) # [1, 3, 5]
```
