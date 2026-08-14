# Day 29 - DevOps & Cloud Computing Fundamentals
*Thu, 6 Aug 2026*

## What Is DevOps?

**DevOps = Development + Operations**

Connects developers and IT operations to build, test, deploy, and monitor software faster.

### The DevOps Flow

```
Developer
    │
    ▼
  Write Code
    │
    ▼
   Git
    │
    ▼
Build & Test
    │
    ▼
CI/CD Pipeline
    │
    ▼
Docker / Kubernetes
    │
    ▼
   Cloud (AWS)
    │
    ▼
Deploy Application
    │
    ▼
Monitor & Maintain
```

DevOps helps build, test, and deploy applications automatically — but where do these applications and their infrastructure actually run? That's where **Cloud Computing** comes in.

---
## Cloud Computing

### What Is It?

Using computing resources — servers, storage, databases, and networking — **over the internet**, instead of purchasing and maintaining physical infrastructure yourself.

> Example: An e-commerce company can use cloud services to host its application and database instead of buying physical servers.

### How Cloud and DevOps Connect

```
Developer → Git → Jenkins/CI → Build & Test → Docker → Cloud → Kubernetes/ECS → Application
```

### Key Characteristics

**1. On-Demand Access** — resources can be created whenever required.
> The dev team needs a new server for testing — they create a cloud server within minutes.

**2. Scalability** — resources scale up or down based on traffic.
> Normal traffic → 2 servers. Festival sale traffic (1 lakh users) → 10 servers. After the sale → back to 2 servers.

**3. Pay-As-You-Go** — you pay for what you actually use, not for owning hardware.
> Using a cloud server for only 10 hours means paying for 10 hours of usage — similar to an electricity bill.

**4. Accessibility** — cloud resources are reachable from anywhere via the internet, with proper authorization.
> Developers in Pune, Bangalore, and Hyderabad can all access the same cloud application.

**5. Managed Infrastructure** — the cloud provider manages physical servers, data centers, networking hardware, power, and cooling, so the company can focus on the application itself.

### Everyday Examples of Cloud Computing

| Example | What It Demonstrates |
|---|---|
| Google Drive / iCloud | Storing files online instead of only locally |
| Microsoft 365 | Using Word/Excel/Teams via the cloud, no server management |
| Netflix | Videos hosted and delivered via cloud infrastructure to millions |
| Online Shopping | Scaling cloud servers up for sales, down afterward |
| Company Applications | Hosting Java/Spring Boot apps, databases, APIs on AWS/Azure/GCP |

---
## Core Compute Resources

Compute resources are what's needed to **process data and run applications**. There are 3 common ways to run applications in the cloud:

### 1. Virtual Machines (VMs)

A virtual computer running on a physical server, with its own OS, CPU, memory, and storage.
> Example: Deploying a Spring Boot app on an AWS EC2 virtual machine.

### 2. Containers

Package an application along with its code, libraries, and dependencies — runs consistently across environments.
> Example: Packaging a Spring Boot app into a Docker container.

### 3. Serverless

Run code without managing servers at all — the cloud provider handles the infrastructure, typically charging based on execution.
> Example: An AWS Lambda function triggered when a file is uploaded to cloud storage.

### Comparison

| Compute Type | You Manage | Example |
|---|---|---|
| **VM** | OS + Application | AWS EC2 |
| **Container** | Application + Dependencies | Docker |
| **Serverless** | Mainly Code | AWS Lambda |

---
## Cloud Deployment Models

Define how cloud resources and services are deployed, owned, and accessed.

### 1. Public Cloud
- Owned by cloud providers (AWS, Azure, GCP)
- Resources shared among multiple customers
- Pay-as-you-go pricing
- **Example:** AWS, Azure, Google Cloud

### 2. Private Cloud
- Used by a single organization
- High security and control
- Dedicated infrastructure
- **Example:** A bank or government data center

### 3. Hybrid Cloud
- Combination of Public and Private Cloud
- Sensitive data stays in Private Cloud, remaining applications run in Public Cloud
- **Example:** Company Data Center + AWS

### 4. Multi-Cloud
- Uses multiple cloud providers
- Avoids dependency on a single vendor, improves flexibility and availability
- **Example:** AWS + Azure

---
## Vendor Lock-In

Becoming dependent on one cloud provider's services, making it difficult to move to another provider.

> Example: Using only AWS services — EC2, Lambda, DynamoDB, S3 — makes migrating to Azure later require significant changes.

**Multi-Cloud** helps reduce Vendor Lock-In by using services from multiple providers.

---
## Introduction to AWS

**AWS (Amazon Web Services)** is a cloud computing platform providing services for computing, storage, databases, networking, security, analytics, and more.

### Major Categories

```
                         AWS
                          |
      -------------------------------------------
      |          |          |          |         |
   Compute    Storage    Database   Network   Security
```
