# Interview Pitfalls

## Introduction

Nothing is more frustrating than having the perfect algorithm in mind, writing it out on the whiteboard, and failing the interview because of a subtle language-specific bug.

Python is designed to be user-friendly, but that friendliness hides a few sharp edges. If you don't know exactly how Python handles memory, references, and defaults, you can easily introduce bugs that are incredibly difficult to spot during a stressful interview.

---

## The Danger Zones

In this section, we cover the classic "gotchas" that sink Python interviews:
- **Mutable Default Arguments**: Why `def func(lst=[])` is a disaster.
- **Shallow vs Deep Copy**: Why `matrix = [[0] * N] * M` ruins DP algorithms.
- **Time Complexity Traps**: Operations that look like $O(1)$ but are actually $O(N)$ (like `list.insert()` and `list.index()`).
- **Memory Pitfalls**: How to avoid exceeding memory limits.
- **Recursion Limits**: Dealing with Python's relatively small default recursion depth.
- **Off-By-One Errors**: Mastering array boundaries and loop ranges.

---

## How to Use This Section

Read through these pitfalls carefully. If you make any of these mistakes during a mock interview, make a flashcard. Preventing these bugs proactively is much faster than trying to debug them retroactively while an interviewer watches you.
