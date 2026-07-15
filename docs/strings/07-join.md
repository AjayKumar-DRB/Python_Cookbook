# `join()`

## Introduction

The `join()` method is the most efficient and Pythonic way to combine a list of strings into a single string. 

Because strings are immutable in Python, repeatedly using the `+` operator to concatenate strings inside a loop leads to poor performance. `join()` solves this by computing the total memory needed and allocating it all at once.

---

## How `join()` Works

Unlike many other programming languages where `join` is called on the list itself, in Python, `join` is a string method called on the **delimiter**.

```python
words = ["coding", "interviews", "are", "fun"]

# Join with a space
sentence = " ".join(words)
print(sentence) # "coding interviews are fun"

# Join with a comma
csv = ",".join(words)
print(csv) # "coding,interviews,are,fun"
```

### Joining Characters

If you have a list of characters, use an empty string `""` as the delimiter.

```python
chars = ['a', 'b', 'c']
result = "".join(chars)
print(result) # "abc"
```

---

## When to use `join()`

You should use `join()` whenever you need to build a string from multiple pieces in a loop.

**Example: Removing Vowels**
```python
def remove_vowels(s):
    vowels = set("aeiouAEIOU")
    result = []
    
    for char in s:
        if char not in vowels:
            result.append(char)
            
    # Much faster than result_string += char
    return "".join(result) 
```

---

## Common Interview Mistakes

### Mistake: `TypeError` with Non-Strings
The `join()` method only works on iterables containing **strings**. If the list contains integers or other data types, it will raise a `TypeError`.

**Incorrect:**
```python
nums = [1, 2, 3]
print("-".join(nums)) # TypeError
```

**Correct:**
You must convert the elements to strings first, usually with a generator expression or list comprehension.
```python
nums = [1, 2, 3]
print("-".join(str(n) for n in nums)) # "1-2-3"
```

### Mistake: Repeated String Concatenation (`+`)
Never do this in an interview:

```python
result = ""
for word in words:
    result += word + " "
```

This takes $O(N^2)$ time because a new string is created and copied during every iteration. Using `" ".join(words)` takes $O(N)$ time.

---

## Time and Space Complexity

- **Time Complexity**: $O(N)$ where $N$ is the total length of all strings combined.
- **Space Complexity**: $O(N)$ to store the newly created string.

---

## Summary
- Use `"delimiter".join(iterable)`.
- Use `"".join()` to convert a list of characters back into a string.
- Never use `+` to build a string iteratively in a loop. Use `join()` instead to guarantee $O(N)$ time complexity.
- Remember to convert numbers to strings before calling `join()`.
