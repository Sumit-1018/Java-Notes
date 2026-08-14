# Day 33 - EKS + Node Group Creation Walkthrough
*Wed, 12 Aug 2026*

A hands-on, step-by-step walkthrough for standing up an EKS cluster and deploying a test workload — builds directly on the EKS concepts from Day 31.

## 1. Create a VPC

```
AWS Console
→ Search VPC
→ Create VPC
→ Select "VPC and More"
→ Availability Zones = 2
→ Keep default subnets
→ Create VPC
```
Note the **VPC ID** — you'll need it later.

## 2. Create the EKS Cluster IAM Role

Gives AWS permission to access other AWS services on the cluster's behalf.

```
IAM → Roles → Create Role

Trusted Entity: AWS Service
Use Case: EKS → EKS Cluster
Attach Policy: AmazonEKSClusterPolicy
Role Name: MyEKSClusterRole

Create Role
```

## 3. Add Required Policies to the Cluster Role

Open `MyEKSClusterRole` and attach:

- `AmazonEKSBlockStoragePolicy`
- `AmazonEKSComputePolicy`
- `AmazonEKSLoadBalancingPolicy`
- `AmazonEKSNetworkingPolicy`

## 4. Create the Node IAM Role

```
IAM → Roles → Create Role

Trusted Entity: AWS Service
Use Case: EC2
Attach Policies:
  - AmazonEKSWorkerNodePolicy
  - AmazonEKS_CNI_Policy
  - AmazonEC2ContainerRegistryReadOnly

Role Name: MyEKSNodeRole

Create Role
```

## 5. Create the EKS Cluster

```
EKS → Clusters → Create Cluster

Cluster Name: MyEKSCluster
Cluster IAM Role: MyEKSClusterRole
Select: VPC created earlier
Select: all available subnets

Create Cluster
```
Wait until **Status = Active**.

## 6. Create a Node Group

```
EKS → MyEKSCluster → Compute → Add Node Group

Node Group Name: MyNodeGroup
Node IAM Role: MyEKSNodeRole

Next
```

## 7. Configure the Node Group

```
AMI: Amazon Linux 2
Instance Type: t3.large
Desired Size: 1
Minimum Nodes: 1
Maximum Nodes: 2

Next
```

## 8. Select Subnets

```
Select subnets from the VPC
Create Node Group
```
Wait until **Node Group Status = Active**.

## 9. Open CloudShell

```
AWS Console → Click CloudShell (>_)
```

## 10. Connect to the Cluster

```bash
aws eks update-kubeconfig --region ap-south-1 --name MyEKSCluster
```

## 11. Verify Nodes

```bash
kubectl get nodes
```
Expected: **STATUS = Ready**

## 12. Deploy Nginx

```bash
kubectl create deployment nginx --image=nginx

# check pods
kubectl get pods
```

## 13. Expose Nginx

```bash
kubectl expose deployment nginx --port=80 --type=LoadBalancer
```

## 14. Get the Public URL

```bash
kubectl get svc
```
Copy the `EXTERNAL-IP` / DNS value and open it in a browser.

**Expected output:** `Welcome to nginx!`

---
## Summary of the Full Flow

```
VPC → IAM Roles (Cluster + Node) → EKS Cluster → Node Group
    → CloudShell → kubectl connect → Deploy → Expose → Access via Load Balancer
```

This mirrors the EKS architecture covered on Day 31 (Users → Load Balancer → Ingress → Kubernetes Service → Pods → Containers) — here you're building that exact chain by hand, end to end, on a real AWS account.
