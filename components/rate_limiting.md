# Rate Limiting & API Security (System Design)

Rate limiting is used to control how many requests a client can make
to a server in a given time window.

It protects systems from:
- Abuse
- DDoS attacks
- Overload
- Bots
- Infinite API calls

All real-world systems like WhatsApp, Uber, Netflix use rate limiting.

---

## 1. What is Rate Limiting?

Rate limiting restricts the number of requests a user or IP can make.

Example:
100 requests per minute per user


If user exceeds limit → request is rejected.

---

## 2. Why Rate Limiting is Needed

Without rate limiting:
- One user can crash the system
- Bots can overload APIs
- DDoS attacks succeed
- Resources get exhausted

With rate limiting:
- Fair usage
- System protection
- Better performance
- Improved reliability

---

## 3. Where is Rate Limiting Applied?

Rate limiting can be applied at:
- API Gateway
- Load Balancer
- Reverse Proxy (Nginx)
- Backend service

Most common: API Gateway or Reverse Proxy

---

## 4. Rate Limiting Strategies

### 1️⃣ Fixed Window Counter

Allow N requests per time window.

Example:
100 requests per minute


Problem:
- Traffic spike at window boundary

---

### 2️⃣ Sliding Window Log

Stores timestamp of each request.

More accurate than fixed window.

Problem:
- High memory usage

---

### 3️⃣ Sliding Window Counter

Hybrid approach:
- Uses counters
- Smooths traffic

---

### 4️⃣ Token Bucket (MOST COMMON) ⭐

- Tokens added at fixed rate
- Each request consumes token
- If no token → reject

Used by:
- AWS API Gateway
- Nginx
- Stripe APIs

---

### 5️⃣ Leaky Bucket

- Requests processed at constant rate
- Excess requests dropped

Used in network traffic shaping

---

## 5. Rate Limiting Key (What to limit?)

Rate limiting can be based on:
- IP address
- User ID
- API key
- Device ID

Example:
limit user_id to 100 requests/minute


---

## 6. Rate Limiting Responses

When limit exceeded, server returns:

HTTP 429 Too Many Requests


Headers:
Retry-After: 60


---

## 7. Rate Limiting Using Redis (Common Design)

Redis stores counters:

key = user:123:minute
value = 45


Flow:
1. Request comes
2. Increment Redis counter
3. Check limit
4. Allow or block request

Redis is used because:
- Fast
- Atomic operations
- TTL support

---

## 8. Distributed Rate Limiting (IMPORTANT)

In multi-server systems:
- Each server must share rate limit data

Solution:
- Central Redis
- Shared cache

---

## 9. Rate Limiting vs Throttling

| Feature | Rate Limiting | Throttling |
|--------|---------------|------------|
| Purpose | Block excess requests | Slow down requests |
| Result | Reject request | Delay response |
| Usage | API protection | Traffic shaping |

---

## 10. API Security Basics (Closely Related)

Rate limiting is part of API security.

Other protections:
- Authentication (JWT, OAuth)
- Authorization (RBAC)
- Input validation
- HTTPS
- Firewall
- WAF (Web Application Firewall)

---

## 11. Real-World Examples

### WhatsApp
- Limit messages per second
- Prevent spam

---

### Uber
- Limit ride requests
- Protect pricing APIs

---

### Netflix
- Limit login attempts
- Prevent brute force

---

### URL Shortener
- Limit URL creation per user
- Prevent abuse

---

## 12. Rate Limiting in System Design Architecture

Client
↓
API Gateway / Reverse Proxy
↓
Rate Limiter (Redis)
↓
Backend Services
↓
Database


---

## 13. Challenges in Rate Limiting

- Distributed systems
- Clock synchronization
- Burst traffic
- Fairness
- Memory usage

---

## 14. Interview Questions from Rate Limiting

1. What is rate limiting?
2. Why is rate limiting important?
3. Difference between throttling and rate limiting?
4. What is token bucket algorithm?
5. How do you implement rate limiting in distributed systems?
6. Why use Redis for rate limiting?

---

## 15. Key Interview One-Liners

- “Rate limiting protects systems from abuse and overload.”
- “Token bucket is the most commonly used algorithm.”
- “Redis is used for distributed rate limiting.”
- “HTTP 429 indicates too many requests.”
- “Rate limiting improves system reliability.”

---

## 16. Summary

- Rate limiting controls traffic
- Prevents abuse
- Improves stability
- Essential for public APIs
- Implemented using Redis or API gateways