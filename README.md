# Eureka Discovery Server – README
# Overview

This repository contains a Spring Cloud Netflix Eureka Server, which acts as the Service Discovery component in a microservices architecture.

It enables:

Automatic service registration

Load-balanced routing via API Gateway

Real-time health status tracking of microservices

Dynamic scaling (add/remove nodes without config changes)

This Discovery Server is part of a larger system that includes:

Order Service

Payment Service

API Gateway

MySQL Databases

# Architecture Context
Client → API Gateway → Eureka Discovery → Microservices → Databases


# Eureka Server Responsibilities

Maintain registry of all active microservices

Provide service lookup for API Gateway and other clients

Support load balancing & fault tolerance

# Features

✔ Centralized service registry
✔ Real-time heartbeat monitoring
✔ Auto-registration of microservices
✔ Web dashboard for visualization
✔ No hardcoded URLs — dynamic resolution

# Tech Stack
Technology	Purpose
Spring Boot	Core framework
Spring Cloud Netflix Eureka	Service Discovery
Java 17+	Runtime
Maven	Build tool

# Project Structure
eureka-server/
 ├── src/main/java/com/example/eurekaserver/
 │       └── EurekaServerApplication.java
 ├── src/main/resources/
 │       └── application.yml
 ├── pom.xml
 └── README.md

# Configuration
application.yml
server:
  port: 8761

eureka:
  client:
    register-with-eureka: false
    fetch-registry: false
  instance:
    hostname: localhost

# How to Run the Eureka Server
Prerequisites

Java 17+

Maven installed

IntelliJ / VS Code optional

Run using Maven
mvn spring-boot:run

Run using your IDE

➡ Open EurekaServerApplication.java
➡ Run as Java Application

# Access the Eureka Dashboard

Once started, open:

👉 http://localhost:8761

Expected dashboard view:

Registered Applications

Status of microservices

Health check indicators

# Registering Microservices

Each service needs the following in application.yml:

eureka:
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka/


And add dependency in pom.xml:

<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
</dependency>

# Verification Steps

Start Eureka Server

Start Order Service

Start Payment Service

Start API Gateway

Visit http://localhost:8761

You should see:

ORDER-SERVICE (UP)

PAYMENT-SERVICE (UP)

API-GATEWAY (UP)

# Troubleshooting
 Service not showing in Eureka

Check defaultZone URL

Ensure port 8761 is not blocked

Verify each microservice has:

spring.application.name=<service-name>

# "Unknown dependency: spring-cloud-starter-netflix-eureka-server"

Add Spring Cloud BOM in dependencyManagement:

<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-dependencies</artifactId>
            <version>2022.0.4</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>

# "Class file has wrong version"

Use Java 17 or later.

# Future Enhancements

Integrate with Spring Cloud Config Server

Enable security with OAuth2/JWT

Add service health monitoring (Actuator + Prometheus)
