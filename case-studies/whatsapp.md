# Design WhatsApp (Chat Messaging System)

WhatsApp is a real-time messaging system that allows users to:
- Send messages
- Receive messages instantly
- See online/offline status
- Support millions of users
- Ensure message delivery

This is one of the most asked system design questions.

---

## 1. Functional Requirements

The system should:
1. Send messages between users
2. Support one-to-one chat (for now)
3. Deliver messages in real-time
4. Store chat history
5. Show online/offline status
6. Support message retry if user is offline

---

## 2. Non-Functional Requirements

- Low latency (real-time)
- High availability
- Scalable to millions of users
- Fault tolerant
- Reliable message delivery
- Secure (encryption, auth)

---

## 3. High-Level Architecture

Client (Mobile App)
↓
Load Balancer
↓
WebSocket Servers (Chat Servers)
↓
Message Queue (Kafka / RabbitMQ)
↓
Message Service
↓
Database (Sharded)
↓
Cache (Redis)


---

## 4. Communication Protocol

WhatsApp uses:
- WebSockets (persistent connection)
instead of HTTP polling.

Why WebSockets?
- Server can push messages instantly
- Low latency
- Persistent connection

---

## 5. API Design

### Send Message API
POST /api/v1/messages


Request:
```json
{
  "senderId": "123",
  "receiverId": "456",
  "message": "Hello"
}
Response:

{
  "status": "sent"
}
Fetch Chat History
GET /api/v1/messages?user1=123&user2=456
6. Message Flow (Online User)
User A → WebSocket Server → Message Queue → WebSocket Server → User B
Steps:

User A sends message

Message pushed to queue

Message delivered to User B instantly

Message saved in database

7. Message Flow (Offline User)
User A → WebSocket Server → Message Queue → Database
                               ↓
                        User B comes online
                               ↓
                        Fetch undelivered messages
8. Database Design
Messages Table
Field	Type
message_id	bigint
sender_id	bigint
receiver_id	bigint
content	text
timestamp	datetime
status	sent/delivered/read
Index:

(sender_id, receiver_id)

timestamp

Users Table
Field	Type
user_id	bigint
name	varchar
last_seen	datetime
status	online/offline
9. Caching (Redis)
Cache:

User online status

Recent messages

Keys:

user:123:status → online
chat:123:456 → last 50 messages
10. Sharding Strategy
Shard by:

hash(user_id) % N
Why?

All messages for a user go to same shard

Easy retrieval

Even distribution

11. Message Queue (Kafka / RabbitMQ)
Why queue?

Decouple sending and storing

Handle traffic spikes

Retry failed messages

Used for:

Message delivery

Notifications

Fan-out

12. Reliability & Delivery Guarantees
Use:

Message acknowledgements

Retry mechanism

Idempotent message IDs

Guarantee:

At least once delivery

13. Security
HTTPS / WSS

JWT authentication

End-to-end encryption (conceptually)

Rate limiting (prevent spam)

14. Fault Tolerance
Multiple WebSocket servers

Load balancer health checks

Database replication

Redis cluster

Message queue replication

15. Bottlenecks & Solutions
Problem	        Solution
High latency	WebSockets
DB overload	    Redis cache
Message loss	Message queue
Hot users	    Sharding
Spam        	Rate limiting

16. Scaling the System
Scale by:

Adding more WebSocket servers

Partitioning message queue

Sharding database

Using CDN for media

17. Interview Questions
Why WebSockets instead of HTTP?

How do you deliver messages when user is offline?

How do you scale to millions of users?

How do you ensure message is not lost?

What database will you use and why?

How do you handle retries?

18. Key Interview One-Liners
“We use WebSockets for real-time bidirectional communication.”

“Messages are pushed to a queue for reliable delivery.”

“Redis caches online status and recent messages.”

“Database is sharded by user_id.”

“System is horizontally scalable.”

19. Summary
WebSockets for real-time messaging

Message queue for reliability

Cache for performance

Sharded DB for scalability

Load balancer for availability