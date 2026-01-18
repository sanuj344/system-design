# DNS, Load Balancer & Reverse Proxy (From Basics)

Modern scalable systems depend on three critical components:
1. DNS (Domain Name System)
2. Load Balancer
3. Reverse Proxy

Without these, systems like WhatsApp, Uber, Netflix cannot scale.

---

## 1. DNS (Domain Name System)

### What is DNS?

DNS converts **human-readable domain names** into **IP addresses**.

Example:
instagram.com → 157.240.xxx.xxx

Computers communicate using IP addresses, not domain names.

---

### Why DNS is Needed?

- Humans remember names, not numbers
- Servers can change IPs
- DNS allows flexibility and scalability

---

### DNS Resolution Flow (Interview Favorite)

When you type:
https://instagram.com


Steps:
1. Browser checks local cache
2. OS checks DNS cache
3. Request sent to ISP DNS resolver
4. Resolver queries:
   - Root DNS server
   - TLD server (.com)
   - Authoritative DNS server
5. IP address returned to browser

---

### DNS Caching

DNS responses are cached at:
- Browser level
- OS level
- ISP level

This improves performance and reduces DNS traffic.

---

### Interview One-Liner:
“DNS resolves domain names to IP addresses and uses caching to improve performance.”

---

## 2. Load Balancer (CRITICAL COMPONENT)

### What is a Load Balancer?

A load balancer distributes incoming traffic across multiple backend servers.

Instead of:
Client → Server ❌

We use:
Client → Load Balancer → Server 1
→ Server 2
→ Server 3


---

### Why Load Balancers are Needed?

- Prevent server overload
- Improve availability
- Enable horizontal scaling
- Handle traffic spikes

---

### Types of Load Balancing Algorithms

#### 1️⃣ Round Robin
Requests distributed equally in rotation.

#### 2️⃣ Least Connections
Request goes to server with least active connections.

#### 3️⃣ IP Hash
Same client IP always goes to same server.

---

### Load Balancer Levels

#### L4 Load Balancer
- Works at transport layer
- Based on IP + port
- Faster but less intelligent

#### L7 Load Balancer
- Works at application layer
- Can inspect HTTP headers, URLs
- Used in modern web apps

---

### Popular Load Balancers

- Nginx
- HAProxy
- AWS ALB / NLB

---

### Health Checks

Load balancers continuously check:
- Is server alive?
- Is server responding?

Unhealthy servers are removed automatically.

---

### Interview One-Liner:
“Load balancers distribute traffic across multiple servers to improve scalability and fault tolerance.”

---

## 3. Reverse Proxy

### What is a Proxy?

A proxy sits between:
- Client and server

There are two types:
- Forward Proxy
- Reverse Proxy

---

## 4. Forward Proxy (Quick)

- Used by clients
- Hides client identity
- Example: Corporate proxy, VPN

---

## 5. Reverse Proxy (VERY IMPORTANT)

A reverse proxy sits **in front of backend servers**.

Flow:
Client → Reverse Proxy → Backend Servers


Client does NOT know backend servers exist.

---

### What Does a Reverse Proxy Do?

- SSL termination
- Request routing
- Caching
- Security filtering
- Rate limiting

---

### Nginx as Reverse Proxy (Most Common)

Nginx can:
- Act as reverse proxy
- Act as load balancer
- Serve static files
- Handle SSL

---

### Example Flow (Real World)

Client
↓
DNS
↓
Reverse Proxy (Nginx)
↓
Load Balancer
↓
Backend Services
↓
Database / Cache


---

### Reverse Proxy vs Load Balancer

| Feature | Reverse Proxy | Load Balancer |
|------|---------------|---------------|
| Entry point | Yes | Yes |
| Routes traffic | Yes | Yes |
| SSL termination | Yes | Sometimes |
| Focus | Security + routing | Traffic distribution |

---

### Interview One-Liner:
“A reverse proxy sits in front of servers and handles routing, security, and SSL termination.”

---

## 6. How DNS + LB + Proxy Work Together

Example:
api.instagram.com


1. DNS resolves domain → IP
2. Request reaches reverse proxy
3. Reverse proxy forwards to load balancer
4. Load balancer selects backend server
5. Backend processes request

---

## 7. Why This Matters in System Design

Every scalable system includes:
- DNS for discovery
- Load balancer for scalability
- Reverse proxy for control

Without these:
- Single server failure crashes system
- No scaling
- Poor performance

---

## 8. Interview Questions from This Topic

1. What is DNS and why is it needed?
2. How does DNS resolution work?
3. What is a load balancer?
4. Difference between L4 and L7 load balancer?
5. What is a reverse proxy?
6. Difference between reverse proxy and load balancer?

---

## 9. Key Interview One-Liners

- “DNS maps domain names to IP addresses.”
- “Load balancers distribute traffic across multiple servers.”
- “Reverse proxies handle routing, security, and SSL termination.”
- “L7 load balancers operate at the HTTP level.”

---

## 10. Summary

DNS finds servers  
Load balancers distribute traffic  
Reverse proxies control access  

Together, they form the backbone of scalable backend systems.
