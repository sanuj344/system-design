# Databases in System Design (Interview-Level)

Databases are the backbone of backend systems.
Every system design problem requires choosing the right database,
designing the schema correctly, and scaling it safely.

---

## 1. Why Databases Matter in System Design

Databases store:
- Users
- Messages
- Orders
- Payments
- Metadata

Bad database design leads to:
- Slow queries
- Downtime
- Data inconsistency
- Scaling failures

---

## 2. Types of Databases (Big Picture)

Databases are broadly classified into:
1. SQL (Relational)
2. NoSQL (Non-relational)

---

## 3. SQL Databases (Relational Databases)

Examples:
- PostgreSQL
- MySQL
- Oracle

### Characteristics:
- Fixed schema
- Tables with rows & columns
- Strong consistency
- ACID transactions
- Supports joins

---

### ACID Properties (IMPORTANT)

- **A – Atomicity**: Transaction is all or nothing
- **C – Consistency**: DB remains valid after transaction
- **I – Isolation**: Concurrent transactions don’t interfere
- **D – Durability**: Data persists after commit

---

### When to Use SQL?

Use SQL when:
- Data relationships are important
- Transactions are critical
- Strong consistency is required

Examples:
- Banking
- Payments
- Orders
- Inventory

---

## 4. NoSQL Databases

Examples:
- MongoDB (Document)
- Redis (Key-Value)
- Cassandra (Wide-column)
- DynamoDB

---

### Characteristics:
- Flexible schema
- Horizontally scalable
- High availability
- Eventual consistency
- No joins (usually)

---

### Types of NoSQL Databases

#### 1️⃣ Key-Value Stores
- Redis
- DynamoDB

Used for:
- Caching
- Sessions
- Rate limiting

---

#### 2️⃣ Document Databases
- MongoDB

Used for:
- User profiles
- Content data
- Flexible JSON structures

---

#### 3️⃣ Wide Column Stores
- Cassandra

Used for:
- Time-series data
- Analytics
- Large-scale writes

---

## 5. SQL vs NoSQL (INTERVIEW TABLE)

| Feature | SQL | NoSQL |
|------|-----|-------|
| Schema | Fixed | Flexible |
| Transactions | Strong | Limited |
| Joins | Supported | Not supported |
| Scaling | Vertical | Horizontal |
| Consistency | Strong | Eventual |
| Best For | Payments | Social apps |

---

## 6. Schema Design Basics (VERY IMPORTANT)

### Goals of Schema Design:
- Minimize redundancy
- Ensure data integrity
- Optimize query performance

---

### Example: User Table (SQL)

users

id (PK)
name
email (unique)
password_hash
created_at


---

### Example: Orders Table

orders

id (PK)
user_id (FK)
amount
status
created_at


---

## 7. Normalization vs Denormalization

### Normalization
- Split data into multiple tables
- Avoid duplication

✅ Data integrity  
❌ Slower reads (joins)

---

### Denormalization
- Duplicate data
- Fewer joins

✅ Faster reads  
❌ Data inconsistency risk

---

### Interview Rule:
- OLTP systems → normalized
- Read-heavy systems → denormalized

---

## 8. Indexing (CRITICAL FOR PERFORMANCE)

Indexes speed up **read queries**.

Without index:
- Full table scan ❌

With index:
- Logarithmic search ✅

---

### Common Index Types

#### 1️⃣ B-Tree Index (Most Common)
- Used for range queries
- Default in SQL databases

---

#### 2️⃣ Hash Index
- Fast equality checks
- Not good for range queries

---

#### 3️⃣ Composite Index
- Index on multiple columns

Example:
INDEX (user_id, created_at)


---

### Index Trade-Offs

✅ Faster reads  
❌ Slower writes  
❌ More storage

---

## 9. Replication (High Availability)

Replication means copying data across multiple DB instances.

### Why Replication?
- High availability
- Read scalability
- Fault tolerance

---

### Primary–Replica Model
Primary DB (writes)
↓
Replica DBs (reads)


Reads go to replicas, writes go to primary.

---

### Problems with Replication
- Replication lag
- Stale reads

---

## 10. Consistency Models

### Strong Consistency
- Reads always see latest data
- Slower

Used in:
- Payments
- Banking

---

### Eventual Consistency
- Reads may be stale temporarily
- Faster

Used in:
- Social media
- Feeds
- Likes

---

## 11. Database Bottlenecks

Common DB bottlenecks:
- Too many writes
- Missing indexes
- Large tables
- Hot partitions

---

## 12. How Databases Fit in System Design

Typical architecture:

Client
↓
Load Balancer
↓
Backend Service
↓
Cache (Redis)
↓
Primary Database
↓
Read Replicas


---

## 13. Interview Questions from Databases

1. SQL vs NoSQL?
2. What is ACID?
3. What is indexing?
4. When does indexing hurt performance?
5. What is replication?
6. Strong vs eventual consistency?

---

## 14. Key Interview One-Liners

- “SQL databases provide strong consistency and transactions.”
- “NoSQL databases scale horizontally with eventual consistency.”
- “Indexes improve read performance but slow writes.”
- “Replication improves availability and read scalability.”

---

## 15. Summary

- Choose DB based on use case
- Design schema carefully
- Use indexes wisely
- Replicate for availability
- Cache before database

