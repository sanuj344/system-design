# Network Protocols
A network protocol is simply a set of rules that decide:
1.how data is sent
2.how it is received
3.how errors are handled

## HTTP vs HTTPS
HTTP / HTTPS
Used for:
Web apps
REST APIs
Frontend ↔ Backend communication

Feature 	HTTP	      HTTPS
Encryption	❌ No	    ✅ Yes
Security	❌ Insecure	✅ Secure
Port	     80	           443

“HTTPS encrypts data using TLS to prevent man-in-the-middle attacks and ensure secure communication.”

“HTTP is stateless, so authentication is maintained using tokens like JWT or session cookies.

## TCP vs UDP
TCP (Transmission Control Protocol)
TCP guarantees:
Data arrives completely
Data arrives in order
Retransmission if packet lost

Used by:
HTTP/HTTPS
Database connections


UDP (User Datagram Protocol)
UDP:
No guarantee of delivery
Very fast
No retransmission

Used by:
Video streaming
Voice calls
Online gaming

💡 If one frame drops → no issue

## WebSockets
Problem with HTTP:

Client must keep asking server

WebSocket:
Persistent connection
Server can push data

Used in:
WhatsApp chat
Live notifications
Stock prices

## Request Lifecycle
What Happens When You Type a URL?
https://instagram.com

Step 1: DNS Resolution

Browser asks DNS: “What is IP of instagram.com?”
DNS returns something like:
157.240.xxx.xxx

Step 2: TCP Connection

Browser establishes TCP connection with server IP
3-way handshake:
SYN
SYN-ACK
ACK

Step 3: HTTPS Handshake (TLS)

Encryption keys exchanged
Secure channel established

Step 4: HTTP Request Sent

GET / HTTP/1.1
Host: instagram.com

Step 5: Request Hits Load Balancer

LB decides which backend server handles request

Step 6: Backend Server

Authentication
Business logic
DB / Cache calls

Step 7: Response Sent Back

{
  "status": "ok",
  "data": "homepage"
}
