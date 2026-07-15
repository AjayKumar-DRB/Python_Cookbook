# Company-Specific Patterns

> Tailoring your prep for the specific FAANG company you are interviewing with.

---

## Introduction

While the NeetCode 150 gives you the general foundation required to pass any interview, different tech giants have distinct interviewing cultures and heavily favor specific patterns.

If you have an onsite loop scheduled for a specific company, you should pivot your final 2 weeks of prep to focus entirely on their preferred patterns.

---

## 1. Meta (Facebook)

Meta is notorious for asking exactly 2 LeetCode questions in a 45-minute technical round. This means you have $\approx 20$ minutes per question, including the explanation.

- **The Meta Pattern:** They heavily reuse questions from their "Top 100 Most Frequent" LeetCode list. The questions are usually Medium difficulty.
- **What to study:** Arrays, Hash Maps, Strings, basic Tree Traversals.
- **What to avoid:** Complex 2D Dynamic Programming or esoteric Hard questions. They want clean, bug-free, perfectly optimal code written *fast*.

## 2. Google

Google is the exact opposite of Meta. They despise asking questions that can be memorized from LeetCode. They will often invent a novel problem, or take a standard problem and add a bizarre twist to it.

- **The Google Pattern:** They heavily test your ability to handle ambiguity and edge cases. They love Graph algorithms, Union Find, and complex Matrix traversals.
- **What to study:** Graphs (BFS/DFS), Dynamic Programming, Binary Search on Answer, Trees.
- **What to avoid:** Blindly memorizing solutions. If you try to paste a memorized solution, they will change the constraints mid-interview to break your code.

## 3. Amazon

Amazon interviews are unique because 50% of the interview is Behavioral (the Leadership Principles). The coding portion is usually standard, but highly focused on real-world applicability.

- **The Amazon Pattern:** They love Object-Oriented Design (OOD) infused into algorithms. For example, "Design an LRU Cache" or "Design a Search Autocomplete System".
- **What to study:** Tries (Prefix Trees), Linked Lists, Hash Maps, Heaps (Top K items).
- **What to avoid:** Highly abstract math or bit manipulation problems.

## 4. Apple

Apple interviews are heavily team-dependent. The iOS team will interview you completely differently than the iCloud backend team.

- **The Apple Pattern:** They focus on deep domain knowledge (concurrency, memory management) alongside standard DSA.
- **What to study:** Strings, Arrays, Linked Lists. Often lean towards Easy/Medium standard questions, followed by deep dives into your language of choice.

## 5. Quantitative Finance (Jane Street, Citadel, Two Sigma)

These are arguably harder than FAANG.

- **The Quant Pattern:** Heavy focus on extreme optimization, Math, and Probability.
- **What to study:** Bit Manipulation, Combinatorics, Dynamic Programming, advanced Tree structures (Segment Trees).
- **What to avoid:** Relying on slow interpreted languages (though Python is okay for some rounds, C++ is often preferred here).

---

## Key Takeaways

- Meta wants speed and bug-free standard Mediums.
- Google wants adaptability, Graphs, and DP.
- Amazon wants OOD, Heaps, and Tries alongside Leadership Principles.
- Adjust your study plan using LeetCode Premium's "Company Tags" in the final weeks before your interview.

---

## Related Topics

- [FAANG Interview Guide](../faang-interview-guide/01-index.md)
