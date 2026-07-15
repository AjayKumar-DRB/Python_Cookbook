# Truthy and Falsy Values

> *"Readability counts."*  
> — **The Zen of Python**

### Introduction

In Python, every object has an associated truth value.

When an object is used in a conditional statement such as `if`, `while`, or with logical operators (`and`, `or`, `not`), Python automatically determines whether that object should be treated as **True** or **False**.

Understanding truthy and falsy values allows you to write cleaner, more Pythonic code and avoid unnecessary comparisons.

---

## What Are Truthy and Falsy Values?

A **truthy** value behaves like `True` in a boolean context.

A **falsy** value behaves like `False`.

For example,

```python
if [1, 2, 3]:
    print("List is not empty")
```

Output

```text
List is not empty
```

The list itself is not `True`, but it is considered **truthy** because it contains elements.

---

## Falsy Values

Python has only a small number of built-in falsy values.

| Value | Description |
|--------|-------------|
| `False` | Boolean false |
| `None` | Null object |
| `0` | Integer zero |
| `0.0` | Floating-point zero |
| `0j` | Complex zero |
| `""` | Empty string |
| `[]` | Empty list |
| `()` | Empty tuple |
| `{}` | Empty dictionary |
| `set()` | Empty set |
| `range(0)` | Empty range |

Everything else is generally considered truthy.

---

## Truthy Values

Examples of truthy values:

```python
1
-1
3.14
"Python"
[1, 2, 3]
{"name": "Alice"}
(10,)
{1, 2}
True
```

Each of these evaluates to `True` in a boolean context.

---

## Checking Empty Collections

Instead of writing

```python
if len(nums) > 0:
```

write

```python
if nums:
```

Likewise,

Instead of

```python
if len(queue) == 0:
```

write

```python
if not queue:
```

This is shorter, more readable, and considered Pythonic.

---

## Examples

### Lists

```python
numbers = []

if numbers:
    print("Not Empty")
else:
    print("Empty")
```

Output

```text
Empty
```

---

### Strings

```python
text = ""

if text:
    print("Has content")
else:
    print("Empty")
```

Output

```text
Empty
```

---

### Dictionaries

```python
student = {}

if student:
    print("Contains data")
else:
    print("Dictionary is empty")
```

Output

```text
Dictionary is empty
```

---

## Using `not`

The `not` operator reverses the truth value.

```python
numbers = []

if not numbers:
    print("Empty List")
```

Output

```text
Empty List
```

---

## Truthiness in Loops

A common interview pattern:

```python
stack = []

while stack:
    print(stack.pop())
```

The loop automatically stops when the list becomes empty.

No explicit length check is required.

---

## Truthiness with `and` and `or`

Python's logical operators return **objects**, not just `True` or `False`.

Example:

```python
print([] or "default")
```

Output

```text
default
```

Because the empty list is falsy.

---

Another example:

```python
print("Python" and 42)
```

Output

```text
42
```

The first operand is truthy, so `and` returns the second operand.

---

## Why This Matters in DSA

Many interview solutions rely on truthiness.

Examples:

Checking if a stack contains elements:

```python
if stack:
```

Checking whether BFS should continue:

```python
while queue:
```

Checking for an empty string:

```python
if not s:
```

Checking whether a dictionary has been populated:

```python
if visited:
```

These patterns appear in almost every coding interview.

---

## Time Complexity

Truth value testing is generally **O(1)** for Python's built-in data types.

Checking

```python
if nums:
```

does **not** iterate through the list.

---

## Common Interview Problems

Truthiness appears in:

- DFS
- BFS
- Stack problems
- Queue problems
- Binary Trees
- Linked Lists
- Dynamic Programming
- String processing

---

## Common Mistakes

### Mistake 1

Writing

```python
if len(nums) > 0:
```

Instead write

```python
if nums:
```

---

### Mistake 2

Writing

```python
if len(nums) == 0:
```

Instead write

```python
if not nums:
```

---

### Mistake 3

Comparing directly with `True`

```python
if flag == True:
```

Instead write

```python
if flag:
```

---

### Mistake 4

Comparing directly with `False`

```python
if flag == False:
```

Instead write

```python
if not flag:
```

---

## Best Practices

- Prefer truthiness over explicit length checks.
- Use `if not collection:` for empty collections.
- Use `while queue:` instead of checking the queue's length.
- Avoid comparing boolean values with `== True` or `== False`.

---

## Key Takeaways

- Every Python object has a truth value.
- Empty collections are falsy.
- Non-empty collections are truthy.
- `None` is falsy.
- Truthiness leads to cleaner and more idiomatic Python code.
- Most interview solutions rely heavily on truthy and falsy evaluation.

---

## Related Topics

- Type Conversion
- Operators Used in DSA
- Collections
- Stacks
- Queues

---

## Practice Questions

1. Which built-in values are considered falsy in Python?
2. Why is `if nums:` preferred over `if len(nums) > 0:`?
3. What does `not []` evaluate to?
4. What does `"Python" and 42` return?
5. What does `[] or "default"` return?

---

## Summary

Truthy and falsy values are one of Python's most useful language features.

Rather than writing verbose conditional expressions, Python allows objects to naturally express whether they should be treated as `True` or `False`.

Understanding this behavior will help you write cleaner, shorter, and more idiomatic solutions during coding interviews.
