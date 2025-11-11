# 🏥 Spring Boot Microservices Project – Patient Management System

## 📘 Overview

This project is a **microservices-based Patient Management System** built with **Spring Boot**, integrating **GRPC**, **Kafka**, **API Gateway**, **Docker**, and **AWS (LocalStack)**.
It follows a modular architecture where each service is responsible for a specific domain, communicating via GRPC and Kafka for event-driven processing.

This README summarizes the **full project flow** as implemented in the chapters.

---

## 🧱 Project Architecture

### Services Included:

| Service                             | Description                                                                      |
| ----------------------------------- | -------------------------------------------------------------------------------- |
| **Patient Service**                 | Manages patient records, CRUD operations, validations, and emits Kafka events.   |
| **Billing Service**                 | Handles billing logic and communicates via gRPC.                                 |
| **Analytics Service**               | Consumes Kafka events for analytics and reporting.                               |
| **Auth Service**                    | Manages user authentication, JWT generation, and token validation.               |
| **API Gateway**                     | Routes incoming requests to appropriate microservices and handles JWT filtering. |
| **Infrastructure (AWS/LocalStack)** | Automates deployment using AWS CloudFormation templates.                         |

---

## ⚙️ Development Setup

### 🧩 1. Dev Environment

* **Java 17+**
* **Spring Boot 3+**
* **Maven**
* **Docker / Docker Compose**
* **PostgreSQL**
* **Kafka + Zookeeper**
* **AWS CLI / LocalStack**

### 🧰 2. Tools Used

* **Postman / Insomnia** → for API testing
* **IntelliJ IDEA / Eclipse** → for development
* **pgAdmin** → to view database tables
* **Protobuf Compiler (protoc)** → for GRPC code generation

---

## 🚀 Project Setup & Structure

### 📁 Core Modules

```
/patient-service
/billing-service
/analytics-service
/auth-service
/api-gateway
/infrastructure
```

---

## 🧩 Step-by-Step Breakdown

### **00–04: Setup & Architecture**

* Intro, project structure, and environment setup.
* Created **Spring Boot multi-module** architecture.
* Setup **in-memory DB (H2)** for early development and testing.

### **05–15: Patient Service**

* Implemented **Repository, Service, and Controller layers**.
* Added **DTOs, validation handlers, and custom exceptions**.
* Built full CRUD: create, update (with email validation), delete, and get.
* Added **OpenAPI (Swagger)** documentation.

### **17–20: Dockerization**

* Containerized Patient Service and connected to PostgreSQL via Docker Compose.
* Verified service connection and persistence.

### **21–29: Billing Service with GRPC**

* Introduced **gRPC communication** between Patient and Billing services.
* Defined `.proto` files and generated stubs.
* Implemented **gRPC server** (Billing) and **gRPC client** (Patient).
* Integrated **billing logic** inside patient creation.

### **30–40: Kafka & Analytics**

* Setup Kafka broker and topic definitions.
* Implemented **Kafka producer** in Patient Service.
* Created **Analytics Service** to consume and process Kafka messages.
* Dockerized Analytics Service and validated data flow.

### **41–43: API Gateway**

* Introduced **Spring Cloud Gateway**.
* Setup routing rules and Docker configuration.
* Tested routing to microservices and unified API documentation.

### **44–61: Authentication Service**

* Created **Auth Service** with PostgreSQL.
* Implemented **JWT-based authentication**.
* Added **login, token validation, and password encryption (Spring Security)**.
* Integrated Auth Service with API Gateway for **JWT filtering and validation**.

### **62–66: Integration Testing**

* Added **JUnit and Spring Boot Test** dependencies.
* Wrote integration tests for login, patient retrieval, and authorization flows.

### **67–83: AWS Infrastructure & Deployment**

* Introduced **Infrastructure as Code (IaC)** using **AWS CloudFormation**.
* Setup **LocalStack** for local AWS simulation.
* Created VPC, RDS, MSK (Kafka), ECS cluster, and load balancer stacks.
* Built and deployed Docker images to simulated AWS environment.
* Tested and troubleshooted final deployment.

---

## 🧪 How to Run Locally

### 1️⃣ Clone Repository

```bash
git clone https://github.com/your-username/patient-microservices.git
cd patient-microservices
```

### 2️⃣ Build All Modules

```bash
mvn clean install -DskipTests
```

### 3️⃣ Start Docker Containers

```bash
docker-compose up -d
```

### 4️⃣ Access Services

| Service           | URL                                                                            |
| ----------------- | ------------------------------------------------------------------------------ |
| API Gateway       | [http://localhost:8080](http://localhost:8080)                                 |
| Patient Service   | [http://localhost:8081](http://localhost:8081)                                 |
| Billing Service   | [http://localhost:8082](http://localhost:8082)                                 |
| Analytics Service | [http://localhost:8083](http://localhost:8083)                                 |
| Auth Service      | [http://localhost:8084](http://localhost:8084)                                 |
| Swagger Docs      | [http://localhost:8080/swagger-ui.html](http://localhost:8080/swagger-ui.html) |

---

## 🔐 Authentication Flow

1. User sends login request to **Auth Service**.
2. JWT token is returned and must be attached to headers for every request.
3. **API Gateway** verifies token via Auth Service before routing.

---

## 🧬 Communication Summary

| Type  | Between                | Technology           |
| ----- | ---------------------- | -------------------- |
| REST  | Gateway ↔ All Services | Spring Cloud Gateway |
| GRPC  | Patient ↔ Billing      | Protobuf / gRPC      |
| Kafka | Patient → Analytics    | Event Streaming      |
| JWT   | Gateway ↔ Auth         | Spring Security      |

---

## 🧰 Infrastructure & Deployment

* Infrastructure is defined in `/infrastructure` using **CloudFormation templates**.
* **LocalStack** emulates AWS locally.
* Deploy all stacks using:

```bash
aws cloudformation deploy --template-file template.yaml --stack-name patient-system
```

---

## 🧾 Testing

* Integration tests for Auth and Patient services (`/test` packages).
* Use `mvn test` to run all tests.
* Logs available via Docker dashboard or:

```bash
docker logs patient-service
```

---

## 🧠 Key Learnings

* Microservices architecture and communication patterns
* gRPC integration in Spring Boot
* Kafka event streaming
* Docker container orchestration
* API Gateway with JWT authentication
* Infrastructure as Code (IaC) and AWS deployment

---

## 🏁 Conclusion

This project demonstrates a **complete enterprise-grade microservice ecosystem** using modern Spring technologies and cloud-ready tools.
It covers **development, communication, testing, deployment, and automation** — a full DevOps cycle for real-world systems.

---

## 👩‍💻 Author

**Sara EL AMRANI**
🎓 Software Engineering Student
💼 Spring Boot | Microservices | Docker | AWS | Cloud Computing
