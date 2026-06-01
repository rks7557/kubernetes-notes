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


# Kubeadm in Kubernetes

kubeadm is an official Kubernetes tool used to bootstrap (create and configure) Kubernetes clusters quickly and consistently.

ex :- kubeadm = Kubernetes Cluster Setup Tool

It automates the installation and configuration of Kubernetes control plane components.

Why kubeadm?

Before kubeadm, setting up a cluster required manually configuring:

API Server
Scheduler
Controller Manager
etcd
Certificates
Networking

This was time-consuming and error-prone.

kubeadm automates these tasks.


What kubeadm Does ?

when we run command "kubeadm init", it will generate the following things:-

✅ Generates certificates

✅ Creates kubeconfig files

✅ Starts control plane components

✅ Configures etcd

✅ Creates static pod manifests

✅ Generates join token

✅ Prepares cluster for worker nodes


What kubeadm Does NOT Do :-

❌ Install container runtime

❌ Install kubelet

❌ Install kubectl

❌ Install CNI plugin

❌ Manage applications

❌ Upgrade OS

We need to install these separately.

* Kubernetes Components Required Before kubeadm

Container runtime -> Containerd -> kubelet -> kubectl -> kubeadm

We can verify like :-

kubeadm version
kubectl version --client
kubelet --version

# Kubeadm architecture

                kubeadm init
                       |
                       |
     ---------------------------------
     |               |              |
 API Server      Scheduler      Controller
     |
     |
   etcd

Worker nodes join using:
kubeadm join


Important kubeadm Commands
1. Initialize Control Plane
sudo kubeadm init

Creates:

Control Plane Node
API Server
Scheduler
Controller Manager
etcd
Certificates
2. Initialize with Pod Network CIDR

Example:

sudo kubeadm init --pod-network-cidr=192.168.0.0/16

Common for:

Calico
Flannel
3. Setup kubectl Access

After successful init:

mkdir -p $HOME/.kube

sudo cp -i /etc/kubernetes/admin.conf \
$HOME/.kube/config

sudo chown $(id -u):$(id -g) \
$HOME/.kube/config

Verify:

kubectl get nodes
4. Join Worker Node

Generated automatically:

kubeadm join 10.0.0.10:6443 \
--token abcdef.1234567890abcdef \
--discovery-token-ca-cert-hash sha256:xxxx

Worker node contacts API server and joins cluster.

5. Generate New Join Token

If token expires:

kubeadm token create
6. Print Join Command
kubeadm token create --print-join-command

Example:

kubeadm join 192.168.1.10:6443 \
--token xxxxx \
--discovery-token-ca-cert-hash sha256:xxxxx
7. Check Existing Tokens
kubeadm token list

Output:

TOKEN                     TTL
abcdef.1234567890abcd     23h
8. Reset Cluster

Removes cluster configuration.

sudo kubeadm reset

Used when rebuilding cluster.

kubeadm Cluster Initialization Workflow
kubeadm init
     |
     |
Generate Certificates
     |
Generate kubeconfig Files
     |
Create Static Pod Manifests
     |
Start etcd
     |
Start API Server
     |
Start Controller Manager
     |
Start Scheduler
     |
Generate Join Token
     |
Cluster Ready
Static Pods Created by kubeadm

After initialization:

ls /etc/kubernetes/manifests

Files:

etcd.yaml

kube-apiserver.yaml

kube-controller-manager.yaml

kube-scheduler.yaml

These are called Static Pods.

What Are Static Pods?

Managed directly by kubelet.

Location:

/etc/kubernetes/manifests/

Kubelet continuously watches this directory.

If file exists:

Manifest Exists
      ↓
Kubelet Creates Pod

If deleted:

Manifest Removed
      ↓
Pod Removed
Important kubeadm Files
admin.conf
/etc/kubernetes/admin.conf

Used by kubectl.

Contains:

Cluster endpoint
Certificates
Credentials
PKI Directory
/etc/kubernetes/pki/

Contains certificates.

Examples:

ca.crt
ca.key

apiserver.crt
apiserver.key
Manifests Directory
/etc/kubernetes/manifests/

Contains static pod definitions.

How kubeadm Creates Control Plane Components

Example:

cat /etc/kubernetes/manifests/kube-apiserver.yaml

You will see:

kind: Pod

metadata:
  name: kube-apiserver

Kubelet reads it and starts API Server container.

HA (High Availability) with kubeadm

kubeadm supports:

1 Load Balancer
3 Control Plane Nodes
Multiple Worker Nodes

Architecture:

            Load Balancer
                   |
        ---------------------
        |         |         |
        v         v         v
      CP1       CP2       CP3
        |
        |
   Worker Nodes

Benefits:

No single point of failure
Better availability
Upgrading Kubernetes with kubeadm

Check plan:

kubeadm upgrade plan

Upgrade:

kubeadm upgrade apply v1.xx.x

Upgrade kubelet:

apt install kubelet
systemctl restart kubelet

Verify:

kubectl get nodes
Troubleshooting kubeadm
Check Cluster Info
kubectl cluster-info
Check Nodes
kubectl get nodes
Check Static Pods
kubectl get pods -n kube-system
Check kubelet Logs
journalctl -u kubelet -f
Check Container Runtime
systemctl status containerd
Check Certificates
kubeadm certs check-expiration
Real-World kubeadm Deployment Flow
Install Ubuntu
      ↓
Install Containerd
      ↓
Install kubeadm
      ↓
Install kubelet
      ↓
Install kubectl
      ↓
Disable Swap
      ↓
kubeadm init
      ↓
Configure kubectl
      ↓
Install CNI (Calico)
      ↓
Worker Nodes Join
      ↓
Deploy Applications


# Kind Cluster

KIND (Kubernetes IN Docker) is a tool that runs a complete Kubernetes cluster inside Docker containers.

KIND is mainly used for:

Learning Kubernetes
Development
Testing
CI/CD Pipelines
Certification Practice (CKA, CKAD)

Why KIND?

Normally, to create a Kubernetes cluster you need:

Control Plane VM
Worker Node VM
Networking
Storage

This requires significant resources.

With KIND:

Laptop->Docker->KIND->Kubernetes Cluster

No VMs required.

How KIND works ?

KIND works as a docker containers that works as a kubernetes nodes.

Docker host -> Control Plane -> Worker-1 -> Worker-2

Each node is actually a docker container.

# Kind architecture

Docker Engine -> KIND Node(Container) -> Kubernetes components

Inside the container:

kubelet
kubeadm
containerd
API Server
Scheduler
Controller Manager

# In my case i'm taking Amazon EC2 .

1. take t2.medium 
enable ssh/http/https
storage 30GB
OS -> UBUNTU

then launch instance.

Go to terminal :-

vi install_kind.sh

#!/bin/bash

[$(uname -m) = x86_64] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.20.0/kind-linux-amd64

chmod +x ./kind

sudo cp ./kind /usr/local/bin/bash

VERSION = "v1.30.0"

url = "https://dl.k8s.io/release/${VERSION}/bin/linux/amd64/kubectl"

INSTALL_DIR = "/usr/local/bin"

curl -Lo "$URL"

chmod +x kubectl

sudo mv kubectl $INSTALL_DIR/

kubectl version --client

rm -rf kubectl

rm -rf kind

echo "kind & kubectl installation complete."


# Install docker to run kind

sudo apt-get update

sudo apt-get install docker.io

sudo usermod -aG docker $USER && newgrp docker

docker ps

docker --version

kubectl version

kind version

