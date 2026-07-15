# Debugging Under Pressure

> How to fix your code when the interviewer says "I don't think that's right."

---

## Introduction

In a real interview, you might hit "Run" and get a red `Exception` or `Wrong Answer`. Your heart rate spikes. You have 5 minutes left. 

How you react in this exact moment often determines if you get the offer or the rejection.

---

## 1. Do Not Panic

The worst thing you can do is start randomly changing variables (`i + 1` to `i - 1`) hoping it works. This is called "shotgun debugging" and it screams junior engineer.

Take a deep breath. Say out loud: *"Okay, we have a bug. Let me trace the execution to see where the state diverges from my expectation."*

---

## 2. Read the Error Message

If it's an exception (like `IndexError: list index out of range`), **read the line number**.
Go straight to that line. Ask yourself: *"Under what condition does this index exceed the length of the list?"*

Common Python Exceptions in interviews:
- **`IndexError`**: Loop went too far, or you forgot to check `if not nums`.
- **`KeyError`**: You tried to access `my_dict[val]` without checking `if val in my_dict`. Use `.get()` or `defaultdict`.
- **`RecursionError`**: You forgot a base case, or Python's 1000 limit was hit.
- **`TypeError: 'NoneType' object is not subscriptable`**: A function returned `None` when you expected an array, usually because you forgot a `return` statement in a recursive call.

---

## 3. Print Debugging

If the platform allows you to run code, use `print()` statements aggressively. But be systematic.

**Do not just print the variable.**
```python
print(i) # BAD: What is this?
print(f"Index i={i}, Current Value={nums[i]}") # GOOD: Explicit context
```

Place prints at the entry of loops, the exit of loops, and right before the `return` statement. This will narrow down exactly which block of code is failing.

---

## 4. The Interviewer's Hint

If the interviewer says: *"Are you sure about line 45?"*

**STOP.** They are literally handing you the answer. Do not argue. Do not say *"Yes, because..."*

Immediately look at line 45 and assume it is completely wrong. Say: *"Let me double-check line 45. Ah, I see, I'm using `<=` instead of `<`. Thank you for pointing that out."*

---

## Key Takeaways

- Never shotgun debug.
- Read the explicit error trace and line number.
- Use structured `print()` statements to track state.
- If the interviewer gives a hint, accept it immediately and act on it.

---

## Related Topics

- [Dry Running](07-dry-running.md)
