# LeetCode Pattern Guide

Use this guide to identify which algorithm to use based on keywords in the problem description.

## 1. Arrays & Strings
- **"Sorted Array"** $\rightarrow$ Binary Search OR Two Pointers
- **"Subarray" / "Contiguous Subarray"** $\rightarrow$ Sliding Window OR Prefix Sum
- **"Next Greater Element" / "Previous Smaller"** $\rightarrow$ Monotonic Stack
- **"Palindromes"** $\rightarrow$ Two Pointers (Converging) OR DP

## 2. Linked Lists
- **"Cycle" / "Middle Element"** $\rightarrow$ Fast & Slow Pointers
- **"Kth from End"** $\rightarrow$ Two Pointers (Separated by K)
- **"Merge Sorted Lists"** $\rightarrow$ Dummy Node + Two Pointers

## 3. Trees
- **"Level Order" / "Shortest Path"** $\rightarrow$ BFS (Queue)
- **"Validate BST" / "Kth Smallest"** $\rightarrow$ In-Order Traversal (DFS)
- **"Path Sum"** $\rightarrow$ Pre-Order Traversal (DFS)

## 4. Graphs
- **"Shortest Path (Unweighted)"** $\rightarrow$ BFS
- **"Connected Components" / "Islands"** $\rightarrow$ DFS OR Union-Find
- **"Prerequisites" / "Task Scheduling"** $\rightarrow$ Topological Sort
- **"Cycle Detection"** $\rightarrow$ Union-Find (Undirected) OR DFS with States (Directed)

## 5. Optimization & Combinatorics
- **"Top K" / "Kth Largest"** $\rightarrow$ Heap
- **"All Permutations" / "All Combinations"** $\rightarrow$ Backtracking
- **"Max/Min Value" / "Number of Ways"** (with overlapping subproblems) $\rightarrow$ Dynamic Programming
- **"Max Overlapping Intervals"** $\rightarrow$ Sort by Start/End Time + Greedy
