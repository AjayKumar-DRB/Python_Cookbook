# Hash Tables (Under the Hood)

## Introduction

In an interview, you may be asked *why* a Python dictionary has $O(1)$ lookups, or what happens when a "collision" occurs.

Understanding the theory behind hash tables is critical for these system design and core CS questions.

---

## How a Hash Table Works

A hash table is built on top of an array.

When you insert a key-value pair into a dictionary, Python does not just append it to the end of the array. Instead, it uses a **hash function** to determine exactly where in the array the value should be stored.

### 1. The Hash Function
Python runs the key through a built-in mathematical function called `hash()`. This function converts the key (like a string or a tuple) into a large integer.

```python
print(hash("apple")) # e.g., 872938472934
```

### 2. Modulo Arithmetic
Python takes that large hash value and uses the modulo operator `%` with the current size of the underlying array to find a valid index.

`index = hash(key) % array_size`

### 3. Storage and Lookup
The value is stored at that calculated index. 
When you look up `my_dict["apple"]`, Python hashes `"apple"`, computes the index, and jumps directly to that spot in memory. This is why lookups are $O(1)$.

---

## What Can Be a Key?

Because the dictionary relies on the `hash()` function, **keys must be immutable** (hashable).

- **Valid Keys**: Integers, Strings, Tuples, Booleans.
- **Invalid Keys**: Lists, Sets, other Dictionaries.

```python
valid_dict = {(1, 2): "coordinate"} # Tuple is immutable

# TypeError: unhashable type: 'list'
# invalid_dict = {[1, 2]: "coordinate"} 
```

---

## Collisions

What happens if two different keys result in the exact same array index? This is called a **collision**.

`hash("apple") % 8 == 3`
`hash("banana") % 8 == 3`

Python resolves collisions using a technique called **Open Addressing** (specifically, random probing).

If index 3 is already taken by `"apple"`, Python uses a mathematical formula to jump to another index (e.g., index 5). It keeps jumping until it finds an empty slot to store `"banana"`.

When looking up `"banana"`, Python checks index 3, sees `"apple"`, realizes there was a collision, and follows the same jumping sequence until it finds `"banana"`.

*(Note: Other languages like Java use "Separate Chaining", where each array index holds a linked list of collided items. Python specifically uses Open Addressing).*

---

## Worst-Case Time Complexity

Because of collisions, if a hash table gets too full, or if a malicious user provides keys that all hash to the same index, lookups can degrade to $O(N)$ as Python has to jump through every element.

However, Python automatically resizes (doubles) the underlying array when it is 2/3 full to minimize collisions.

Therefore, for interview purposes:
- **Average Time Complexity**: $O(1)$
- **Worst-Case Time Complexity**: $O(N)$ (but you rarely need to worry about this unless asked).

---

## Summary
- Dictionaries are Hash Tables.
- They use a `hash()` function to turn immutable keys into array indices.
- **Collisions** happen when two keys map to the same index.
- Python handles collisions via **Open Addressing** (probing for an empty slot).
- Lookups are average $O(1)$, worst-case $O(N)$.
