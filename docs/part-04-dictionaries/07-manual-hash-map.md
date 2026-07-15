# Implementing a Hash Map Manually

## Introduction

"Design a Hash Map" is a classic interview question (e.g., LeetCode 706). Interviewers ask this to test your understanding of hashing, collision resolution, and underlying data structures.

You cannot use the built-in `dict` to solve this problem. You must build it from scratch using arrays and (usually) linked lists.

---

## The Concept: Separate Chaining

To build a Hash Map, you need:
1. A **fixed-size array** (often called "buckets").
2. A **hash function** to convert a key into an array index.
3. A way to handle **collisions** (when two keys hash to the same index).

The most common way to handle collisions in interviews is **Separate Chaining**. Instead of storing the value directly in the array, each array index holds a List (or Linked List) of `(key, value)` pairs.

---

## Step-by-Step Implementation

### Step 1: Initialization
Create an array of a fixed size. A prime number (like 1009) is often chosen to reduce collisions, though a power of 2 (like 1024) is also common. Each bucket starts as an empty list.

```python
class MyHashMap:
    def __init__(self):
        self.size = 1009
        self.buckets = [[] for _ in range(self.size)]
```
*(Note: Be sure to use `[[] for _ in range(self.size)]` and NOT `[[]] * self.size`!)*

### Step 2: The Hash Function
Define a helper method to calculate the index.

```python
    def _hash(self, key):
        return hash(key) % self.size
```

### Step 3: Put (Insert or Update)
Hash the key to find the bucket. Iterate through the list in that bucket. If the key exists, update its value. If it doesn't, append a new `(key, value)` tuple.

```python
    def put(self, key: int, value: int) -> None:
        index = self._hash(key)
        bucket = self.buckets[index]
        
        for i, (k, v) in enumerate(bucket):
            if k == key:
                bucket[i] = (key, value) # Update existing
                return
                
        bucket.append((key, value)) # Insert new
```

### Step 4: Get (Retrieve)
Hash the key to find the bucket. Iterate through the bucket to find the key.

```python
    def get(self, key: int) -> int:
        index = self._hash(key)
        bucket = self.buckets[index]
        
        for k, v in bucket:
            if k == key:
                return v
                
        return -1 # Key not found
```

### Step 5: Remove
Find the bucket, iterate through it, and remove the tuple if the key matches.

```python
    def remove(self, key: int) -> None:
        index = self._hash(key)
        bucket = self.buckets[index]
        
        for i, (k, v) in enumerate(bucket):
            if k == key:
                del bucket[i]
                return
```

---

## Time and Space Complexity

Let $N$ be the number of keys inserted and $K$ be the number of buckets (`self.size`). The average number of elements per bucket is $N/K$ (the Load Factor).

- **Time Complexity** (Put, Get, Remove): 
  - **Average**: $O(1)$ assuming a good hash function and low load factor.
  - **Worst-case**: $O(N)$ if every single key hashes to the exact same bucket.
- **Space Complexity**: $O(N + K)$ to store the array of buckets and all inserted elements.

---

## Summary
- Know how to implement a hash map using an array of lists (Separate Chaining).
- Understand that the core mechanic is `index = hash(key) % array_size`.
- Always iterate through the bucket to check if a key already exists before inserting.
