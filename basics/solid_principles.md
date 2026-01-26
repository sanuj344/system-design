# SOLID Principles (Clean Code & System Design Foundation)

SOLID principles are a set of 5 design principles that help us write:
- Clean code
- Maintainable code
- Scalable architecture
- Testable systems

They are the foundation of:
- Object Oriented Design
- System Design
- Microservices
- Clean Architecture

SOLID =  
S → Single Responsibility Principle  
O → Open/Closed Principle  
L → Liskov Substitution Principle  
I → Interface Segregation Principle  
D → Dependency Inversion Principle  

---

## 1. Single Responsibility Principle (SRP)

### Definition:
A class should have **only one reason to change**.

That means:
One class = one responsibility

---

### ❌ Bad Example (Multiple Responsibilities)

```js
class UserService {
  createUser(user) {
    // create user
  }

  sendEmail(user) {
    // send email
  }

  logToFile(user) {
    // log to file
  }
}


Problems:

User creation

Email sending

Logging
All in one class ❌

✅ Good Example (SRP Followed)
class UserService {
  createUser(user) {
    // create user
  }
}

class EmailService {
  sendEmail(user) {
    // send email
  }
}

class LoggerService {
  log(user) {
    // log
  }
}


Each class has one responsibility only.

Benefits of SRP:

Easy to maintain

Easy to test

Less bugs

Clean structure

2. Open/Closed Principle (OCP)
Definition:

Software entities should be:

Open for extension

Closed for modification

Meaning:
You should be able to add new functionality without changing existing code.

❌ Bad Example
function getDiscount(type) {
  if (type === "student") return 10;
  if (type === "senior") return 20;
}


If new type comes → modify function ❌

✅ Good Example (OCP)
class Discount {
  getDiscount() {}
}

class StudentDiscount extends Discount {
  getDiscount() {
    return 10;
  }
}

class SeniorDiscount extends Discount {
  getDiscount() {
    return 20;
  }
}


Now new discount = new class
No existing code touched ✅

Benefits of OCP:

Less risk of breaking code

Easy to extend

Good for large systems

3. Liskov Substitution Principle (LSP)
Definition:

Objects of a superclass should be replaceable with objects of a subclass
without breaking the application.

Child class should behave like parent class.

❌ Bad Example
class Bird {
  fly() {}
}

class Ostrich extends Bird {
  fly() {
    throw new Error("Cannot fly");
  }
}


Ostrich is Bird but cannot fly ❌
Breaks LSP.

✅ Good Example
class Bird {}

class FlyingBird extends Bird {
  fly() {}
}

class Ostrich extends Bird {
  walk() {}
}


Correct behavior separation ✅

Benefits of LSP:

Prevents unexpected bugs

Reliable inheritance

Strong polymorphism

4. Interface Segregation Principle (ISP)
Definition:

Clients should not be forced to depend on interfaces they do not use.

Meaning:
Do not create large interfaces.
Create smaller, specific interfaces.

❌ Bad Example
class Machine {
  print() {}
  scan() {}
  fax() {}
}


What if printer cannot fax? ❌

✅ Good Example
class Printer {
  print() {}
}

class Scanner {
  scan() {}
}

class Fax {
  fax() {}
}


Small focused interfaces ✅

Benefits of ISP:

Less coupling

Easier to implement

Flexible code

5. Dependency Inversion Principle (DIP)
Definition:

High-level modules should not depend on low-level modules.
Both should depend on abstractions.

❌ Bad Example
class MySQLDatabase {
  connect() {}
}

class UserService {
  constructor() {
    this.db = new MySQLDatabase();
  }
}


UserService depends directly on MySQL ❌

✅ Good Example
class Database {
  connect() {}
}

class MySQLDatabase extends Database {
  connect() {}
}

class UserService {
  constructor(database) {
    this.db = database;
  }
}


Now UserService depends on abstraction ✅

Benefits of DIP:

Loose coupling

Easy to replace components

Testable code

Flexible architecture

Why SOLID is Important in System Design

SOLID helps:

Build scalable systems

Change components easily

Avoid tight coupling

Write maintainable services

Used in:

Microservices

Clean Architecture

Layered Architecture

Backend APIs

Interview Questions on SOLID

What is SOLID?

Explain SRP with example.

Difference between OCP and SRP?

Why LSP is important?

What is dependency inversion?

Where have you used SOLID in projects?

Key Interview One-Liners

“SRP means one class should have one responsibility.”

“OCP allows extension without modification.”

“LSP ensures correct inheritance behavior.”

“ISP avoids fat interfaces.”

“DIP reduces tight coupling.”

Summary

SOLID principles:

Improve code quality

Enable scalability

Help system design

Make code easy to test and maintain