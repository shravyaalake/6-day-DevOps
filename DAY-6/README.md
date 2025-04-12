# Day 6 – Kubernetes Concepts: Namespace, ReplicaSet, Deployment, and Monitoring  
### 📅 Date: 03/04/2025

## 🧩 What is a Namespace in Kubernetes?

A **Namespace** is a way to divide a Kubernetes cluster into virtual sub-clusters to support multiple environments or teams within the same physical cluster.

### ✨ Default Namespaces in Kubernetes:
| Namespace         | Description                                                                 |
|-------------------|-----------------------------------------------------------------------------|
| `default`         | Automatically created; default namespace for resources like Pods, Services. |
| `kube-system`     | Holds core Kubernetes components like DNS, CLI, and Metrics Server.         |
| `kube-public`     | Accessible by all users (including unauthenticated).                         |
| `kube-node-lease` | Used by nodes to report their health status via heartbeats.                 |

### 🔧 Creating a Custom Namespace:
```bash
kubectl create ns <namespace-name>
kubectl get ns
```
>⚠️ Best Practice: Never deploy production applications in the default namespace.

### 🧪 Deploying Pods in a Custom Namespace
```bash
kubectl run test-pod --image=nginx --port=80 -n <namespace-name>
kubectl get pods -n <namespace-name>
```

## 💥 Problems When a Pod Fails

| Problem                             | Solution                                                  |
|-------------------------------------|------------------------------------------------------------|
| Application downtime                | Use **ReplicaSet** to ensure availability.                 |
| Changing Pod IP                     | Use **Service** to get a stable endpoint (URL).            |
| Data loss when pod is terminated    | Use **Volumes** for persistent storage.                    |

## 🔁 What is a ReplicaSet?

A ReplicaSet ensures that a specified number of pod replicas are running at all times. It maintains Desired State = Actual State.

#### 🧾 Commands:
```bash
kubectl apply -f rs.yml -n <namespace-name>
kubectl get rs -n <namespace-name>
kubectl get pods -n <namespace-name>
kubectl describe pod <pod-name> -n <namespace-name>
```
>If pods are stuck in Pending, you may need to add node groups via AWS EKS.

### 🚀 Creating Node Groups (AWS EKS Steps)

1. Go to AWS Console > EKS > Clusters

2. Click on your cluster > Compute > Add Node Group

3. Set:

    - Name: test1-linux

    - Launch Template: Your Template Name

    -  Instance Type: t2.medium or similar

    -   Auto Repair: Enable

4. Click Next and Create

## 🧨 ReplicaSet Limitations

Although useful, ReplicaSet is not recommended for real-world deployments because:

  - No support for rolling updates

  - No ability to roll back

## 📦 What is a Deployment?

A Deployment in Kubernetes is a higher-level controller that manages:

- ReplicaSets (which in turn manage Pods)

- Rolling Updates & Rollbacks

- Application Lifecycle
```bash
kubectl apply -f deployment.yaml -n <namespace-name>

```
## 🌐 Exposing Applications with Services

To expose applications externally or internally, Kubernetes provides Service objects.

Types of Services:

## 🔌 Kubernetes Service Types

| Service Type   | Description                                                  |
|----------------|--------------------------------------------------------------|
| ClusterIP      | Exposes the service on a cluster-internal IP.               |
| NodePort       | Exposes the service on a static port on each node.          |
| LoadBalancer   | Provisions an external IP via cloud provider.               |
>💡 In real-world scenarios, we use LoadBalancer to expose web apps.
```
kubectl get svc -n <namespace-name>
```
## 📊 Monitoring Kubernetes Clusters
#### 🔍 Why Monitoring?

- Monitoring allows us to:

    - Identify resource usage (CPU, Memory)

    - Detect unhealthy nodes or pods

    - Track application behavior over time

## 🛠️ Tools Used:
### 📊 Monitoring Tools in Kubernetes

| Tool       | Role                                                              |
|------------|-------------------------------------------------------------------|
| Prometheus | Time-series database; collects metrics (TSDB).                   |
| Grafana    | Visualization tool; displays Prometheus data using graphs/charts.|
>📈 These tools help build real-time dashboards to ensure observability and alerting.

## 🧠 Four Important YAML Fields in Kubernetes:
### 📄 Important Kubernetes YAML Fields

| Field      | Meaning                                                |
|------------|--------------------------------------------------------|
| `apiVersion` | Version of Kubernetes API used.                      |
| `kind`     | Type of Kubernetes object (Pod, Deployment, etc.)      |
| `metadata` | Metadata such as name and labels of the object.        |
| `spec`     | Specification - the desired state/configuration.       |

---

### ⚙️ Resource Requests Format

| Resource | Kubernetes Unit        |
|----------|------------------------|
| 1 CPU    | `1000m` (millicores)   |
| 1 GB RAM | `1024Mi`               |

### 🌐 Accessing Application

- Use the following format in your browser: 

      http://<EC2-Public-IP>:<Port>
- Make sure security group allows inbound access to the port defined in your service.

## ✅ Summary

### 🧩 Kubernetes Core Concepts Covered:

- **Namespaces**:  
  Logical partitions in the cluster for isolating resources (useful for multi-team environments).

- **ReplicaSet**:  
  Ensures a specified number of pod replicas are running at all times.  

- **Deployments**:  
  Manages ReplicaSets and handles the full lifecycle of your application, including rollouts and rollbacks.

- **Services**:  
  Used to expose applications to other components or externally.  
  Types of services:
  - `ClusterIP`: Internal access within the cluster.
  - `NodePort`: Exposes app on a static port of every node.
  - `LoadBalancer`: Provides external access via cloud providers.

- **Monitoring**:
  - **Prometheus**: Collects and stores time-series metrics (TSDB).
  - **Grafana**: Visualizes metrics in the form of graphs, charts, and dashboards.

---

> 📌 These are essential building blocks for deploying and managing scalable, observable, and production-ready Kubernetes applications.
