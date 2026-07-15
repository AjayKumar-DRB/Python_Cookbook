# Probability Basics

> Randomness, shuffling, and expected value.

---

## Introduction

Probability questions in FAANG coding interviews are somewhat rare, but they do appear, especially for Data Engineering or Quant-heavy roles. The most famous probability coding question is the Fisher-Yates Shuffle.

---

## 1. Fisher-Yates Shuffle (Random Permutation)

If an interviewer asks you to "Shuffle an array randomly, such that every permutation is equally likely" (LeetCode 384: Shuffle an Array), you must use the Fisher-Yates shuffle algorithm.

The naive approach (picking random elements into a new array) often carries bias or requires $O(N^2)$ time to delete elements. Fisher-Yates runs in $O(N)$ time, $O(1)$ space, and is mathematically proven to be perfectly uniform.

### The Algorithm
Iterate through the array backwards. For each index `i`, pick a random index `j` from `0` to `i` (inclusive), and swap the elements at `i` and `j`.

```python
import random

def shuffle_array(nums: list[int]):
    n = len(nums)
    # Iterate backwards from the end
    for i in range(n - 1, 0, -1):
        # Pick a random index from 0 to i (inclusive)
        j = random.randint(0, i)
        # Swap
        nums[i], nums[j] = nums[j], nums[i]
```

*(Note: Python's built-in `random.shuffle(nums)` uses this exact algorithm under the hood!)*

---

## 2. Reservoir Sampling (Random item from a stream)

If an interviewer asks you to "Pick a random item from a stream of data where the total size is unknown, with uniform probability" (LeetCode 382: Linked List Random Node), you use Reservoir Sampling.

### The Algorithm
Maintain a variable `chosen_val`. Iterate through the stream, keeping track of the current count `i` (1-indexed). At the $i$-th item, generate a random number from $1$ to $i$. If the random number equals $1$, replace `chosen_val` with the current item.

```python
import random

def get_random_node(head) -> int:
    chosen_val = head.val
    curr = head.next
    i = 2
    
    while curr:
        # random.randint(1, i) generates a number between 1 and i
        if random.randint(1, i) == 1:
            chosen_val = curr.val
        curr = curr.next
        i += 1
        
    return chosen_val
```

**Why it works:**
The probability of picking the $i$-th element is $\frac{1}{i}$. The probability of it *surviving* the next iteration is $1 - \frac{1}{i+1} = \frac{i}{i+1}$. Through induction, the probabilities cancel out perfectly so every element has an exact $\frac{1}{N}$ chance of surviving at the end!

---

## Key Takeaways

- Use **Fisher-Yates** (`random.randint(0, i)` and swap) to shuffle an array uniformly in $O(N)$ time and $O(1)$ space.
- Use **Reservoir Sampling** (`random.randint(1, i) == 1`) to pick a random item from a stream of unknown length in $O(N)$ time and $O(1)$ space.

---

## Related Topics

- [Math Module](../standard-library/06-math.md)
