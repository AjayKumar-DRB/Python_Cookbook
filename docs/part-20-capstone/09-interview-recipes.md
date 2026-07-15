# Capstone Interview Recipes

> Final reminders before you walk into the interview room.

---

## The Golden Rules

1. **Clarify before coding.** Never start typing until you have fully walked through an example and confirmed the edge cases with the interviewer.
2. **Talk about trade-offs.** If you jump straight to the $O(N)$ solution without acknowledging the $O(N^2)$ brute force approach, you lose points. Explain *why* you are using extra space.
3. **Beware Python's hidden complexities.** 
   - `in` on a list is $O(N)$. Convert to a `set` first.
   - `list.pop(0)` is $O(N)$. Use `collections.deque.popleft()`.
   - String concatenation in a loop is $O(N^2)$. Use `"".join(list)`.
4. **Dry run manually.** Treat the dry run as the most important part of the interview. Catching your own bug before execution is a strong "Hire" signal.
5. **Handle hints gracefully.** If an interviewer questions a line of code, assume you are wrong. Do not argue.

---

## System Design Cheat Sheet

- **Read Heavy?** Add a Cache (Redis/Memcached) and Read Replicas.
- **Write Heavy?** Add a Message Queue (Kafka) and Shard the Database.
- **Large Files/Media?** Use Object Storage (S3) and a CDN.
- **Latency Issues?** Move data closer to the user (CDN, Edge Computing).
- **Single Point of Failure?** Add Load Balancers and multiple instances in different Availability Zones.

---

## Python specific Interview Tips

- Use `float('inf')` and `float('-inf')` to initialize max/min trackers.
- Use `divmod(a, b)` if you need both the quotient and remainder.
- Python integers do not overflow, but if the problem expects a 32-bit integer, mask it with `& 0xFFFFFFFF`.
- Use `collections.defaultdict(list)` heavily in Graph problems to avoid `KeyError` checks.
- If you hit the recursion limit, you can technically use `sys.setrecursionlimit(2000)`, but it's better to rewrite it iteratively using a Stack.

---

## Final Words

Technical interviews evaluate preparation, not innate intelligence. 

If you have mastered the NeetCode 150 patterns, practiced the UMPIRE framework, and can communicate your thoughts clearly, you have everything you need to pass. 

Good luck.
