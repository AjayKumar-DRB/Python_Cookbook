# Whiteboard vs Editor

> Surviving the transition from an IDE to a marker.

---

## Introduction

Since the pandemic, almost all FAANG interviews transitioned to remote shared editors (like CoderPad, HackerRank, or a shared Google Doc). 

However, if you are invited to an in-person onsite (which is making a comeback at companies like Meta and Apple), you might be forced to write code on a physical whiteboard.

---

## The Shared Editor (CoderPad)

In a remote interview, you will use a browser-based IDE.

**Pros:**
- Syntax highlighting.
- You can execute the code (sometimes).
- Easy to copy, paste, and refactor.

**Cons:**
- No autocomplete (usually disabled).
- You can't rely on a linter to catch your typos.

**Tips:**
- Practice on LeetCode with **autocomplete turned off**. You must know the exact spelling of `collections.defaultdict` or `heapq.heappush`.
- Write your algorithm plan in comments at the top of the file before coding.

---

## The Whiteboard

Whiteboarding is incredibly unnatural for developers. You cannot copy/paste, and inserting a line of code between two existing lines is a nightmare.

**Tips for the Whiteboard:**

1. **Start on the far left:** Most candidates start writing in the middle of the board and run out of room for indentation. Start as far left and as high up as possible.
2. **Leave blank lines:** Between major blocks of code (like after a loop), leave a physical gap on the board. This gives you space to insert code later if you find a bug.
3. **Use abbreviations (with permission):** Writing `collections.defaultdict(list)` takes a long time. Ask the interviewer: *"To save time, is it okay if I just write `defdict()`?"* They almost always say yes.
4. **Step back:** When dry running your code, physically step 3 feet back from the whiteboard. Looking at it from a distance helps you see the overall structure and spot missing `return` statements.

---

## The Google Doc

The absolute worst medium for coding is a Google Doc or plain text editor (still occasionally used by Google or Amazon).

- **The Problem:** It automatically capitalizes the first letter of new lines. It automatically replaces normal quotes `" "` with smart quotes `“ ”` (which causes syntax errors if you run the code later). The font is not monospaced, making indentation impossible to read.
- **The Fix:** Immediately turn off Auto-Capitalization and Smart Quotes in the settings before the interview starts. Change the font to Courier New or Consolas.

---

## Key Takeaways

- Disable autocomplete when practicing.
- On a whiteboard, leave physical space between lines so you can insert fixes later.
- If forced to use Google Docs, change the font to a monospaced font immediately.

---

## Related Topics

- [Coding Round](02-coding-round.md)
