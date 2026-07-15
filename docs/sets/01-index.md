# Sets in Python

## Introduction

Sets in Python are collections of unique, hashable objects. They are implemented using the same underlying hash table structure as dictionaries, but they only store the keys, not the values.

In coding interviews, sets are your primary tool for removing duplicates and achieving $O(1)$ membership testing (checking if an item exists).

---

## What You Need to Know

In coding interviews, you will frequently use sets to:
- Remove duplicates from a list.
- Keep track of visited nodes in Graph traversals (DFS/BFS) to prevent infinite loops.
- Find the intersection or difference between two collections.
- Optimize $O(N)$ list lookups into $O(1)$ set lookups.

In this section, we will cover:
- **Hashing**: Why sets provide $O(1)$ lookups and what constraints this places on set elements.
- **Python Sets**: Creating, modifying, and iterating over sets.
- **Set Operations**: Intersections, unions, and differences.
- **Frozenset**: Immutable sets that can be used as dictionary keys.
- **Interview Recipes**: Standard templates for common set problems.

---

## Key Concept: Optimization through $O(1)$ Lookups

The most common mistake candidates make is writing `if item in my_list:`. This requires an $O(N)$ linear scan of the list.

If you need to perform this check inside a loop, your algorithm becomes $O(N^2)$. By converting the list to a set first, `if item in my_set:` becomes an $O(1)$ operation, reducing the total time complexity to $O(N)$.
