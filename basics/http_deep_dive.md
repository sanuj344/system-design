# HTTP Deep Dive (From Basics to Interview Level)

HTTP (HyperText Transfer Protocol) is the foundation of communication
between clients (browser/mobile apps) and servers in modern web systems.

Every system design problem — WhatsApp, Uber, Netflix, URL Shortener —
starts and ends with HTTP requests.

---

## 1. What is HTTP?

HTTP is an **application-layer protocol** used for transferring data
between a client and a server.

### Key Characteristics:
- Request–Response based
- Stateless
- Text-based
- Built on top of TCP
- Platform independent

### Example:
A browser sends a request:
GET /users/1 HTTP/1.1


The server sends a response:
HTTP/1.1 200 OK


---

## 2. HTTP Request Structure

An HTTP request has **three main parts**:

### 1️⃣ Request Line
POST /api/payments HTTP/1.1


Contains:
- HTTP Method (GET, POST, etc.)
- Request Path
- HTTP Version

---

### 2️⃣ Headers

Headers contain **metadata** about the request.

Example:
Host: api.example.com
Authorization: Bearer <JWT_TOKEN>
Content-Type: application/json
User-Agent: Chrome


Common headers:
- Authorization → authentication
- Content-Type → request body format
- Accept → expected response format
- Cookie → session info

---

### 3️⃣ Request Body

- Present in POST, PUT, PATCH
- Contains actual data
- Usually JSON

Example:
```json
{
  "amount": 500,
  "currency": "INR"
}


HTTP Response Structure

An HTTP response also has three parts:
1️⃣ Status Line
HTTP/1.1 201 Created


Contains:
HTTP Version
Status Code
Status Message

HTTP Methods (Very Important)

HTTP methods define what action the client wants to perform.

Common Methods:
Method	     Purpose	       Idempotent
GET	      Read data	                  Yes
POST	 Create resource         	No
PUT	    Replace resource	           Yes
PATCH	Partial update	            No
DELETE 	Delete resource	            Yes


Idempotency:

A request is idempotent if calling it multiple times
produces the same result.

Example:

GET /users/1 → always same user
POST /orders → creates new order each time ❌


HTTP Status Codes
Status codes tell the client what happened.

2xx – Success

200 OK → request successful
201 Created → resource created
204 No Content → success, no response body

4xx – Client Errors

400 Bad Request → invalid input
401 Unauthorized → not authenticated
403 Forbidden → authenticated but no permission
404 Not Found → resource not found
429 Too Many Requests → rate limited

5xx – Server Errors

500 Internal Server Error
502 Bad Gateway
503 Service Unavailable

1XX - Informational
3XX - Redirectional 

HTTP is Stateless 

HTTP is stateless, meaning:
Server does NOT remember previous requests
Each request is independent

Problem:
How does server know who the user is?

Solutions:
Cookies
Sessions
JWT Tokens

REST API Design Basics

REST stands for Representational State Transfer.

REST Principles:
Resource-based URLs
Stateless communication
Use HTTP methods correctly
Consistent naming

API Versioning

Why version APIs?

Prevent breaking existing clients
Allow backward compatibility