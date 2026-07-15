# Performance Optimizations

## Introduction

In an interview, achieving the correct Big-O time complexity is your primary goal. However, understanding constant-factor optimizations and hidden $O(N)$ traps can be the difference between a "Hire" and a "Strong Hire."

---

## 1. The `list.pop(0)` Trap

This is the most common reason candidates fail BFS questions.

```python
queue = [1, 2, 3]

# This is an O(N) operation!
queue.pop(0) 
```
When you pop from the front of a list, Python has to physically shift every remaining element one index to the left in memory. In a loop, this turns an $O(N)$ algorithm into an $O(N^2)$ algorithm.

**The Fix:** Always `import collections.deque` and use `queue.popleft()`, which is $O(1)$.

---

## 2. String Concatenation Trap

Strings in Python are immutable. Every time you use `+` or `+=` to concatenate a string, Python must allocate new memory and copy the entire contents of both strings.

```python
# This is O(N^2) time!
result = ""
for char in "hello":
    result += char 
```

**The Fix:** Append characters to a list, and use `"".join()` at the very end. This is $O(N)$ time.

```python
chars = []
for char in "hello":
    chars.append(char)
    
result = "".join(chars) # O(N)
```

---

## 3. Hash Set vs List Lookups

If you need to repeatedly check if an element exists in a collection, **never use a list**.

```python
banned_words = ["apple", "banana", "cherry"] # Imagine this has 10,000 words

# O(N) operation!
if "apple" in banned_words:
    pass
```

**The Fix:** Convert the list to a `set` first. Set lookups are $O(1)$.

```python
banned_set = set(banned_words)

# O(1) operation!
if "apple" in banned_set:
    pass
```

---

## 4. Local vs Global Variables

In Python, accessing local variables is significantly faster than accessing global variables. This is because local variables are stored in a fixed-size array accessed by index (in C), whereas globals require a dictionary lookup.

If you have a highly performance-sensitive inner loop, assigning a global or class variable to a local variable before the loop can yield a noticeable speedup.

```python
class Solution:
    def process(self):
        # Accessing self.data inside a massive loop is slower
        
        # Optimization: bind to local variable
        local_data = self.data
        for item in local_data:
            pass
```

---

## 5. Use Built-ins (They are written in C)

Whenever possible, use Python's built-in functions (`sum()`, `max()`, `min()`, `map()`) instead of writing a manual `for` loop.

The built-in functions are implemented in heavily optimized C code. A manual Python `for` loop has to go through the Python interpreter on every iteration, which is vastly slower.

```python
nums = [1, 2, 3, 4]

# Slower (Interpreted)
total = 0
for n in nums:
    total += n

# Faster (Executed in C)
total = sum(nums)
```

---

## Summary
- Never `pop(0)` from a list. Use `collections.deque`.
- Never `+=` strings in a loop. Append to a list and `"".join()`.
- Use `set` for all membership `in` lookups.
- Favor built-in functions (`max`, `sum`) over manual loops.
