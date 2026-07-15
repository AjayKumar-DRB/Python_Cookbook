# Operators Used in DSA

> *"Simple code is easier to reason about."*

### Introduction

Python provides a rich set of operators that make coding interview solutions concise and expressive.

While Python supports many operators, only a subset appears regularly in Data Structures and Algorithms (DSA) problems.

This chapter focuses on the operators you will actually use in coding interviews.

---

## Arithmetic Operators

| Operator | Description | Example |
|----------|-------------|---------|
| `+` | Addition | `a + b` |
| `-` | Subtraction | `a - b` |
| `*` | Multiplication | `a * b` |
| `/` | Floating-point Division | `a / b` |
| `//` | Floor Division | `a // b` |
| `%` | Modulus | `a % b` |
| `**` | Exponentiation | `a ** b` |

Example

```python
a = 17
b = 5

print(a + b)
print(a // b)
print(a % b)
```

Output

```python
22
3
2
```

---

### Floor Division (`//`)

Floor division returns the quotient without the fractional part.

```python
17 // 5
```

Output

```python
3
```

Very common in Binary Search.

```python
mid = (left + right) // 2
```

---

### Modulus (`%`)

Returns the remainder.

```python
17 % 5
```

Output

```python
2
```

Common interview uses:

- Even/Odd checking
- Circular arrays
- Hashing
- Bucketing

Example

```python
if num % 2 == 0:
    print("Even")
```

---

## Comparison Operators

| Operator | Meaning |
|----------|---------|
| `==` | Equal |
| `!=` | Not Equal |
| `<` | Less Than |
| `<=` | Less Than or Equal |
| `>` | Greater Than |
| `>=` | Greater Than or Equal |

Example

```python
if score >= 90:
    print("Excellent")
```

---

## Logical Operators

| Operator | Description |
|----------|-------------|
| `and` | Logical AND |
| `or` | Logical OR |
| `not` | Logical NOT |

Example

```python
if left <= right and nums[mid] == target:
    print("Found")
```

---

## Assignment Operators

| Operator | Example |
|----------|---------|
| `=` | `x = 5` |
| `+=` | `x += 1` |
| `-=` | `x -= 1` |
| `*=` | `x *= 2` |
| `/=` | `x /= 2` |
| `//=` | `x //= 2` |
| `%=` | `x %= 2` |

Example

```python
count = 0

count += 1
```

Preferred over

```python
count = count + 1
```

---

## Membership Operators

| Operator | Meaning |
|----------|---------|
| `in` | Exists |
| `not in` | Does Not Exist |

Example

```python
if target in nums:
    print("Found")
```

---

Dictionary example

```python
if word in frequency:
    frequency[word] += 1
```

---

Set example

```python
if value in visited:
    return
```

Membership testing is heavily used in BFS and DFS.

---

## Identity Operators

| Operator | Meaning |
|----------|---------|
| `is` | Same object |
| `is not` | Different object |

Example

```python
if node is None:
    return
```

Avoid

```python
if node == None:
```

---

## Bitwise Operators

| Operator | Description |
|----------|-------------|
| `&` | AND |
| `|` | OR |
| `^` | XOR |
| `~` | NOT |
| `<<` | Left Shift |
| `>>` | Right Shift |

Example

```python
5 & 3
```

Output

```python
1
```

---

Bitwise operators appear in:

- Bit Manipulation
- Masks
- Subset Generation
- XOR problems

They will be covered in detail later.

---

## Operator Precedence

Understanding precedence prevents subtle bugs.

Example

```python
2 + 3 * 4
```

Output

```python
14
```

because multiplication happens first.

When in doubt, use parentheses.

```python
(2 + 3) * 4
```

Output

```python
20
```

---

## Common DSA Examples

### Binary Search

```python
mid = (left + right) // 2
```

---

### Even or Odd

```python
if num % 2 == 0:
```

---

### Membership

```python
if node in visited:
```

---

### Counting

```python
count += 1
```

---

### DFS

```python
if node is None:
    return
```

---

## Time Complexity

Most operators execute in **O(1)** time.

Exceptions include:

- Membership checks on lists → **O(n)**
- Membership checks on strings → **O(n)**
- Membership checks on sets and dictionaries → **O(1)** average case

---

## Common Mistakes

### Mistake 1

Using

```python
/
```

instead of

```python
//
```

when computing array indices.

---

### Mistake 2

Using

```python
==
```

instead of

```python
is
```

for `None`.

---

### Mistake 3

Forgetting operator precedence.

Always use parentheses when expressions become complex.

---

### Mistake 4

Assuming

```python
target in list
```

is O(1).

It is **O(n)**.

---

## Best Practices

- Use `//` for integer division.
- Use `%` for parity and cyclic indexing.
- Use `+=` for counters.
- Use `is None` for null checks.
- Prefer set or dictionary membership over list membership when performance matters.

---

## Key Takeaways

- Arithmetic, comparison, logical, and membership operators appear in almost every coding interview.
- Use `//` when calculating indices.
- Understand the complexity of membership operations.
- Bitwise operators become important for advanced problems.
- Parentheses improve readability and prevent precedence mistakes.

---

## Related Topics

- Membership Operators
- Bit Manipulation
- Binary Search
- Sets
- Dictionaries

---

## Practice Questions

1. Why is `//` preferred over `/` in Binary Search?
2. What is the difference between `%` and `//`?
3. Why is `target in nums` slower for a list than for a set?
4. When should you use `is` instead of `==`?
5. What does the XOR (`^`) operator do?

---

## Summary

Operators are the building blocks of every algorithm.

A strong understanding of Python's operators helps you write cleaner, more efficient solutions and avoid common interview mistakes.

In the next chapter, we'll focus specifically on **membership operators**, exploring how `in` and `not in` behave across different Python data structures and why their performance characteristics matter in interview problems.
