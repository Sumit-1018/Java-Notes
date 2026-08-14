# Day 30 - Amazon EC2 & Docker Containers
*Fri, 7 Aug 2026*

## Amazon EC2 (Elastic Compute Cloud)

### What Is EC2?

A service that provides **virtual servers (Virtual Machines)** in the AWS cloud. Instead of buying physical servers, you create and use virtual servers on demand, paying only for what you use.

### Why EC2?

- Run applications in the cloud
- Create Linux or Windows servers
- Scale up or down as needed
- Pay-as-you-go pricing
- Avoid managing physical hardware

### EC2 Instance

An EC2 Instance **is** a Virtual Machine.

```
EC2 Instance
├── Operating System (Linux/Windows)
├── Java / Python / NodeJS
├── Application
└── Storage
```

With a direct EC2 deployment, **you are responsible for**:
- OS management
- Software installation
- Application deployment
- Security updates

### Real-World Example — Spring Boot on EC2

```
Spring Boot Application

EC2 Instance
├── Amazon Linux
├── Java 21
└── Spring Boot App

Users → Internet → EC2 Instance → Spring Boot Application
```

### Limitations of Direct EC2 Deployment

With a direct deployment, the team manages:
- Operating system
- Java/runtime installation
- Dependencies
- Patches
- Security
- Server configuration
- Application deployment
- Scaling
- Monitoring

This raises the question: **can we package the application and its dependencies together?** That's where **containers and Docker** come in.

---
## Containers and Docker

### Container

A lightweight package containing an application and **all its dependencies**.

- Runs consistently across different environments
- Shares the host operating system's kernel
- Faster and smaller than Virtual Machines

**Benefits:** Portable, fast startup, easy deployment, efficient resource usage.

### Docker

An **open-source platform** used to create, run, and manage containers.

- Packages applications into containers
- Ensures the application runs the same way on any system

**Key Components:**

| Component | Role |
|---|---|
| **Docker Image** | Template for a container |
| **Docker Container** | A running instance of an image |

### VM (EC2) vs Container

| Virtual Machine | Container |
|---|---|
| Includes a full OS | Shares the host OS |
| Larger size | Lightweight |
| More memory usage | Starts in seconds |

### Example — Spring Boot in a Container

```
Spring Boot Application

Docker Container
├── Java Runtime
├── Spring Boot App
└── Required Libraries
```

This container can run on: Local Machine, an EC2 Instance, ECS, or EKS.

---
## EC2 and Containers

Docker Containers run on **Docker Engine**, and Docker Engine runs **on EC2**.

```
EC2
├── Linux OS
├── Docker
│
├── Container 1
├── Container 2
└── Container 3
```

ECS and EKS help deploy, manage, scale, and monitor containers running on EC2 instances (or Fargate).

### Without Docker

```
EC2 Instance
├── Linux OS
├── Java
└── Spring Boot App
```
You install and manage all application dependencies directly on the EC2 server.

### With Docker

```
EC2 Instance
├── Linux OS
├── Docker Engine
│
├── Container 1
│     └── Spring Boot App
│
├── Container 2
│     └── NodeJS App
│
└── Container 3
      └── Python App
```

The EC2 instance provides CPU, Memory, Storage, and OS. Docker uses those resources to run **multiple** containers on the **same** EC2 machine — each with its own JDK, dependencies, and tools.

---
## Key Components When Launching an EC2 Instance

### AMI (Amazon Machine Image)

A pre-configured template used to create an EC2 instance — contains the OS, software, and configurations.
**Examples:** Amazon Linux, Ubuntu, Windows Server

### Instance Type

Defines the hardware configuration — CPU, Memory (RAM), Storage, Network capacity.

| Instance Type | Family | General Idea |
|---|---|---|
| `t2.micro` | T2 | Very small, good for basic learning |
| `t3.medium` | T3 | More CPU/RAM, better for applications |
| `m5.large` | M5 | General-purpose, more powerful |

> Memory trick: **Instance Type = Server Size**

### Security Group

Acts as a **virtual firewall** for an EC2 instance — controls inbound and outbound network traffic.

| Port | Purpose |
|---|---|
| 22 | SSH (Server Login) |
| 80 | HTTP (Website) |
| 443 | HTTPS (Secure Website) |

> Memory trick: **Security Group = Firewall**

### EC2 Launch Process

1. Select AMI (Operating System)
2. Select Instance Type (Server Size)
3. Configure Security Group (Firewall)
4. Launch EC2 Instance

*(Hands-on: create an EC2 instance via the AWS Console.)*
