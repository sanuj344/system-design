# Caching in System Design (Redis & Cache Patterns)

Caching is one of the most important techniques in system design.
It improves performance, reduces database load, and enables systems
to scale efficiently.

Almost every large-scale system (Instagram, WhatsApp, Netflix)
uses caching heavily.

---

## 1. What is Caching?

Caching means storing **frequently accessed data** in a **fast storage layer**
so future requests can be served quickly.

Instead of:
Client → Database (slow)

We do:
Client → Cache (fast) → Database (only if needed)

---

## 2. Why Caching is Needed?

Databases are:
- Slow compared to memory
- Expensive at scale
- Hard to scale infinitely

Caching helps:
- Reduce latency
- Reduce database load
- Improve throughput
- Handle traffic spikes

---

## 3. Where Can We Cache Data?

### 1️⃣ Browser Cache
- Static assets (JS, CSS, images)
- Controlled by HTTP headers

---

### 2️⃣ CDN Cache
- Images, videos, static files
- Used by Netflix, Instagram

---

### 3️⃣ Server-Side Cache (MOST IMPORTANT)
- Redis
- Memcached

This is what system design interviews focus on.

---

## 4. Why Redis is Popular?

Redis is:
- In-memory (very fast)
- Key-value based
- Supports TTL (expiry)
- Supports data structures (list, set, hash)
- Horizontally scalable

Typical latency:
- Redis: ~1 ms
- Database: 10–100 ms

---

## 5. Basic Cache Flow (Interview Core)

Client
↓
Backend
↓
Cache (Redis) ── HIT ──→ Response
↓
MISS
↓
Database
↓
Cache Update
↓
Response


---

## 6. Cache Hit vs Cache Miss

### Cache Hit
- Data found in cache
- Very fast response
- No database call

---

### Cache Miss
- Data not found in cache
- Fetch from database
- Store in cache for future

---

## 7. Cache Patterns (VERY IMPORTANT)

### 1️⃣ Cache-Aside (Lazy Loading) ⭐ MOST COMMON

Steps:
1. Check cache
2. If miss → fetch from DB
3. Store in cache
4. Return response

Example:
GET user/123


Flow:
- Redis miss
- Query DB
- Save result in Redis
- Return data

✅ Simple  
✅ Widely used  
❌ Slight stale data risk

---

### 2️⃣ Write-Through Cache

Steps:
1. Write data to cache
2. Write data to database

✅ Cache always consistent  
❌ Slower writes

Used when consistency is critical.

---

### 3️⃣ Write-Back (Write-Behind) Cache

Steps:
1. Write to cache
2. Async write to database

✅ Very fast writes  
❌ Risk of data loss if cache crashes

Used in analytics, logs.

---

## 8. Cache Eviction Policies

Cache memory is limited. When full, data must be removed.

### Common eviction strategies:

- LRU (Least Recently Used) ⭐
- LFU (Least Frequently Used)
- FIFO

Redis commonly uses **LRU**.

---

## 9. TTL (Time To Live)

TTL defines **how long data stays in cache**.

Example:
user:123 → TTL = 5 minutes


After TTL expires:
- Data automatically removed
- Fresh data fetched next time

TTL helps avoid stale data.

---

## 10. Cache Invalidation (HARDEST PROBLEM)

When data changes, cache becomes outdated.

### Common strategies:

1️⃣ TTL-based expiration  
2️⃣ Explicit invalidation on update  
3️⃣ Versioned keys  

Example:
user:123:v2

Interview truth:
“There are only two hard things in CS: cache invalidation and naming.”

---

## 11. Caching in Real Systems

### Instagram Feed
- Cache recent posts
- Cache user profiles

---

### WhatsApp
- Cache user presence
- Cache recent messages

---

### URL Shortener
- Cache shortURL → longURL mapping

---

## 12. Cache Stampede Problem

Problem:
- Many requests hit cache miss simultaneously
- All hit database → DB overload

### Solutions:
- Locking
- Request coalescing
- Pre-warming cache

---

## 13. Cache Consistency vs Performance

Trade-off:
- Strong consistency → slower
- Eventual consistency → faster

Most large systems choose:
**Eventual consistency**

---

## 14. Cache Placement in System Design

Typical architecture:

Client
↓
Load Balancer
↓
Backend Service
↓
Redis Cache
↓
Database



---

## 15. Interview Questions from Caching

1. Why do we use caching?
2. What is Redis?
3. Cache hit vs cache miss?
4. Cache-aside vs write-through?
5. How do you handle cache invalidation?
6. What happens if Redis goes down?

---

## 16. Key Interview One-Liners

- “Caching reduces latency and database load.”
- “Redis is an in-memory key-value store used for fast access.”
- “Cache-aside is the most commonly used caching pattern.”
- “TTL helps prevent stale data.”
- “Eventual consistency is acceptable in most large systems.”

---

## 17. Summary

- Cache frequently accessed data
- Use Redis for server-side caching
- Prefer cache-aside pattern
- Handle invalidation carefully
- Accept eventual consistency
