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
<<<<<<< HEAD
=======

Control Plane Components

The Control Plane manages the entire Kubernetes cluster.

1. API Server

The API Server is the entry point of Kubernetes.

Responsibilities:

Receives kubectl commands
Validates requests
Communicates with ETCD
Exposes Kubernetes APIs

Example:

kubectl get pods
kubectl create deployment nginx --image=nginx

All requests first reach the API Server.

2. ETCD

ETCD is a distributed key-value database.

Responsibilities:

Stores cluster state
Stores configurations
Stores secrets
Stores node and pod information

Example:

Pod Information
Deployment Configuration
Service Details
Cluster Metadata

ETCD is the source of truth for Kubernetes.

3. Scheduler

The Scheduler decides where Pods should run.

Responsibilities:

Monitors pending Pods
Selects appropriate Worker Nodes
Considers CPU and memory requirements

Example:

Pod Created
      ↓
Scheduler Chooses Node
      ↓
Pod Assigned
4. Controller Manager

Maintains the desired state of the cluster.

Responsibilities:

Monitors cluster health
Replaces failed Pods
Maintains replica count
Handles node failures

Example:

Desired Pods = 3
Running Pods = 2
      ↓
Controller Creates New Pod
Worker Node Components

Worker Nodes run application workloads.

1. Kubelet

Kubelet is the node agent.

Responsibilities:

Communicates with API Server
Creates Pods
Monitors container health
Reports node status

Example:

API Server
      ↓
Kubelet
      ↓
Container Runtime
      ↓
Pods Created
2. Kube Proxy

Responsible for networking.

Responsibilities:

Maintains networking rules
Enables Pod communication
Implements Service networking
Handles load balancing

Example:

User Request
      ↓
Service
      ↓
Kube Proxy
      ↓
Pod
3. Container Runtime

Runs containers on the node.

Examples:

containerd
CRI-O
Docker (legacy support)

Responsibilities:

Pull container images
Start containers
Stop containers
Manage container lifecycle
Kubernetes Objects
Pod

Smallest deployable unit in Kubernetes.

Contains:

One or more containers
Shared network
Shared storage

Example:

Pod
 ├── Nginx Container
 └── Sidecar Container
Deployment

Manages Pods and ReplicaSets.

Features:

Rolling Updates
Rollbacks
Auto-healing
Scaling

Example:

replicas: 3

Maintains three Pod instances.

ReplicaSet

Ensures desired number of Pods are running.

Example:

Desired Pods = 3
Current Pods = 2
      ↓
Create 1 New Pod
Service

Provides stable network access to Pods.

Types:

ClusterIP
NodePort
LoadBalancer
ExternalName

Example:

Service
     ↓
Pod 1
Pod 2
Pod 3
Namespace

Provides logical separation within a cluster.

Examples:

default
kube-system
dev
test
production
ConfigMap

Stores non-sensitive configuration data.

Example:

DATABASE_HOST=db.example.com
LOG_LEVEL=INFO
Secret

Stores sensitive data.

Example:

Passwords
API Keys
Certificates
Tokens
>>>>>>> e660bf0 (Kubernetes architecture)

