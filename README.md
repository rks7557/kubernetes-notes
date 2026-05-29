# Kubernetes Introduction

Kubernetes (also called K8s) is an open-source container orchestration platform developed by Google and now maintained by the Cloud Native Computing Foundation (CNCF).

It is used to automate the deployment, scaling, management, networking, and monitoring of containerized applications.

Kubernetes helps organizations run applications reliably across multiple servers by automatically handling tasks such as:

Container deployment
Load balancing
Auto scaling
Self-healing
Storage management
Rolling updates and rollbacks

Kubernetes mainly works with containers created using Docker or other container runtimes.

# Why Kubernetes

Before Kubernetes, managing containers manually on multiple servers was difficult because:

Containers could crash
Traffic distribution was hard
Scaling applications required manual work
Monitoring and recovery were time-consuming

Kubernetes solves these problems by automating the entire container management process.

# Real-World Example

Imagine a company like Netflix or Amazon:

1. Thousands of users access the application every second.
2. Multiple application containers run on many servers.
3. If one server fails, the application should still work.
4. During high traffic, more containers should automatically start.

Kubernetes manages all of this automatically.

# Key Features of Kubernetes

1. Container Orchestration – Manages multiple containers automatically
2. Auto Scaling – Increases or decreases containers based on traffic
3. Self-Healing – Restarts failed containers automatically
4. Load Balancing – Distributes traffic among containers
5. Rolling Updates – Updates applications without downtime
6. Service Discovery – Helps containers communicate easily
7. Storage Orchestration – Manages persistent storage volumes.

# Difference between Monolith and Microservices

1. Monolith

In a Monolithic Architecture, the entire application is built as a single unit.
All modules like authentication, payment, database access, notifications, and UI are tightly connected.

* Traditional E-Commerce Website

Example modules:

Login
Product Catalog
Cart
Payment
Order Management

Everything runs inside one application.

If one small feature crashes, the entire application can be affected.

# Microservices Architecture Examples

In Microservices Architecture, the application is divided into multiple small independent services.

Each service:

Has its own responsibility
Can be deployed independently
Can use separate databases
Communicates using APIs


1. Example Netflix

Netflix uses microservices for:

User Service
Recommendation Service
Payment Service
Streaming Service
Notification Service

If recommendation service fails, video streaming still works.

# Kubernetes Architecture :-

A Kubernetes Cluster consists of:

Control Plane (Master Node)
Worker Nodes

