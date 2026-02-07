# Real-Time Transaction Monitoring System

A cloud-ready, event-driven microservices system built using **Spring Boot**, **Apache Kafka**, and **Docker**, designed with **OWASP Top 10 security principles**, modern **CI/CD**, and **enterprise-grade architecture**.

This project simulates real-time transaction ingestion, stream processing, and alert generation — similar to financial transaction monitoring systems.

---

## 🧩 High-Level Overview

### What this system does
1. Accepts transaction events via REST APIs
2. Publishes events to Kafka
3. Processes transactions in real time using stream processing concepts
4. Detects suspicious activity
5. Generates alerts
6. Exposes APIs to query alerts

---

## 🏗️ Architecture Overview

```text
Client / API Consumer
        |
        | POST /transactions
        v
+----------------------------+
| Transaction Producer       |
| Spring Boot REST API       |
| - Validation               |
| - Secure logging           |
+-------------+--------------+
              |
              | Kafka Event
              v
        +-------------+
        | Kafka Topic |
        | transactions|
        +------+------+ 
               |
               | Consume + Process
               v
+----------------------------+
| Transaction Processor      |
| Kafka Consumer / Streams   |
| - Stateful processing      |
| - Fraud rules              |
+-------------+--------------+
              |
              | Alert Event
              v
        +-------------+
        | Kafka Topic |
        | alerts      |
        +------+------+ 
               |
               | Consume
               v
+----------------------------+
| Alert Service               |
| Spring Boot REST API        |
| - Persist alerts            |
| - Secure endpoints          |
+-------------+--------------+
              |
              v
        +-------------+
        | Database    |
        | (H2 / RDS)  |
        +-------------+
```
## Sequence Diagram

```

Client
  |
  | POST /transactions
  v
Transaction Producer
  |
  | publish event
  v
Kafka (transactions topic)
  |
  | consume
  v
Transaction Processor
  |
  | apply rules
  | generate alert
  v
Kafka (alerts topic)
  |
  | consume
  v
Alert Service
  |
  | store alert
  v
Database

Client
  |
  | GET /alerts
  v
Alert Service
```


⸻

## 🧱 Services Breakdown
```
1️⃣ Transaction Producer
	•	REST API to accept transactions
	•	Validates payloads
	•	Publishes events to Kafka

Tech
	•	Spring Boot
	•	Spring Web
	•	Validation
	•	Kafka Producer

⸻

2️⃣ Transaction Processor
	•	Consumes transactions
	•	Applies stateful stream processing logic
	•	Generates alerts for suspicious activity

Tech
	•	Spring Boot
	•	Kafka Consumer / Streams
	•	Strategy Pattern for fraud rules

⸻

3️⃣ Alert Service
	•	Consumes alert events
	•	Persists alerts
	•	Exposes secure REST APIs

Tech
	•	Spring Boot
	•	Spring Data JPA
	•	H2 (local)
	•	Spring Security
```

## 🧪 Testing Strategy
```
	•	Unit tests for business logic
	•	Service-level tests for APIs
	•	Integration tests using Kafka
	•	Manual API testing via Postman
```

## ⚙️ Local Development Setup
```
Prerequisites
	•	Java 17 or 21
	•	Maven 3.9+
	•	Docker & Docker Compose

⸻
```
