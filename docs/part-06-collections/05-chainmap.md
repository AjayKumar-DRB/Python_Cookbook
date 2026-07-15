# `collections.ChainMap`

## Introduction

A `ChainMap` groups multiple dictionaries or mappings together to create a single, updatable view. 

While it is one of the more obscure tools in the `collections` module, it is the perfect solution for questions involving variable scoping, configuration fallback, or nested environments.

---

## How `ChainMap` Works

When you create a `ChainMap`, it takes a list of dictionaries. When you look up a key, it searches the dictionaries in the order they were provided, returning the value from the **first dictionary that has the key**.

```python
from collections import ChainMap

defaults = {'theme': 'light', 'language': 'en'}
user_prefs = {'language': 'fr'}

# Search user_prefs first, then fallback to defaults
config = ChainMap(user_prefs, defaults)

print(config['language']) # 'fr' (from user_prefs)
print(config['theme'])    # 'light' (fallback to defaults)
```

---

## Mutations Only Affect the First Mapping

A key property of `ChainMap` is how it handles updates. If you add, update, or delete a key in a `ChainMap`, it **only affects the very first dictionary** in the chain.

```python
config['theme'] = 'dark'

print(user_prefs) # {'language': 'fr', 'theme': 'dark'}
print(defaults)   # {'theme': 'light', 'language': 'en'}
```

---

## Interview Application: Scope Resolution

If an interviewer asks you to build a simple interpreter or a system with variable scoping (e.g., local variables shadowing global variables), `ChainMap` is the ideal data structure.

You can use the `.new_child()` method to push a new scope (a new empty dictionary at the front of the chain), and `.parents` to pop the current scope.

```python
# Start with global scope
globals_env = {'x': 10}
env = ChainMap(globals_env)

# Enter a local function scope
local_env = env.new_child()
local_env['x'] = 20 # Shadows the global 'x'
local_env['y'] = 5

print(local_env['x']) # 20 (local)
print(local_env['y']) # 5 (local)

# Exit the local scope
env = local_env.parents

print(env['x']) # 10 (global)
# print(env['y']) # KeyError (out of scope)
```

---

## Time and Space Complexity

- **Time Complexity**: 
  - Lookup: $O(K)$ where $K$ is the number of dictionaries in the chain (it must check them sequentially).
  - Update: $O(1)$ (always modifies the first dictionary).
- **Space Complexity**: $O(1)$ overhead. It does not copy the dictionaries; it simply holds references to them.

---

## Summary
- A `ChainMap` groups multiple dictionaries into a single view.
- Lookups search dictionaries sequentially from left to right.
- Updates and deletions only affect the first dictionary.
- Use it for scoping (local/global variables) or configuration fallbacks.
