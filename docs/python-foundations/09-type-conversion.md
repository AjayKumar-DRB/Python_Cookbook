# Type Conversion

> *"Practicality beats purity."*  
> — **The Zen of Python**

### Introduction

Type conversion is the process of converting one data type into another.

Python provides several built-in functions for converting between common data types.

Type conversion appears frequently in coding interviews, especially when working with user input, strings, numbers, lists, sets, and dictionaries.

---

## Implicit Type Conversion

Python automatically converts compatible types when it is safe to do so.

```python
result = 10 + 2.5

print(result)
```

Output

```python
12.5
```

Python automatically converts the integer into a float.

---

## Explicit Type Conversion

Explicit conversion is performed using built-in functions.

Example

```python
age = "25"

age = int(age)
```

---

## `int()`

Converts a compatible value into an integer.

```python
int("42")
```

Output

```python
42
```

---

```python
int(3.9)
```

Output

```python
3
```

Notice that it **truncates** the decimal part instead of rounding.

---

Invalid conversion

```python
int("abc")
```

Raises

```python
ValueError
```

---

### Common Interview Use Cases

Convert user input

```python
n = int(input())
```

Convert digits while iterating over a string

```python
digit = int(ch)
```

---

## `float()`

Converts a value into a floating-point number.

```python
float("3.14")
```

Output

```python
3.14
```

---

## `str()`

Converts any object into its string representation.

```python
str(123)
```

Output

```python
"123"
```

Useful when building output strings.

---

## `list()`

Creates a list from an iterable.

```python
list("hello")
```

Output

```python
['h', 'e', 'l', 'l', 'o']
```

---

Common interview trick

```python
chars = list(s)

chars.reverse()

result = "".join(chars)
```

---

## `tuple()`

Creates a tuple.

```python
tuple([1, 2, 3])
```

Output

```python
(1, 2, 3)
```

---

## `set()`

Creates a set.

```python
set([1, 2, 2, 3])
```

Output

```python
{1, 2, 3}
```

Very common for removing duplicates.

---

Interview example

```python
if len(nums) != len(set(nums)):
    print("Duplicates Found")
```

---

## `dict()`

Creates a dictionary.

```python
pairs = [
    ("a", 1),
    ("b", 2)
]

dictionary = dict(pairs)
```

Output

```python
{
    "a": 1,
    "b": 2
}
```

---

## `bool()`

Converts values into boolean form.

```python
bool(1)
```

Output

```python
True
```

---

```python
bool(0)
```

Output

```python
False
```

---

```python
bool("")
```

Output

```python
False
```

---

```python
bool("Python")
```

Output

```python
True
```

---

## `ord()`

Returns the Unicode code point of a character.

```python
ord("a")
```

Output

```python
97
```

Very useful in string problems.

Example

```python
index = ord(ch) - ord("a")
```

We'll cover this in detail in the Strings section.

---

## `chr()`

Converts a Unicode value back into a character.

```python
chr(97)
```

Output

```python
'a'
```

---

## Binary, Octal and Hexadecimal

Convert to binary

```python
bin(10)
```

Output

```python
'0b1010'
```

---

Convert to hexadecimal

```python
hex(255)
```

Output

```python
'0xff'
```

---

Convert to octal

```python
oct(10)
```

Output

```python
'0o12'
```

---

## Parsing Different Bases

Binary

```python
int("1010", 2)
```

Output

```python
10
```

---

Hexadecimal

```python
int("FF", 16)
```

Output

```python
255
```

---

## Common Interview Examples

### Reverse Integer

```python
num = int(str(num)[::-1])
```

---

### Remove Duplicate Characters

```python
unique = set(s)
```

---

### Convert String to Character List

```python
chars = list(word)
```

---

### Frequency Array

```python
index = ord(ch) - ord("a")
```

---

## Time Complexity

| Operation | Complexity |
|-----------|------------|
| `int()` | O(n) (for strings) |
| `float()` | O(n) |
| `str()` | O(n) |
| `list()` | O(n) |
| `tuple()` | O(n) |
| `set()` | O(n) |
| `dict()` | O(n) |
| `bool()` | O(1) |
| `ord()` | O(1) |
| `chr()` | O(1) |

---

## Common Mistakes

### Mistake 1

Using

```python
int("3.14")
```

Raises

```python
ValueError
```

Instead

```python
int(float("3.14"))
```

---

### Mistake 2

Expecting

```python
list(123)
```

to work.

It raises

```python
TypeError
```

Only iterables can be converted using `list()`.

---

### Mistake 3

Assuming

```python
bool("False")
```

returns `False`.

It returns

```python
True
```

Any non-empty string is truthy.

---

## Best Practices

- Use `set()` to remove duplicates.
- Use `list()` when string mutation is required.
- Use `ord()` and `chr()` for character arithmetic.
- Avoid unnecessary conversions inside loops.
- Validate user input before conversion.

---

## Key Takeaways

- Python provides built-in functions for converting between common data types.
- `ord()` and `chr()` are extremely useful for string algorithms.
- `set()` is one of the easiest ways to remove duplicates.
- Be aware that some conversions may raise exceptions.
- Avoid repeated conversions inside performance-critical loops.

---

## Related Topics

- Truthy and Falsy Values
- Strings
- Sets
- Dictionaries
- ASCII and Unicode

---

## Practice Questions

1. What is the difference between implicit and explicit conversion?
2. Why does `int(3.9)` return `3`?
3. What does `list("hello")` produce?
4. How do you remove duplicates using `set()`?
5. Why is `ord()` useful in interview questions?

---

## Summary

Type conversion is a fundamental skill for Python programmers.

Understanding when and how to convert between data types allows you to write cleaner, more efficient solutions and makes many interview problems significantly easier to solve.

The next chapter introduces the operators that appear most frequently in coding interviews, including arithmetic, comparison, logical, membership, identity, and bitwise operators.
