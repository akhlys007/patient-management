# 🏥 Patient Management System – Microservices-Based Healthcare Platform

> A production-ready, cloud-native Patient Management System built using Java Spring Boot, Docker, Kafka, gRPC, and AWS infrastructure tools. This project showcases my understanding of distributed systems, microservices, secure authentication, and scalable cloud deployments.

![Java](https://img.shields.io/badge/Java-SpringBoot-informational?style=flat&logo=java) ![Docker](https://img.shields.io/badge/Docker-Containerized-blue?style=flat&logo=docker) ![AWS](https://img.shields.io/badge/AWS-Cloud--Deployed-orange?style=flat&logo=amazonaws) ![Kafka](https://img.shields.io/badge/Kafka-Event--Driven-lightgrey?style=flat&logo=apachekafka)

---

## 📌 Project Overview

This Patient Management System is built using a **microservices architecture** where each service (Patient, Billing, Notification, Auth, Analytics) performs a single business function. It is designed to be modular, scalable, and fault-tolerant.

**Communication:**  
- gRPC → For internal service communication  
- Kafka → For asynchronous event-driven architecture  

**Deployment:**  
- AWS ECS (Elastic Container Service)  
- RDS for relational DBs  
- MSK for Kafka messaging  
- API Gateway for routing and authentication  
- Infrastructure as Code with AWS CloudFormation and LocalStack for testing

---

## 🎯 Project Goals

- Learn and implement Java microservices with best practices
- Showcase real-world usage of Spring Boot, Kafka, and gRPC
- Gain hands-on experience with Docker, CI/CD, and AWS deployment
- Solidify integration testing, JWT security, and API Gateway routing

---

## 📽️ Video Guide Source

This project follows [this YouTube tutorial](https://www.youtube.com/watch?v=tseqdcFfTUY) by Amigoscode:
> **"Build & Deploy a Production-Ready Patient Management System with Microservices: Java Spring Boot AWS"**

---

## 🛠️ Tech Stack

- **Backend Framework**: Spring Boot, Spring Web, Spring Security, Spring Data JPA  
- **Databases**: PostgreSQL, H2 (for in-memory testing)  
- **Messaging**: Apache Kafka  
- **RPC Communication**: gRPC, Protobuf  
- **Authentication**: JWT-based Security  
- **Infrastructure**: Docker, Docker Compose, AWS ECS, RDS, MSK, API Gateway, CloudFormation  
- **Testing**: Integration Tests, JUnit, Spring Boot Test  
- **Documentation**: OpenAPI / Swagger UI

---

## 🧩 System Architecture


![System Architecture](System%20Architecture.png)

### Micro-Services Spring Boot Architecture
![Micro-Services Spring Boot Architecture](Springboot%20Architecture.png)
---

## 🧪 Services & Features

### 🧍 Patient Service
- REST API for patient CRUD operations
- Validations with Hibernate Validator
- Kafka producer for event emission
- gRPC client for billing updates

### 💰 Billing Service
- gRPC server implementation
- Receives patient billing info from gRPC client
- Dockerized as a standalone microservice

### 🔔 Notification Service
- Kafka consumer setup
- Consumes patient event messages
- Sends out notifications (stubbed)

### 🔐 Auth Service
- JWT-based user authentication and authorization
- PostgreSQL-backed user repository
- Endpoints: `/login`, `/validate`, etc.
- API Gateway integration with token validation

### 📊 Analytics Service
- Kafka consumer to collect patient event data
- Metrics and logging functionality
- Dockerized and tested independently

---

## ⚙️ Environment Variables

### Patient Service

```env
JAVA_TOOL_OPTIONS=-agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=*:5005;
SPRING_DATASOURCE_PASSWORD=password
SPRING_DATASOURCE_URL=jdbc:postgresql://patient-service-db:5432/db
SPRING_DATASOURCE_USERNAME=admin_user
SPRING_JPA_HIBERNATE_DDL_AUTO=update
SPRING_KAFKA_BOOTSTRAP_SERVERS=kafka:9092
SPRING_SQL_INIT_MODE=always
BILLING_SERVICE_ADDRESS=billing-service
BILLING_SERVICE_GRPC_PORT=9005
```

### Billing Service

gRPC Maven Dependencies (add to `pom.xml`):
```xml
<!-- gRPC Dependencies -->
<dependency>...</dependency>
```

Build Section:
```xml
<build>
  ...
  <plugin>
    <artifactId>protobuf-maven-plugin</artifactId>
    ...
  </plugin>
</build>
```

### Kafka Broker (local setup in IntelliJ)
```env
KAFKA_CFG_ADVERTISED_LISTENERS=PLAINTEXT://kafka:9092,EXTERNAL://localhost:9094
...
```

### Notification Service
```env
SPRING_KAFKA_BOOTSTRAP_SERVERS=kafka:9092
```

### Auth Service
```env
SPRING_DATASOURCE_URL=jdbc:postgresql://auth-service-db:5432/db
SPRING_DATASOURCE_USERNAME=admin_user
SPRING_DATASOURCE_PASSWORD=password
SPRING_JPA_HIBERNATE_DDL_AUTO=update
SPRING_SQL_INIT_MODE=always
```

Auth Service User Setup (`data.sql`)
```sql
INSERT INTO "users" (id, email, password, role) ...
```

---

## 🧰 Project Setup (from YouTube Chapters)

| Chapter No. | Description                                |
|-------------|--------------------------------------------|
| 00–04       | Project setup and dev environment          |
| 05–15       | Patient model, controller, and validation  |
| 16–20       | Docker and PostgreSQL integration          |
| 21–29       | gRPC setup for Billing Service             |
| 30–36       | Kafka setup and Kafka Producer integration |
| 37–40       | Analytics Kafka Consumer                   |
| 41–43       | API Gateway introduction and routing       |
| 44–56       | Auth service with Spring Security & JWT    |
| 57–60       | Gateway JWT filtering                      |
| 61–66       | Integration Testing                        |
| 67–82       | AWS infrastructure and deployment setup    |

---

## 🧪 Local Development & Testing

### Pre-requisites
- Java 17+
- Docker & Docker Compose
- Maven
- IntelliJ IDEA or VS Code
- LocalStack (for AWS emulation)

### Run locally
```bash
docker-compose up --build
```

---

## 🚀 Deployment

AWS Services Used:
- **ECS**: For container orchestration
- **RDS**: PostgreSQL backend
- **MSK**: Kafka managed service
- **API Gateway**: Auth and routing
- **CloudFormation**: Infrastructure as code
- **CloudWatch**: Logging & Monitoring

Deploy with CloudFormation scripts included in `/infrastructure`.

---

## 📚 References

- [Original YouTube Tutorial](https://www.youtube.com/watch?v=tseqdcFfTUY) by Amigoscode
- Spring Boot Documentation
- Apache Kafka Docs
- AWS CloudFormation Templates

---

## 👤 Author

**Timothy Chelelgo**  
Aspiring Backend Engineer | Cloud Developer  
[GitHub](https://github.com/your-github-username) • [LinkedIn](https://linkedin.com/in/your-linkedin-profile)

---

## ✅ Roadmap

- [ ] Add CI/CD pipeline using GitHub Actions
- [ ] Implement full OAuth2 support
- [ ] Add more analytics endpoints
- [ ] Add frontend interface using React or Angular
- [ ] Deploy to production ECS cluster

---

## 🪪 License

This project is licensed under the MIT License — feel free to use and modify it for your learning or projects.
