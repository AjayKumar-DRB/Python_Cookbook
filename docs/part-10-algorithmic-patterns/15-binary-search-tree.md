# Binary Search Tree (BST)

## Introduction

A Binary Search Tree is a specialized Binary Tree with a strict ordering property:
For any given node, **all values in its left subtree are strictly less than its value**, and **all values in its right subtree are strictly greater than its value**.

This property allows for incredibly fast lookups, insertions, and deletions ($O(\log N)$ on average).

---

## How to Recognize It

Use BST properties when:
- The problem explicitly states the tree is a Binary Search Tree.
- The problem asks you to find a value, find the closest value, or validate an ordering in a tree.
- You need an in-order sequence of sorted data.

---

## Key Concept 1: In-order Traversal

The most critical property of a BST is that an **in-order DFS traversal (Left, Node, Right) visits the nodes in perfectly sorted order**.

If a question asks you to validate a BST, or find the Kth smallest element, an in-order traversal is almost always the answer.

### Example: Validate BST
A clever way to validate a BST is to perform an in-order traversal and ensure that every element is strictly greater than the previous element.

```python
def is_valid_bst(root):
    def inorder(node):
        if not node:
            return True
            
        # Left Subtree
        if not inorder(node.left):
            return False
            
        # Current Node (Must be strictly greater than previous)
        if node.val <= inorder.prev:
            return False
        inorder.prev = node.val
        
        # Right Subtree
        return inorder(node.right)
        
    inorder.prev = float('-inf')
    return inorder(root)
```
*(Note: Using function attributes `inorder.prev` is a clean way to maintain state across recursive calls without using global variables).*

---

## Key Concept 2: Binary Search in a Tree

Searching in a BST is identical in concept to searching in a sorted array. You can eliminate half of the remaining tree at every step.

```python
def search_bst(root, val):
    curr = root
    
    while curr:
        if val == curr.val:
            return curr
        elif val < curr.val:
            # Value must be in the left subtree
            curr = curr.left
        else:
            # Value must be in the right subtree
            curr = curr.right
            
    return None # Not found
```

---

## Time and Space Complexity

- **Time Complexity (Search/Insert/Delete)**: $O(\log N)$ average case, $O(N)$ worst case (if the tree becomes skewed like a linked list).
- **Time Complexity (Traversal)**: $O(N)$ since you must visit every node.
- **Space Complexity**: $O(\log N)$ average case for the recursion stack during traversal, $O(1)$ for iterative search.

---

## Summary
- A BST guarantees: Left Subtree $<$ Node $<$ Right Subtree.
- An **In-order Traversal** yields a sorted list of values.
- You can search a BST iteratively in $O(1)$ space by comparing the target value to the current node and moving left or right.
