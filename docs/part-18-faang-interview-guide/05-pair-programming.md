# Pair Programming

> Interviewing as a teammate, not a test subject.

---

## Introduction

Modern technical interviews are moving away from the adversarial "quiz" format. Instead, companies like Stripe, Netflix, and heavily engineering-focused startups use the **Pair Programming** interview.

In this format, the interviewer acts as your coworker. You are given a real-world codebase and asked to build a feature or fix a bug *together*.

---

## What to Expect

Instead of LeetCode algorithms on a blank CoderPad, you will usually be given a repo to clone, or a fully functional Replit environment.

The tasks are usually practical:
- Parse a JSON file and aggregate data.
- Build a rate limiter class.
- Fix a failing unit test in an existing API endpoint.

---

## How to Succeed

### 1. Drive, but ask for directions
You are the "driver" (the one typing). The interviewer is the "navigator". You should constantly explain what you are doing, but if you get stuck on a library detail, ask!

*"I know I need to parse this timestamp, but I don't remember the exact `datetime` format string off the top of my head. Can I Google it, or do you happen to know?"*

A good interviewer will happily give you the answer because that's what a real coworker would do.

### 2. Google is often allowed (but ask first)
In pair programming rounds, interviewers often encourage you to use Google or Stack Overflow, just like in real life. However, always ask for permission first.

Do not use Google to search for the exact answer to the prompt. Use it to search for syntax (e.g. *"Python read CSV into dict"*).

### 3. Emphasize Clean Code
Because this simulates real work, variable names and code structure matter immensely.
Do not use `x`, `y`, or `res`. Use `parsed_records` or `user_id_map`.
Extract logic into helper functions.

---

## Common Pitfalls

- **Going silent:** If you treat this like an OA and just code in silence, you will fail the collaboration aspect.
- **Ignoring the interviewer's suggestions:** If the interviewer says *"What if we extracted that into a function?"*, do it immediately. They are testing how receptive you are to code review.

---

## Key Takeaways

- Treat the interviewer like a senior engineer pairing with you.
- Write clean, production-ready code with good variable names.
- Ask for syntax help if you need it; don't waste 10 minutes guessing.

---

## Related Topics

- [Coding Round](02-coding-round.md)
- [Communicating Your Solution](../part-16-systematic-problem-solving/09-communicating-your-solution.md)
