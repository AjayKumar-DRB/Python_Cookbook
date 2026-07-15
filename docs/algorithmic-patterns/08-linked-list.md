# Linked Lists

## Introduction

A Linked List is a linear data structure where elements (nodes) are not stored in contiguous memory locations. Instead, each node points to the next node.

In Python interviews, you will rarely need to implement a full Linked List class from scratch. Instead, the interviewer will provide a simple `ListNode` class, and you will manipulate the pointers.

---

## The Standard `ListNode`

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next
```

---

## Key Concept 1: The Dummy Node

The most important pattern for Linked List problems is the **Dummy Node**. 

When a problem asks you to delete nodes, merge lists, or reverse parts of a list, the *head* of the list might change. Managing edge cases where the head changes is notoriously bug-prone.

A Dummy Node is a fake node placed *before* the head. It guarantees that the head always has a previous node, eliminating edge cases.

### Example: Remove elements with a specific value
```python
def remove_elements(head, val):
    # 1. Create dummy node pointing to head
    dummy = ListNode(next=head)
    
    # 2. Use a pointer starting at dummy
    current = dummy
    
    while current.next:
        if current.next.val == val:
            # Bypass the node to delete it
            current.next = current.next.next
        else:
            current = current.next
            
    # 3. Return dummy.next (the true head)
    return dummy.next
```

---

## Key Concept 2: Multiple Pointers

Because you cannot access elements by index in $O(1)$ time, Linked List problems frequently rely on Two Pointers.

1. **Fast and Slow Pointers**: Used to find the middle of the list or detect cycles (covered in the Fast and Slow Pointers section).
2. **Prev, Curr, Next Pointers**: Used to reverse a linked list.

### Example: Reversing a Linked List
This is a mandatory algorithm to memorize.

```python
def reverse_list(head):
    prev = None
    curr = head
    
    while curr:
        # 1. Save the next node
        next_temp = curr.next
        
        # 2. Reverse the pointer
        curr.next = prev
        
        # 3. Move pointers forward
        prev = curr
        curr = next_temp
        
    return prev # prev is the new head
```

---

## Common Gotchas (AttributeErrors)

The most common mistake in Linked List interviews is raising an `AttributeError: 'NoneType' object has no attribute 'next'`.

Always check that a node is not `None` before checking `node.next`.

**Incorrect:**
```python
while node.next: # Will crash if node is None!
    # ...
```

**Correct:**
```python
while node and node.next: 
    # ...
```

---

## Summary
- Use a **Dummy Node** (`dummy = ListNode(next=head)`) whenever the head of the list might change or be deleted. Return `dummy.next`.
- Memorize the **Reverse a Linked List** pattern (`prev, curr, next_temp`).
- Always guard against `AttributeError` by checking if the node exists before accessing `.next`.
