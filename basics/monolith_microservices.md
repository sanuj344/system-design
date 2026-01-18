# Monolith vs Microservices & Scalability Basics

Understanding application architecture is critical in system design.
Most real-world systems start as monoliths and evolve into microservices
as scale increases.

---

## 1. What is a Monolithic Architecture?

A monolith is a **single, unified application** where:
- Frontend
- Backend logic
- Database access
- Authentication
- Payments

all live in **one codebase and one deployment**.

---

### Example Monolith

Client
↓
Backend Application
├── Auth Module
├── User Module
├── Payment Module
└── Order Module
↓
Single Database


---

### Advantages of Monolith

- Simple to develop
- Easy to deploy
- Easier debugging
- Ideal for startups and MVPs

---

### Disadvantages of Monolith

- Hard to scale individual features
- One bug can crash entire system
- Slower deployments as app grows
- Tight coupling between modules

---

### When to Use Monolith?

- Early-stage product
- Small team
- Low traffic
- Fast iteration needed

---

## 2. What are Microservices?

Microservices architecture splits the application into **small, independent services**.

Each service:
- Handles a single responsibility
- Has its own codebase
- Can be deployed independently
- Often has its own database

---

### Example Microservices Architecture

Client
↓
API Gateway
↓
Auth Service User Service Payment Service
↓ ↓ ↓
Auth DB User DB Payment DB


---

### Advantages of Microservices

- Independent scaling
- Fault isolation
- Faster deployments
- Better for large teams

---

### Disadvantages of Microservices

- Complex infrastructure
- Network latency
- Data consistency challenges
- Requires DevOps maturity

---

### When to Use Microservices?

- High traffic systems
- Large engineering teams
- Independent scaling required
- Long-term products

---

## 3. Monolith vs Microservices (Comparison)

| Feature | Monolith | Microservices |
|------|---------|---------------|
| Codebase | Single | Multiple |
| Deployment | Single unit | Independent |
| Scalability | Whole app | Per service |
| Complexity | Low | High |
| Best for | Startups | Large-scale systems |

---

## 4. Real-World Evolution (IMPORTANT)

Most companies follow this path:

Monolith → Modular Monolith → Microservices


Example:
- Amazon
- Netflix
- Uber

They did NOT start with microservices.

---

## 5. What is Scalability?

Scalability is the system’s ability to handle **increased load** without performance degradation.

---

## 6. Types of Scalability

### 1️⃣ Vertical Scaling (Scale Up)

- Increase CPU, RAM
- Single machine

Example:
4GB RAM → 32GB RAM


❌ Limited  
❌ Expensive  
❌ Single point of failure

---

### 2️⃣ Horizontal Scaling (Scale Out)

- Add more servers
- Distribute traffic

Example:
1 server → 10 servers


✅ Preferred  
✅ Fault tolerant  
✅ Cost effective

---

## 7. Stateless vs Stateful Services

### Stateless Service
- Does not store session data
- Easy to scale
- Uses JWT, Redis, DB

Example:
- REST APIs

---

### Stateful Service
- Stores client state
- Hard to scale
- Requires session affinity

Example:
- In-memory sessions

---

### Interview Line:
“Stateless services scale better in distributed systems.”

---

## 8. Scaling a Backend System (High-Level)

Basic scalable backend flow:

Client
↓
Load Balancer
↓
Stateless Backend Services
↓
Cache (Redis)
↓
Database


---

## 9. Single Point of Failure (SPOF)

A SPOF is a component whose failure crashes the system.

Examples:
- Single server
- Single database
- Single load balancer

### Solution:
- Replication
- Redundancy
- Failover

---

## 10. Interview Questions from This Topic

1. What is a monolith?
2. Why not start with microservices?
3. Difference between vertical and horizontal scaling?
4. What is a stateless service?
5. What is a single point of failure?

---

## 11. Key Interview One-Liners

- “Monoliths are easier to build; microservices are easier to scale.”
- “Horizontal scaling is preferred for large systems.”
- “Stateless services simplify scaling and fault tolerance.”
- “Microservices introduce operational complexity.”

---

## 12. Summary

- Start simple with monolith
- Scale horizontally using load balancers
- Move to microservices only when required
- Avoid premature optimization
