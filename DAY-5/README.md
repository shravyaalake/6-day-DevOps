# Day 5 - Kubernetes & Container Orchestration (02/04/2025)
## Github link: https://github.com/shravyaalake/Retail-App_kubernetes.git
## Github link : https://github.com/shravyaalake/shravya-k8s-manifests.git
## 🚨 Problems with Containers

While containers (like Docker) are efficient for lightweight application deployment, they come with several limitations:

- ❌ **No Auto Scaling**  
  - Cannot automatically scale up or down based on traffic.
  - **Vertical Scaling**: Increasing resources (CPU, RAM) on the same system.
  - **Horizontal Scaling**: Adding/removing instances to match demand.

- ❌ **No Built-in Load Balancing**  
  - Cannot distribute traffic across multiple containers by itself.

- ❌ **No Self-Healing**  
  - If a container fails, it causes downtime. It cannot automatically recover.

---

## ✅ Solution: Kubernetes (K8s)

Kubernetes is a **container orchestration tool** that solves the above issues by:

- 🔁 **Orchestration** – Automating container deployment, management, scaling, and networking.
- 📈 **Auto Scaling** – Automatically adjusts the number of container instances.
- ⚖️ **Load Balancing** – Efficiently distributes traffic across containers.
- 🛠 **Self-Healing** – Automatically replaces failed containers.

> Kubernetes is **platform-independent** and can run on any cloud (AWS, GCP, Azure) or on-premises.

---
## ☸️ Kubernetes Concepts

### 🧱 Core Objects

- **Pods**: Smallest deployable units in Kubernetes.
- **ReplicaSets**: Ensure specified number of pods are always running.
- **Deployments**: Manage ReplicaSets; used for scaling, rolling updates.
- **Namespaces**: Provide logical separation between Kubernetes resources.

### 🗂️ Common Namespaces

| Namespace           | Description                              |
|---------------------|------------------------------------------|
| `default`           | Default workspace                        |
| `kube-system`       | Core system processes                    |
| `kube-public`       | Public cluster info                      |
| `kube-node-lease`   | Node heartbeats                          |

```bash
kubectl create ns <namespace>
kubectl get pods -n <namespace>
```
---
### 🌐 Services in Kubernetes

| Type           | Description                                             |
|----------------|---------------------------------------------------------|
| `ClusterIP`    | Exposes service internally within the cluster           |
| `NodePort`     | Exposes service on a static port on each node           |
| `LoadBalancer` | Provisions external IP through cloud provider           |

```bash
kubectl get svc -n <namespace>
```
---

## 🛠️ Setup Steps

### 1. Launch EC2 Instance (Ubuntu)
- Name: Your choice  
- Storage: 30 GB  
- Create and download key pair (.ppk)

### 2. Install CLI Tools

Install the following tools on your EC2 instance:

- `kubectl` – Kubernetes CLI  
- `eksctl` – EKS CLI for AWS  
- `awscli` – AWS CLI  

```bash
snap install kubectl --classic
```
### 3. Create IAM User for EKS

    Go to IAM → Users → Create Use  

    Username: your-choice  

    Skip checkboxes  

    Attach Policy: Administrator Access 

    Create and Download CSV (contains access & secret keys)

### 4. Configure AWS CLI

aws configure

Enter:

    AWS Access Key

    Secret Access Key

    Region

    Output Format

### 5. Create a Cluster

Use eksctl to create a Kubernetes cluster:
```bash
eksctl create cluster --name my-cluster --region <region> --nodegroup-name standard-workers --node-type t2.micro --nodes 2
```
## 🧠 Kubernetes Concepts
### 🔹 What is a Cluster?

A Cluster is a group of instances (nodes) that run containerized applications. It includes:

- Master Node – Controls and manages the cluster.

- Worker Nodes – Run the actual applications (pods).

🔹 Types of Clusters

- On-Premise Cluster – You manage everything.

- Cloud Managed Cluster – Cloud provider (e.g., AWS) manages the master node.

- AWS uses EKS (Elastic Kubernetes Service) for this.

## ⚙️ Master Node Components

| Component     | Description                                                                 |
|---------------|-----------------------------------------------------------------------------|
| API Server    | Frontend for the Kubernetes control plane. Handles requests from CLI/UI.   |
| ETCD          | Key-value store for all cluster data.                                       |
| Controller    | Ensures the actual state matches the desired state (self-healing).          |
| Scheduler     | Assigns pods to nodes based on resource availability and requirements.      |

## ⚙️ Worker Node Components

| Component         | Description                                                                 |
|-------------------|-----------------------------------------------------------------------------|
| Kubelet           | Agent that talks to the master and starts/stops pods as instructed.         |
| Container Runtime | (e.g., Docker) Pulls images, creates and manages containers.                |
| Kube-Proxy        | Handles networking, forwarding traffic to the right containers.             |

## 📦 Pods

- Smallest deployment unit in Kubernetes.

- A pod wraps one or more containers with shared storage/networking.

    📁 Manifest File (YAML)
Structure:
## 📄 Four Important Fields in Kubernetes Manifest

| **Field**     | **Meaning**                                              |
|---------------|----------------------------------------------------------|
| `apiVersion`  | Specifies the version of the Kubernetes API              |
| `kind`        | Defines the type of Kubernetes object (e.g., Pod, Deployment) |
| `metadata`    | Contains metadata such as the name and labels of the object |
| `spec`        | Defines the desired state or configuration of the object  |

## 🧪 Kubernetes Commands
```bash
 kubectl apply -f pod.yaml // Deploy the pod

 kubectl get pods //List running pods

 kubectl get pods -o wide //Show more info (like IP)

 kubectl describe pod sample-pod //Inspect pod details
```
To expose your pod (via EC2 Public IP):

   - Update your security group (inbound rule):

       - Type: All traffic

       - Source: My IP or Anywhere (0.0.0.0/0)

   - In your browser:

         👉 [http://<EC2-Public-IP>:<Port>]

## ⚙️ Kubernetes Resource Units

| **Resource** | **Kubernetes Unit**    |
|--------------|------------------------|
| 1 CPU        | `1000m` (millicores)   |
| 1 GB RAM     | `1024Mi` (Mebibytes)   |

## ✅ Summary

By using Kubernetes, we overcome the limitations of traditional containers and gain powerful orchestration capabilities. We can now deploy, scale, and manage applications more reliably and efficiently in the cloud.
