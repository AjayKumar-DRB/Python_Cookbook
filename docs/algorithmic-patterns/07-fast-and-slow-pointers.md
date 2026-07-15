# Fast and Slow Pointers (Floyd's Cycle Detection)

## Introduction

The Fast and Slow Pointers pattern (also known as Floyd's Tortoise and Hare algorithm) is a variation of the Two Pointer pattern. It is primarily used to detect cycles in Linked Lists or Arrays.

---

## How to Recognize It

Use Fast and Slow Pointers when:
- You are dealing with Linked Lists and need to find the **middle node**.
- You need to determine if a **cycle exists** in a Linked List.
- The problem involves following a sequence of indices where an index points to the next index (e.g., "Find the Duplicate Number").

---

## Pattern 1: Cycle Detection

If there is a cycle, a fast pointer moving two steps at a time will eventually "lap" and meet the slow pointer moving one step at a time.

```python
def has_cycle(head):
    slow = head
    fast = head
    
    while fast and fast.next:
        slow = slow.next          # Move 1 step
        fast = fast.next.next     # Move 2 steps
        
        if slow == fast:
            return True           # They met! Cycle exists.
            
    return False                  # Fast reached the end
```

---

## Pattern 2: Finding the Middle

If a fast pointer moves twice as fast as a slow pointer, when the fast pointer reaches the end, the slow pointer will be exactly in the middle.

This is extremely useful for dividing a Linked List in half for Merge Sort, or for reversing the second half of a list (e.g., checking if a Linked List is a palindrome).

```python
def get_middle(head):
    slow = head
    fast = head
    
    # Check fast and fast.next to avoid NoneType errors
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        
    return slow # Slow is now at the middle node
```

---

## Time and Space Complexity

- **Time Complexity**: $O(N)$. In cycle detection, the fast pointer will catch the slow pointer in $O(N)$ time.
- **Space Complexity**: $O(1)$. We only use two node references.

---

## Summary
- Use `slow = slow.next` and `fast = fast.next.next`.
- If `slow == fast`, a cycle exists.
- When `fast` reaches the end, `slow` is at the middle.
- Always check `while fast and fast.next:` to prevent `AttributeError`s when `fast` hits the end of a non-cyclic list.
