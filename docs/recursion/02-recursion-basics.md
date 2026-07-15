# Recursion Basics

> Recursion is simply a function that calls itself until it reaches a stopping condition.

---

## Introduction

Understanding the mechanics of a recursive function is essential before tackling tree traversals or backtracking. Every recursive function consists of two mandatory parts: the **Base Case** and the **Recursive Step**.

---

## What is it?

A recursive function breaks a problem down into smaller instances of the same problem. 

Think of it like standing in a line of people and wanting to know how many people are in front of you. Instead of walking to the front and counting, you ask the person directly in front of you: *"How many people are in front of you?"* 
They don't know either, so they ask the person in front of them, and so on. 
When the person at the very front is asked, they can definitively say *"Zero"* (the **Base Case**). The answer is then passed back down the line, with each person adding `1` to the number they received (the **Recursive Step**).

---

## Anatomy of a Recursive Function

Every recursive function follows this template:

```python
def recursive_function(parameters):
    # 1. Base Case(s)
    if stopping_condition:
        return base_result
    
    # 2. Recursive Step
    # Do some work, and call the function with a smaller input
    result = recursive_function(smaller_parameters)
    
    # 3. Combine/Return
    return combined_result
```

---

## Time Complexity

| Case | Complexity |
|------|------------|
| General | $O(\text{branches}^{\text{depth}})$ or $O(\text{Number of Recursive Calls})$ |

Time complexity in recursion depends entirely on how many times the function calls itself.

---

## Space Complexity

| Case | Complexity |
|------|------------|
| Worst Case | $O(H)$ where $H$ is the maximum depth of the recursive calls |

Every time a function calls itself, Python must allocate memory on the Call Stack to store local variables and the return address. This memory is released only when the base case is reached and the functions start returning.

---

## Basic Example: Factorial

The classic example of recursion is calculating the factorial of a number $n$ (written as $n!$).
$5! = 5 \times 4 \times 3 \times 2 \times 1$

Notice that $5! = 5 \times 4!$. This perfectly matches our definition of solving a problem using a smaller instance of the same problem!

```python
def factorial(n: int) -> int:
    # 1. Base Case: 0! is 1 (and 1! is 1)
    if n <= 1:
        return 1
        
    # 2 & 3. Recursive Step and Combine
    return n * factorial(n - 1)

print(factorial(5)) # 120
```

---

## The "Leap of Faith"

The most common mistake beginners make is trying to mentally trace every single function call all the way down to the base case and back up. This is exhausting and prone to error.

Instead, take the **Leap of Faith**:
1. Prove your base case is correct.
2. Assume the recursive call returns the correct answer for the smaller problem.
3. Prove that *if* the recursive call is correct, your current function will return the correct answer.

In the `factorial` example:
1. `factorial(1)` returns `1`. (Correct)
2. Assume `factorial(4)` returns `24`.
3. Does `5 * factorial(4)` yield `120`? Yes. 

You don't need to manually trace how `factorial(4)` got `24`. Just trust that it does.

---

## Common Pitfalls

- **Missing or Incorrect Base Case:** This leads to infinite recursion and a `RecursionError: maximum recursion depth exceeded`.
- **Not Returning the Recursive Call:** If you call the function but don't `return` its result, you will lose the computed value and return `None`.

```python
# BAD: Missing return statement
def bad_factorial(n):
    if n <= 1:
        return 1
    bad_factorial(n - 1) # BUG: Result is lost!

print(bad_factorial(5)) # None
```

---

## Best Practices

- Always define your base case(s) first.
- Ensure the arguments you pass to the recursive call bring it closer to the base case (e.g., `n - 1`).
- Practice the "Leap of Faith" instead of manual tracing for complex problems.

---

## Key Takeaways

- Recursion is a function calling itself with smaller inputs.
- Every recursive function needs a base case to prevent infinite loops.
- Recursion inherently consumes memory due to the call stack.

---

## Related Topics

- [Base Case](04-base-case.md)
- [Call Stack](05-call-stack.md)
- [Recursion Tree](03-recursion-tree.md)
