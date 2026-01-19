# Sharding & Partitioning in System Design

As systems grow, a single database becomes a bottleneck.
Sharding and partitioning are used to scale databases horizontally
by distributing data across multiple machines.

This is mandatory knowledge for designing systems like:
- WhatsApp
- Instagram
- Uber
- URL Shortener

---

## 1. Why Sharding is Needed

Problems with a single database:
- Limited storage
- Limited write throughput
- Single point of failure
- Slow queries on large tables

Vertical scaling (more RAM/CPU) has limits.
Horizontal scaling solves this.

---

## 2. What is Sharding?

Sharding means **splitting data across multiple databases (shards)**,
where each shard stores a **subset of the total data**.

Instead of:
One Big Database ❌

We use:
Shard 1 Shard 2 Shard 3 Shard 4


Each shard runs on a different machine.

---

## 3. Sharding vs Partitioning (IMPORTANT DISTINCTION)

### Partitioning
- Logical division of data
- Happens inside a single database
- Example: table partitioned by date

### Sharding
- Physical division of data
- Data stored on different machines
- Each shard is independent

Interview rule:
> “Partitioning is logical, sharding is physical.”

---

## 4. How Sharding Works (High-Level Flow)

Client
↓
Backend Service
↓
Shard Router / Logic
↓
Correct Database Shard


Backend decides **which shard** to query.

---

## 5. Shard Key (MOST IMPORTANT CONCEPT)

A **shard key** determines **where data is stored**.

### Good shard key properties:
- High cardinality
- Even distribution
- Frequently used in queries

---

### Common Shard Keys

#### 1️⃣ User ID (MOST COMMON)
shard_id = user_id % number_of_shards

Used in:
- WhatsApp
- Instagram
- Facebook

---

#### 2️⃣ Geographic Location
India → Shard A
US → Shard B


Used when data locality matters.

---

#### 3️⃣ Hash-Based Sharding
hash(user_id) % N


Ensures uniform distribution.

---

## 6. Types of Sharding Strategies

### 1️⃣ Range-Based Sharding

Example:
User IDs:
1–1M → Shard 1
1M–2M → Shard 2


✅ Simple  
❌ Hot shard problem

---

### 2️⃣ Hash-Based Sharding ⭐ (Preferred)

hash(key) % number_of_shards

✅ Even distribution  
❌ Hard to rebalance

---

### 3️⃣ Directory-Based Sharding

A lookup table maps:
user_id → shard_id


✅ Flexible  
❌ Extra lookup cost

---

## 7. Sharding Example (User Table)

Assume:
- 4 shards
- shard_key = user_id

user_id = 25
25 % 4 = 1 → Shard 1


All data for user 25 lives in Shard 1.

---

## 8. Sharding Problems (INTERVIEW FAVORITES)

### 1️⃣ Hot Shards

Problem:
- One shard receives most traffic

Example:
- Celebrity user with millions of followers

Solutions:
- Better shard key
- Split hot shard
- Caching

---

### 2️⃣ Re-Sharding (Very Hard)

Problem:
- Number of shards changes
- Data redistribution needed

Solutions:
- Consistent hashing
- Virtual shards

---

### 3️⃣ Cross-Shard Queries

Problem:
- Queries that need data from multiple shards
- Joins become difficult

Solution:
- Avoid cross-shard joins
- Do joins at application layer

---

## 9. Sharding vs Replication (CLEAR DIFFERENCE)

| Feature | Sharding | Replication |
|------|---------|-------------|
| Goal | Scale | Availability |
| Data | Split | Copied |
| Writes | Distributed | Single primary |
| Reads | From shard | From replicas |

Interview line:
> “Sharding scales writes, replication improves availability.”

---

## 10. Sharding + Replication (REAL SYSTEMS)

Each shard usually has replicas:

Shard 1 → Primary + Replicas
Shard 2 → Primary + Replicas
Shard 3 → Primary + Replicas


This gives:
- Horizontal scalability
- High availability

---

## 11. Sharding in Real Systems

### URL Shortener
- Shard by short URL hash

---

### WhatsApp
- Shard by user ID
- Messages for a user stay in one shard

---

### Instagram
- Shard by user ID
- Feed generated using fan-out strategy

---

## 12. When NOT to Use Sharding

- Low traffic systems
- Early-stage startups
- Simple CRUD apps

Rule:
> “Sharding is introduced only when a single database cannot scale.”

---

## 13. Interview Questions from Sharding

1. What is sharding?
2. Difference between sharding and partitioning?
3. What is a shard key?
4. What causes hot shards?
5. How do you handle re-sharding?
6. Sharding vs replication?

---

## 14. Key Interview One-Liners

- “Sharding horizontally scales databases by splitting data.”
- “A good shard key evenly distributes traffic.”
- “Hash-based sharding avoids hot shards.”
- “Re-sharding is one of the hardest database problems.”

---

## 15. Summary

- Sharding splits data across machines
- Choose shard key carefully
- Combine sharding with replication
- Avoid premature sharding
