# Python Dictionaries

## Introduction

A Python dictionary (`dict`) is a mutable, unordered (historically) collection of key-value pairs. 

*(Note: As of Python 3.7, dictionaries maintain insertion order, but you should rarely rely on this property in algorithm interviews unless specifically using `collections.OrderedDict`).*

---

## Creating Dictionaries

You can create dictionaries using curly braces `{}` or the `dict()` constructor.

```python
# Empty dictionary
empty_dict = {}

# Initialized dictionary
person = {
    "name": "Alice",
    "age": 25,
    "city": "New York"
}
```

---

## Accessing and Updating Values

You access values using square bracket notation.

```python
print(person["name"]) # "Alice"
```

If you access a key that does not exist, Python raises a `KeyError`.
```python
# KeyError: 'job'
# print(person["job"]) 
```

To update a value or add a new key-value pair, assign a value to the key.

```python
# Update existing key
person["age"] = 26

# Add new key
person["job"] = "Engineer"
```

---

## The `in` Operator (Crucial for Interviews)

To check if a **key** exists in a dictionary, use the `in` operator. 
This is an $O(1)$ operation and is the most common way to prevent `KeyError`s.

```python
if "job" in person:
    print(person["job"])
else:
    print("Job not found")
```

### Common Interview Mistake: Checking Values
The `in` operator *only* checks keys, not values.

```python
# This is False, because "Alice" is a value, not a key
print("Alice" in person) 
```
If you need to check if a value exists, you must use `val in person.values()`, which takes $O(N)$ time.

---

## Deleting Elements

You can remove elements using the `del` keyword or the `pop()` method.

```python
# Using del (raises KeyError if key doesn't exist)
del person["city"]

# Using pop (returns the value, allows a default to avoid KeyError)
job = person.pop("job", "Unemployed")
```

---

## Time and Space Complexity

- **Time Complexity**:
  - Insert: $O(1)$ average
  - Lookup: $O(1)$ average
  - Delete: $O(1)$ average
  - `key in dict`: $O(1)$ average
- **Space Complexity**: $O(N)$ to store $N$ key-value pairs.

---

## Summary
- Use `{}` to create a dictionary.
- Keys must be immutable (strings, integers, tuples).
- Use `key in dict` to check for key existence in $O(1)$ time.
- `del dict[key]` or `dict.pop(key)` removes elements.
