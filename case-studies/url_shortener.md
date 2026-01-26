# Design a URL Shortener (TinyURL / Bit.ly)

A URL Shortener converts a long URL into a short URL.

Example:
https://www.amazon.in/products/books/fiction/harrypotter  
→ https://bit.ly/3AbX9Q

This is one of the most common system design interview questions.

---

## 1. Functional Requirements

The system should:
1. Generate a short URL from a long URL
2. Redirect short URL to original long URL
3. Support millions of users
4. Handle high read traffic
5. URLs should be unique
6. URLs should not expire (or optional TTL)

---

## 2. Non-Functional Requirements

- High availability
- Low latency
- Scalable
- Fault tolerant
- Secure
- Prevent abuse (rate limiting)

---

## 3. Capacity Estimation (Basic)

Assume:
- 10 million new URLs per day
- Read requests = 100 million per day

Storage:
- Each mapping ~ 500 bytes
- 10M * 500 bytes ≈ 5 GB per day

---

## 4. API Design

### Create Short URL



POST /api/v1/shorten


Request:
json
{
  "longUrl": "https://www.amazon.in/products/books/harrypotter"
}

Response:

{
  "shortUrl": "https://sho.rt/Ab3xY"
}


Redirect API
GET /{shortCode}

Response:

HTTP 302 Redirect to long URL


Client
  ↓
Load Balancer
  ↓
API Server
  ↓
Cache (Redis)
  ↓
Database (Sharded)


6. Database Design

Table: url_mapping


| Field              | Type      |
| ------------------ | --------- |
| id (PK)            | bigint    |
| short_code         | varchar   |
| long_url           | text      |
| created_at         | timestamp |
| user_id (optional) | bigint    |

Index:

short_code (unique index)


7. Short Code Generation Strategy


7. Short Code Generation Strategy

We need unique short codes.

Option 1: Base62 Encoding

Characters:

[a-z A-Z 0-9] = 62 characters


Convert auto-increment ID to Base62.

Example:

ID = 125
Base62 → "cb"


Short URL:

sho.rt/cb



8. Cache Design (Redis)

Use cache-aside pattern.

Key:

shortCode → longUrl


Flow:

Request comes

Check Redis

If hit → redirect

If miss → fetch from DB and cache

TTL:

Optional (eg. 24 hours)


9. Sharding Strategy

Shard by:

hash(short_code) % N


Why?

Even distribution

Avoid hot shard

10. Rate Limiting

Prevent abuse:

Limit URL creation per IP/user

Example: 100 URLs per hour

Return:

HTTP 429 Too Many Requests

11. Handling Collisions

If random code used:

Check DB

Retry generation

Better solution:

Use Base62 ID generation

12. Fault Tolerance

Multiple API servers

Replicated DB

Redis cluster

Load balancer health checks

13. Security

HTTPS only

Input validation

Prevent malicious URLs

Rate limiting

Auth for premium users

14. Bottlenecks & Solutions
Problem	Solution
DB overload	Redis cache
Hot shard	Hash-based sharding
Abuse	Rate limiting
High latency	CDN + cache
ID generation	Distributed ID generator
15. System Flow (End-to-End)
Create URL:
Client → API → DB → Base62 → Return short URL

Redirect:
Client → API → Redis → DB (if miss) → Redirect

16. Interview Questions You May Be Asked

How do you generate unique short URLs?

How do you scale the database?

What happens if Redis fails?

How do you avoid collisions?

How do you prevent abuse?

How do you handle millions of redirects?

17. Key Interview One-Liners

“We use Base62 encoding of auto-increment IDs to generate unique short URLs.”

“Redis cache reduces database load for frequent redirects.”

“Hash-based sharding evenly distributes data.”

“Rate limiting prevents abuse.”

“System is horizontally scalable using load balancers.”

18. Summary

REST APIs for create & redirect

Cache for performance

DB for persistence

Sharding for scale

Rate limiting for security

High availability with replicas

