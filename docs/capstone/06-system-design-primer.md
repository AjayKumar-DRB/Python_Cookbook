# System Design Primer

> Designing distributed systems at scale.

---

## Introduction

If you are interviewing for a Mid-Level (L4) or Senior (L5) position, you will face a System Design round.

Unlike the Coding round where there is a mathematically optimal answer, System Design has no "correct" answer. It is an open-ended discussion about trade-offs, bottlenecks, and architecture.

You will be asked a question like: *"Design Twitter."* or *"Design a URL Shortener."*

---

## The 45-Minute Framework

Just like the UMPIRE framework for coding, you need a strict framework for System Design to prevent the conversation from devolving into chaos.

### 1. Requirements Clarification (5 mins)
Never start drawing boxes immediately. Clarify the scope.
- **Functional:** What exactly does the system do? (e.g. Users can post tweets, users can follow others, users can see a timeline).
- **Non-Functional:** What are the constraints? (e.g. High availability, low latency, 100 million DAU (Daily Active Users), heavy read-to-write ratio).

### 2. Back-of-the-Envelope Estimation (5 mins)
Calculate the scale.
- How many Tweets per second? (Write QPS).
- How many Timeline reads per second? (Read QPS).
- How much storage do we need for 5 years of media?
*(Tip: Always round numbers to make the math easy in your head. 100M users / 100k seconds in a day = 1000 requests per second).*

### 3. API Design (5 mins)
Define the core endpoints.
- `postTweet(user_id, text, media_url)` -> `201 Created`
- `getTimeline(user_id, page_token)` -> `200 OK`, JSON list of tweets.

### 4. High-Level Design (10 mins)
Draw the core components on the whiteboard (or Excalidraw).
- Client -> Load Balancer -> API Gateway -> Web Servers -> Database.
- Don't worry about scale yet, just make the "Happy Path" work for 1 user.

### 5. Deep Dive & Bottlenecks (20 mins)
The interviewer will start poking holes in your design. *"What happens when Taylor Swift tweets and 50 million people try to read it at once?"*
This is where you prove you are a Senior Engineer.
- **Caching:** Add a Redis cluster between the Web Servers and the DB.
- **Database Scaling:** Shard the database by `user_id`. Add read replicas.
- **Message Queues:** Use Kafka or RabbitMQ to decouple slow tasks (like image processing) from the main API thread.
- **CDNs:** Serve static images globally from a CDN to reduce latency.

---

## Core Concepts to Memorize

You must deeply understand the trade-offs of the following technologies:

1. **Relational (SQL) vs NoSQL Databases:**
   - SQL (PostgreSQL, MySQL): ACID compliant, rigid schema, good for complex joins (e.g. Financial transactions). Hard to scale horizontally.
   - NoSQL (Cassandra, DynamoDB): Eventually consistent, flexible schema, massive horizontal scalability. Bad for joins.
2. **CAP Theorem:** You can only pick two of Consistency, Availability, and Partition Tolerance. In distributed systems (where P is a given), you must choose between CP (accurate data, might go down) or AP (always up, data might be stale).
3. **Caching Strategies:** Write-through, Write-around, Cache Aside. LRU eviction policies.

---

## Key Takeaways

- System Design is about discussing trade-offs, not writing code.
- Always clarify functional and non-functional requirements first.
- The answer to almost every scaling problem involves some combination of Load Balancers, Read Replicas, Caching, and Message Queues.

---

## Related Topics

- [Concurrency Basics](08-concurrency-basics.md)
