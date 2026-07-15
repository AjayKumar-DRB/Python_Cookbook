# Dictionary Methods

## Introduction

Python dictionaries come with several built-in methods that make iterating and safely accessing data much cleaner. Mastering these methods will make your interview code faster to write and less prone to bugs.

---

## Safely Accessing Values: `get()`

Instead of checking if a key exists before accessing it, you can use the `get()` method. 

If the key exists, `get()` returns the value. If it doesn't, it returns `None` (or a default value you specify), avoiding a `KeyError`.

```python
counts = {"a": 1, "b": 2}

# Avoids KeyError, returns None
print(counts.get("c")) 

# Returns a default value of 0 if "c" is missing
print(counts.get("c", 0)) # 0
```

### When to use `get()`
Use `get(key, default)` when incrementing counters or building frequency maps manually.

```python
# Increment count of char, defaulting to 0 if not seen yet
counts[char] = counts.get(char, 0) + 1
```

---

## Iterating Over Dictionaries

By default, iterating over a dictionary yields its **keys**.

```python
person = {"name": "Alice", "age": 25}

for key in person:
    print(key) 
# "name"
# "age"
```

### 1. `keys()`
Returns a view object of the dictionary's keys. Rarely needed in loops since iterating the dictionary directly does the same thing, but useful for set operations.

```python
print(person.keys()) # dict_keys(['name', 'age'])
```

### 2. `values()`
Returns a view object of the dictionary's values.

```python
for val in person.values():
    print(val)
# "Alice"
# 25
```

### 3. `items()` (Most Important)
Returns a view object yielding `(key, value)` tuples. **Always use this when you need both the key and the value in a loop.**

```python
for key, value in person.items():
    print(f"{key}: {value}")
```

### Common Interview Mistake: Manual Value Lookup
Many candidates iterate over the keys and manually look up the value. This is un-Pythonic and technically requires an extra hash table lookup per iteration.

**Avoid:**
```python
for key in person:
    value = person[key] # Extra O(1) lookup
    print(key, value)
```

**Prefer:**
```python
for key, value in person.items():
    print(key, value)
```

---

## Safely Updating Values: `setdefault()`

If you are building a dictionary where values are lists (like an adjacency list for a graph), you often need to initialize the list before appending to it.

```python
graph = {}

# The verbose way
if "A" not in graph:
    graph["A"] = []
graph["A"].append("B")
```

You can do this in one line using `setdefault()`. It checks if the key exists; if not, it sets it to the default value, and then returns the value.

```python
graph = {}

# The concise way
graph.setdefault("A", []).append("B")
```
*(Note: While `setdefault()` is useful, `collections.defaultdict` is usually preferred in interviews. We will cover `defaultdict` in the Collections section).*

---

## Summary
- Use `get(key, default)` to safely retrieve values without `KeyError`s.
- Use `items()` to iterate over both keys and values simultaneously.
- Use `setdefault(key, default)` to initialize complex values like lists or sets before modifying them.
