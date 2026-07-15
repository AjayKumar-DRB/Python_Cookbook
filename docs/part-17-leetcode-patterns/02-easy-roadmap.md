# Easy Roadmap

> Building your fundamental muscle memory.

---

## Introduction

"Easy" LeetCode questions are rarely asked in FAANG onsite loops (they might appear as a warm-up in a phone screen). However, you must master them because they form the atomic building blocks of Medium and Hard questions.

If you struggle with an Easy question, it means you have a gap in your knowledge of a core Data Structure.

---

## The Goals of Easy Questions

1. **Language Fluency:** You should be able to write `for` loops, initialize dictionaries, and slice arrays in Python without thinking about the syntax.
2. **Edge Case Awareness:** Learning to handle empty arrays, single-element arrays, and negative numbers.
3. **Complexity Intuition:** Realizing why your nested `for` loop (Brute Force) is too slow, and learning how a Hash Map fixes it.

---

## The Easy Patterns to Master

Do not move on to Medium questions until you can comfortably solve these Easy patterns in under 15 minutes:

### 1. Hash Maps (Counting & Lookups)
The ability to map a key to a value in $O(1)$ time is the most important skill in interviewing.
- **Classic Problem:** Two Sum (LeetCode 1)
- **Classic Problem:** Valid Anagram (LeetCode 242)

### 2. Two Pointers (Opposite Ends)
Moving a `left` and `right` pointer towards the center of an array or string.
- **Classic Problem:** Valid Palindrome (LeetCode 125)

### 3. Linked List Traversal
Understanding how to move a pointer `curr = curr.next` without losing the `head`.
- **Classic Problem:** Reverse Linked List (LeetCode 206)
- **Classic Problem:** Merge Two Sorted Lists (LeetCode 21)

### 4. Binary Search (Basic)
Finding a target in a sorted array in $O(\log N)$ time.
- **Classic Problem:** Binary Search (LeetCode 704)

### 5. Depth-First Search (Tree Traversal)
Understanding basic recursive calls on `root.left` and `root.right`.
- **Classic Problem:** Maximum Depth of Binary Tree (LeetCode 104)
- **Classic Problem:** Invert Binary Tree (LeetCode 226)

---

## When are you ready for Mediums?

You are ready for Mediums when:
- You know exactly when to use a Dictionary vs a Set.
- You can reverse a Linked List perfectly on the first try without a `NoneType` error.
- You can write a basic Binary Search `while left <= right` loop from memory.
- You can explain the difference between $O(N)$ and $O(N^2)$ confidently.

---

## Related Topics

- [Medium Roadmap](03-medium-roadmap.md)
- [Blind 75](05-blind-75.md)
