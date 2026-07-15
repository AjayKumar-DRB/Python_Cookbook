# Mutable Default Arguments

## The Pitfall

This is perhaps the most famous "gotcha" in Python.

If you use a mutable object (like a `list`, `dict`, or `set`) as a default argument in a function signature, **that object is created exactly once when the function is defined, NOT every time the function is called.**

### The Broken Code
```python
def append_to_list(val, my_list=[]):
    my_list.append(val)
    return my_list

# Interviewer: "What does this print?"
print(append_to_list(1))
print(append_to_list(2))
```

### What You Think Happens:
```python
[1]
[2]
```

### What Actually Happens:
```python
[1]
[1, 2]
```

Because `my_list` is created once during function definition, the second call to `append_to_list(2)` appends to the *exact same list* that was used in the first call.

---

## When Does This Happen in Interviews?

This bug frequently occurs when candidates write helper functions for Trees or Graphs, and they try to initialize a `visited` set or a `path` list in the signature.

```python
# DANGEROUS
def dfs(node, visited=set()):
    if node in visited: return
    visited.add(node)
    # ...
```
If the interviewer runs your `dfs()` function twice on two different test cases, the second test case will fail immediately because `visited` still contains all the nodes from the first test case!

---

## The Fix

Always use `None` as the default value, and initialize the mutable object inside the function body.

```python
# CORRECT
def dfs(node, visited=None):
    if visited is None:
        visited = set()
        
    if node in visited: return
    visited.add(node)
    # ...
```
This guarantees that a fresh, empty set is created every single time the function is called without a `visited` argument.
