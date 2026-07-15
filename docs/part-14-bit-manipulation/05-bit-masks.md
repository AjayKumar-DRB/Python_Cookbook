# Bit Masks

> Using an integer as a lightweight, lightning-fast boolean array.

---

## Introduction

A **Bit Mask** is a sequence of bits used to isolate, modify, or query specific bits within another integer. 

In technical interviews, bit masking is heavily used in Dynamic Programming (Bitmask DP) or when generating combinations to represent which elements have been "selected" in $O(1)$ space.

---

## What is it?

Instead of using a `list[bool]` to track if items are `True` or `False`, we can use a single integer. 

For example, an integer `5` (binary `101`) can represent a state where the 0th and 2nd items are selected, and the 1st item is not.

| Data Structure | Space | Time to copy state |
|----------------|-------|--------------------|
| `list[bool]` | $O(N)$ | $O(N)$ |
| `int` (Bit Mask) | $O(1)$ | $O(1)$ |

---

## Common Bit Mask Operations

You must know how to perform these four basic operations on a bit mask. Let `mask` be our state integer, and `i` be the index (0-based) of the bit we want to interact with.

### 1. Check if the $i$-th bit is SET (is `True`)
Use the AND (`&`) operator. If the result is not `0`, the bit is set.

```python
# To check if the 2nd bit is set:
# We shift 1 to the left by 2 spaces (creating 000...100)
# Then we AND it with the mask
if mask & (1 << i):
    print(f"Bit {i} is True!")
```

### 2. SET the $i$-th bit to 1 (`True`)
Use the OR (`|`) operator.

```python
# Sets the 2nd bit to 1, leaving all other bits unchanged.
mask = mask | (1 << i)
```

### 3. CLEAR the $i$-th bit to 0 (`False`)
Use the AND (`&`) operator combined with NOT (`~`).

```python
# ~ (1 << i) creates a mask of all 1s, except a 0 at index i.
# ANDing this with our mask forces the i-th bit to 0.
mask = mask & ~(1 << i)
```

### 4. TOGGLE the $i$-th bit (Flip it)
Use the XOR (`^`) operator.

```python
# Flips 0 to 1, or 1 to 0 at the i-th position.
mask = mask ^ (1 << i)
```

---

## DSA Example: Bitmask DP State

Imagine you are solving the Traveling Salesperson Problem (TSP) using Dynamic Programming. You have 10 cities to visit, and you need to track which cities you have already visited.

Using a tuple or list as the DP state key is slow. Instead, use a bitmask!

```python
def tsp(current_city, visited_mask):
    # Base case: if all 10 cities are visited (bits 0-9 are all 1s)
    # The number where the first 10 bits are 1 is (1 << 10) - 1
    if visited_mask == (1 << 10) - 1:
        return 0
        
    # Check neighbors...
    for next_city in range(10):
        # Check if the next_city has already been visited
        if not (visited_mask & (1 << next_city)):
            # It hasn't! Set the bit to 1 and recurse
            new_mask = visited_mask | (1 << next_city)
            tsp(next_city, new_mask)
```

---

## Key Takeaways

- Bit masks replace boolean arrays for states with less than 64 items.
- `mask | (1 << i)` sets a bit.
- `mask & ~(1 << i)` clears a bit.
- `mask & (1 << i)` checks a bit.
- `(1 << N) - 1` creates a mask where the first $N$ bits are all `1`.

---

## Related Topics

- [Bitwise Operators](03-bitwise-operators.md)
- [Subsets Using Bits](08-subsets-using-bits.md)
