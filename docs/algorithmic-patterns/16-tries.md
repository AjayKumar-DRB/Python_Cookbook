# Tries (Prefix Trees)

## Introduction

A Trie (pronounced "try") is a specialized tree data structure used to efficiently store and retrieve keys in a dataset of strings.

It is heavily used in autocomplete systems, spell checkers, and IP routing.

---

## How to Recognize It

Use a Trie when:
- The problem involves **prefixes** of strings (e.g., "Find all words that start with 'app'").
- You need to search for many words in a massive dictionary simultaneously (e.g., Word Search II).
- You are dealing with bitwise XOR maximums (using a Binary Trie).

---

## The Pythonic Implementation

A Trie consists of `TrieNode`s. Instead of `left` and `right` pointers, a `TrieNode` has a dictionary of `children` mapping a character to the next node. It also has a boolean flag `is_end_of_word`.

```python
class TrieNode:
    def __init__(self):
        # Maps char -> TrieNode
        self.children = {}
        self.is_end_of_word = False

class Trie:
    def __init__(self):
        self.root = TrieNode()
        
    def insert(self, word):
        curr = self.root
        for char in word:
            if char not in curr.children:
                curr.children[char] = TrieNode()
            curr = curr.children[char]
        curr.is_end_of_word = True
        
    def search(self, word):
        curr = self.root
        for char in word:
            if char not in curr.children:
                return False
            curr = curr.children[char]
        return curr.is_end_of_word
        
    def starts_with(self, prefix):
        curr = self.root
        for char in prefix:
            if char not in curr.children:
                return False
            curr = curr.children[char]
        return True # The prefix exists
```

---

## Why use a Trie over a Hash Set?

If you just need to check if a whole word exists, a `set()` provides $O(1)$ lookup time, which is faster than a Trie's $O(L)$ time (where $L$ is word length).

However, a Hash Set **cannot** tell you if a *prefix* exists without iterating through every single word in the set. A Trie can do this in $O(L)$ time.

Furthermore, if many words share the same prefix (e.g., "car", "cart", "card", "care"), a Trie saves massive amounts of memory by only storing the prefix "car" once.

---

## Time and Space Complexity

Let $L$ be the length of the word and $N$ be the total number of words.
- **Time Complexity (Insert/Search/Prefix)**: $O(L)$. The time depends solely on the length of the word, independent of how many millions of words are in the Trie.
- **Space Complexity**: $O(N \times L)$ in the worst case (if no words share prefixes).

---

## Summary
- A Trie is a tree of characters.
- Each node contains a dictionary of children and a boolean `is_end_of_word`.
- Use it when you need to perform fast **prefix** lookups ($O(L)$ time).
