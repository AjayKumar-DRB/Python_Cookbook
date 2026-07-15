# Complexity Analysis

> Big O Notation in the real world.

---

## Introduction

"What is the time and space complexity of your solution?"

You will be asked this question at the end of exactly 100% of your technical interviews. If you hesitate, guess, or get it wrong, it is a massive red flag. 

You must be able to confidently analyze your own code.

---

## Time Complexity (Big O)

Time complexity measures how the runtime scales as the input size ($N$) grows towards infinity. We drop all constants and lower-order terms.

- $O(2N)$ becomes $O(N)$
- $O(N^2 + N)$ becomes $O(N^2)$

### How to analyze your code

Look at your loops:

1. **No loops:** $O(1)$
2. **One loop:** $O(N)$
3. **Two nested loops:** $O(N^2)$
4. **Halving the search space every step:** $O(\log N)$ (e.g., Binary Search)
5. **Looping while halving:** $O(N \log N)$ (e.g., Merge Sort, Python's `list.sort()`)
6. **Branching recursion:** $O(\text{branches}^{\text{depth}})$ (e.g., $O(2^N)$ for basic Fibonacci)
7. **Permutations:** $O(N!)$

### Hidden Complexities

In Python, built-in functions have hidden time complexities that you MUST know.

- `val in my_list`: $O(N)$
- `val in my_set`: $O(1)$
- `my_list.pop(0)`: $O(N)$
- `sum(my_list)`: $O(N)$
- `my_string.replace()`: $O(N)$
- `min(my_list)` or `max(my_list)`: $O(N)$

If you put an $O(N)$ built-in method inside a `for` loop, your algorithm is $O(N^2)$, even if it looks like one loop!

---

## Space Complexity

Space complexity measures how much *extra* memory your algorithm allocates as the input size grows. 

**Do not count the memory required to hold the input itself, or the memory required to hold the final output array.** We only care about the *auxiliary* (extra) space.

### How to analyze your space

1. **Variables only:** $O(1)$
2. **Storing elements in a Set/Dict:** $O(N)$ (Worst case, every element is unique).
3. **Recursion:** $O(H)$ where $H$ is the maximum depth of the recursive call stack.

### Python-Specific Space Complexities

- **Slicing strings or lists:** `arr[1:5]` creates a *brand new copy* in memory. Doing this in a loop creates massive space overhead.
- **String Concatenation:** `string += "a"` creates a *new string* every time because strings are immutable. This takes $O(N^2)$ time and $O(N)$ space. Use `''.join(list)` instead.

---

## The "Amortized" Keyword

Sometimes an operation takes $O(N)$ in the worst case, but $O(1)$ on average. This is called **Amortized** $O(1)$.

For example, appending to a Python list is Amortized $O(1)$. When the list runs out of allocated memory, Python must allocate a new, larger block and copy all elements over ($O(N)$). But this happens so rarely that the *average* cost of an append is $O(1)$.

---

## Key Takeaways

- Drop constants and lower-order terms.
- Beware of hidden $O(N)$ complexities in Python built-ins like `in` on lists or `pop(0)`.
- Space complexity only measures *extra* memory allocated, including the recursive Call Stack.

---

## Related Topics

- [Python Complexity Reference](../part-01-python-foundations/13-python-complexity-reference.md)
