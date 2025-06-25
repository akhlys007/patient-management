# 🏥 Patient Management System – Microservices-Based Healthcare Platform

> A production-ready, cloud-native Patient Management System built using Java Spring Boot, Docker, Kafka, gRPC, and AWS infrastructure tools. This project showcases my understanding of distributed systems, microservices, secure authentication, and scalable cloud deployments.

![Java](https://img.shields.io/badge/Java-SpringBoot-informational?style=flat&logo=java)
![Docker](https://img.shields.io/badge/Docker-Containerized-blue?style=flat&logo=docker)
![AWS](https://img.shields.io/badge/AWS-Cloud--Deployed-orange?style=flat&logo=amazonaws)
![Kafka](https://img.shields.io/badge/Kafka-Event--Driven-lightgrey?style=flat&logo=apachekafka)

---

## 📌 Project Overview

This Patient Management System is built using a **microservices architecture**, where each service (Patient, Billing, Notification, Auth, Analytics) performs a single business function. It is designed to be modular, scalable, and fault-tolerant.

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

## 🏗️ Build Process Highlights

The system was built incrementally using IntelliJ IDEA and Docker, following a modular design with Spring Boot and cloud-native practices.

### 🔧 Patient Service
- Created `Patient` entity with JPA annotations, validation, and a PostgreSQL-backed repository.
- Built RESTful APIs with DTOs, error handling, and validation.
- Integrated gRPC client for communication with Billing Service.
- Produced Kafka messages on patient creation.
- Used H2 for local testing and PostgreSQL in Docker for production.
- Dockerized with a multi-stage build.
- Config files: [`/patient-service/Dockerfile`](./patient-service/Dockerfile), [`application.properties`](./patient-service/src/main/resources/application.properties)

### 💰 Billing Service
- Defined `billing_service.proto` and generated code using `protobuf-maven-plugin`.
- Implemented gRPC server handling `CreateBillingAccount` requests.
- Dockerized with HTTP and gRPC ports exposed.
- Config files: [`/billing-service/Dockerfile`](./billing-service/Dockerfile), [`pom.xml`](./billing-service/pom.xml)

### 📊 Analytics Service
- Subscribed to Kafka `patient-events` topic.
- Parsed protobuf messages and logged events for future metrics.
- Dockerized and configured with Kafka bootstrap servers.
- Files: [`/analytics-service/Dockerfile`](./analytics-service/Dockerfile), [`application.properties`](./analytics-service/src/main/resources/application.properties)

### 🔐 Auth Service
- Implemented login and token validation using JWT.
- Connected to PostgreSQL via Docker with seed data.
- Password encoding with Spring Security.
- Exposed endpoints: `/auth/login`, `/auth/validate`
- Dockerized and connected via API Gateway.
- Files: [`/auth-service/Dockerfile`](./auth-service/Dockerfile), [`application.yml`](./auth-service/src/main/resources/application.yml)

### 🌐 API Gateway
- Spring Cloud Gateway routes traffic to underlying services.
- Added custom `JwtValidationGatewayFilterFactory` for secure JWT validation.
- Separated dev (`application.yml`) and production (`application-prod.yml`) configurations.
- Files: [`/api-gateway/application.yml`](./api-gateway/src/main/resources/application.yml), [`JwtValidationGatewayFilterFactory.java`](./api-gateway/src/main/java/com/gateway/JwtValidationGatewayFilterFactory.java)

### 🧪 Testing & Integration
- Created `integration-test` Maven module.
- Used RestAssured and JUnit to test both patient and auth endpoints.
- Verified unauthorized/authorized flows with API Gateway and JWT.

### ☁️ Infrastructure with LocalStack
- Created Java CDK project under `/infrastructure`.
- Defined CloudFormation stacks for:
  - VPC
  - RDS (PostgreSQL)
  - MSK (Kafka)
  - ECS cluster and services
  - Application Load Balancer and Gateway
- Deployed with AWS CLI pointing to LocalStack.
- Files: [`/infrastructure/LocalStack.java`](./infrastructure/src/main/java/com/pm/stack/LocalStack.java), [`localstack.template.json`](./infrastructure/templates/)

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
- **Testing**: Integration Tests, JUnit, RestAssured  
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
- Kafka producer for event emission  
- gRPC client for billing updates  

### 💰 Billing Service
- gRPC server receiving billing info  
- Communicates with patient service post-creation  

### 🔔 Notification Service
- Kafka consumer for patient events  
- Sends notifications (stubbed for now)  

### 🔐 Auth Service
- Handles login, validation, and JWT generation  
- Integrated with API Gateway for route protection  

### 📊 Analytics Service
- Kafka consumer for analytical event logging  

---

## ⚙️ Environment Variables

Each service has its own `.env` or `application.yml` file. Example for Patient Service:

```env
SPRING_DATASOURCE_URL=jdbc:postgresql://patient-service-db:5432/db
SPRING_DATASOURCE_USERNAME=admin_user
SPRING_DATASOURCE_PASSWORD=password
SPRING_KAFKA_BOOTSTRAP_SERVERS=kafka:9092
SPRING_JPA_HIBERNATE_DDL_AUTO=update
SPRING_SQL_INIT_MODE=always
````
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

- [Original YouTube Tutorial](https://www.youtube.com/watch?v=tseqdcFfTUY) by Chris Blakely
- Spring Boot Documentation
- Apache Kafka Docs
- AWS CloudFormation Templates

---

## 👤 Author

**Timothy Chelelgo**  
Aspiring FullStack Engineer | Cloud DevOps Engineer  
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
