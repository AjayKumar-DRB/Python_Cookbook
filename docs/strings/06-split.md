# `split()`

## Introduction

The `split()` method divides a string into a list of substrings based on a specified delimiter. It is the primary tool for parsing text input in coding interviews.

Whether you're processing log files, reading CSV data, or reversing words in a sentence, `split()` is often your first step.

---

## How `split()` Works

If you call `split()` without any arguments, it splits the string on **any whitespace** (spaces, tabs, newlines) and automatically discards empty strings.

```python
text = "  hello   world  \n"
words = text.split()
print(words) # ['hello', 'world']
```

### Splitting by a Specific Delimiter

If you provide a string argument, `split()` uses that exact string as the delimiter.

```python
csv = "apple,banana,orange"
fruits = csv.split(",")
print(fruits) # ['apple', 'banana', 'orange']
```

### The `maxsplit` Parameter

You can limit the number of splits by passing a second argument, `maxsplit`.

```python
text = "key:value1:value2"

# Split only on the first colon
parts = text.split(":", 1)
print(parts) # ['key', 'value1:value2']
```

---

## Interview Pattern: Reverse Words in a String

A classic interview question asks you to reverse the order of words in a string, ensuring there's only a single space between words and no leading/trailing spaces.

`split()` and `join()` make this trivial.

```python
def reverse_words(s):
    # split() with no args automatically handles multiple spaces
    words = s.split()
    
    # Reverse the list of words
    words.reverse()
    
    # Join them back together
    return " ".join(words)

print(reverse_words("  the sky   is blue  ")) 
# "blue is sky the"
```

---

## Common Interview Mistakes

### Mistake: Splitting by `" "` instead of `()` 
When a string contains multiple consecutive spaces, `split(" ")` will yield empty strings in the result, which is rarely what you want.

**Incorrect:**
```python
text = "a  b"
print(text.split(" ")) 
# ['a', '', 'b']
```

**Correct:**
```python
text = "a  b"
print(text.split()) 
# ['a', 'b']
```
Always use `split()` without arguments if you simply want to separate words by whitespace.

---

## Time and Space Complexity

- **Time Complexity**: $O(N)$ where $N$ is the length of the string.
- **Space Complexity**: $O(N)$ to store the resulting list of strings.

---

## Summary
- `split()` divides a string by whitespace and drops empty strings.
- `split("delimiter")` divides exactly by the delimiter, keeping empty strings if consecutive delimiters exist.
- Use `split()` in combination with `join()` to easily parse and reformat text.
