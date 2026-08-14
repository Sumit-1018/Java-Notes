# Day 31 - ECS, EKS, Serverless & Key AWS Resources
*Mon, 10 Aug 2026 (Week 7)*

## AWS Container Services: ECS & EKS

AWS provides two main services for running and managing containers — both help deploy, manage, monitor, and scale Docker containers.

## ECS (Elastic Container Service)

**AWS-native container orchestration service** — simpler and easier to manage, no Kubernetes knowledge required.

**When to Use:** Small to medium projects, AWS-only environments, teams new to containers, faster setup.

**Benefits:** Easy to learn, easy deployment, auto scaling, AWS managed.

```
Spring Boot Application
        ↓
Docker Container
        ↓
ECS
        ↓
EC2 / Fargate
```

### ECS Architecture

```
                +-----------+
                |  Users    |
                +-----------+
                      |
                      v
                +-----------+
                |    ALB    |  // Application Load Balancer
                +-----------+
                      |
                      v
                +----------------------+
                | Ingress Controller   |  // manages all service traffic — like ECS/EKS
                +----------------------+
                      |
                      v
                +-----------+
                | Service   |  // ECS/EKS managing pods
                +-----------+
                      |
             ------------------
             |                |
             v                v
          +------+        +------+
          | Pod1 |        | Pod2 |  // Pods, each holding one or more containers
          +------+        +------+
              ^
              |
      +----------------+
      | Docker Hub     |  // images — from Docker Hub or your own Java app image
      | nginx:latest   |
      +----------------+
```

---
## EKS (Elastic Kubernetes Service)

**AWS-managed Kubernetes service** — uses industry-standard Kubernetes, suitable for large-scale deployments.

**When to Use:** Organization already uses Kubernetes, multi-cloud strategy, large enterprise applications, advanced container management.

**Benefits:** Kubernetes standard, highly scalable, portable across clouds, advanced orchestration.

```
Docker Hub
      |
      v
Docker Image
      |
      v
Kubernetes Pod
      |
      v
Running Container
      |
      v
employee-app.jar executes
```

### EKS Architecture

```
           +------------------+
           |      Users       |
           +------------------+
                    |
                    v
           +------------------+
           | Load Balancer    |
           +------------------+
                    |
                    v
           +------------------+
           | Ingress          |
           +------------------+
                    |
                    v
           +------------------+
           | Kubernetes       |
           | Service          |
           +------------------+
                    |
          -------------------
          |                 |
          v                 v
      +--------+      +--------+
      | Pod 1  |      | Pod 2  |
      +--------+      +--------+
          ^
          |
   +-------------+
   | Image Repo  |
   | (ECR)       |
   +-------------+
```

**Flow:** `Cluster → Node → Pods → Container`

### One-Line Component Descriptions

| Component | Role |
|---|---|
| **Users** | Access the application through a browser or API |
| **Load Balancer (ALB)** | Distributes incoming traffic to the Kubernetes cluster |
| **Ingress** | Traffic router that decides which service should handle a request |
| **Kubernetes Service** | Internal load balancer exposing Pods via a stable endpoint |
| **Pod** | Smallest deployable unit in Kubernetes, containing one or more containers |
| **Container** | Running instance of your application (Spring Boot, React, Nginx, etc.) |
| **ECR** | AWS repository that stores Docker images for deployment |

### ECS vs EKS

| ECS | EKS |
|---|---|
| AWS Native | Kubernetes Based |
| Easier to learn | More complex |
| Quick setup | Industry standard |
| Best for AWS-only projects | Best for enterprise Kubernetes environments |

---
## Serverless Computing on AWS

### What Is Serverless?

- Run code without managing servers
- AWS handles infrastructure and scaling
- Pay only when the code actually executes

### AWS Lambda

AWS's serverless service — executes code when an event occurs, with no EC2 management required.

```
User clicks "Calculate EMI"
          ↓
API Request
          ↓
Lambda Function
          ↓
EMI Calculated
          ↓
Result Returned
```

### Benefits

- No server management
- Auto scaling
- Pay per use
- Faster development

### EC2 vs ECS/EKS vs Lambda

| Service | What You Manage |
|---|---|
| **EC2** | Server, OS, Application deployment |
| **ECS/EKS** | Containers — AWS helps manage the infrastructure |
| **Lambda** | Just your function code — AWS manages everything else |

---
## Key AWS Resources

### Compute — "Run Code"

Used to run applications and workloads.
**Examples:** EC2 (VMs), ECS (Containers), EKS (Kubernetes), Lambda (Serverless)

### Storage — "Save Data"

Used to store files and data.
**Examples:** S3 (Object Storage), EBS (Disk Storage for EC2), EFS (Shared File Storage)

### Databases — Store Application Data

**Examples:** RDS (SQL Database), DynamoDB (NoSQL Database)

### Networking — "Connect Resources"

Used to connect and secure resources.
**Examples:** VPC, Subnets, Route 53, Security Groups

**VPC (Virtual Private Cloud):** your own isolated network inside AWS.

**Subnet:** a smaller network inside your VPC — used because you don't want everything accessible from the internet.

```
                 🏢 Company Office
                    (VPC)
                       |
        ┌──────────────┴──────────────┐
        |                             |
   👨‍💼 Public Area                🔒 Private Area
   (Public Subnet)              (Private Subnet)
        |                             |
   Web Servers                    Database
   Load Balancer                 MySQL
```

```
🏢 VPC (Company Building)
│
├── 🚪 Public Subnet
│     Web Server
│     Load Balancer
│
└── 🔐 Private Subnet
      Database
      Backend Server
```

### Quick Summary

| Service | What It Is |
|---|---|
| **EC2** | Virtual Machine |
| **S3** | File Storage |
| **RDS** | SQL Database |
| **DynamoDB** | NoSQL Database |
