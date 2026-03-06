# config-service

In Microservices architecture, a Config Service (Configuration Server) is used to manage configuration properties of all microservices in one central place.

A common implementation with Spring Boot is Spring Cloud Config.

1️⃣ Problem Without Config Service

Suppose you have 3 microservices:

User Service
Order Service
Payment Service

Each service has its own application.properties:

server.port=8081
db.url=jdbc:mysql://localhost:3306/userdb
db.username=root

Problems ❌

Config duplicated in many services

If DB password changes, you must update all services

Need to redeploy every service

Hard to manage dev / test / prod environments

2️⃣ Solution: Config Service

A Config Service stores all configuration in one central location (usually Git).

Example:

Git Repository

user-service.yml
order-service.yml
payment-service.yml

All microservices fetch configuration from the Config Server.

3️⃣ Architecture
                 Git Repository
                       |
                Config Server
                       |
        --------------------------------
        |              |               |
   User Service    Order Service    Payment Service
4️⃣ How It Works
Step 1

Config stored in Git

Example user-service.yml

server:
  port: 8081

spring:
  datasource:
    url: jdbc:mysql://localhost:3306/userdb
Step 2

Config Server reads configuration from Git.

Step 3

When User Service starts, it requests config:

http://config-server:8888/user-service/default
Step 4

Config server returns properties to the service.

Service starts with those values.

5️⃣ Main Uses of Config Service
1️⃣ Centralized Configuration

All configs stored in one place.

2️⃣ Environment Management

Example:

dev
qa
prod

Different configs for each environment.

3️⃣ Dynamic Config Updates

Using refresh, config can change without restarting services.

4️⃣ Security

Sensitive values stored securely.

Example:

DB password
API keys
6️⃣ Example Interview Answer

Question: What is Config Server?

Answer:

Config Server is a centralized configuration management system used in microservices to store and manage application properties externally. It allows multiple services to fetch configuration from a central location such as Git.

Example tool:

Spring Cloud Config

7️⃣ Service Registry vs Config Server
Feature	Service Registry	Config Server
Purpose	Service discovery	Centralized configuration
Example	Eureka	Spring Cloud Config
Stores	Service locations	Application properties
Used by	Microservices	Microservices