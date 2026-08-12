# 🚀 Kubernetes YAML Manifests & DevOps Practice Guide

Welcome to the **Kubernetes Manifests & DevOps Practice Repository**! This repository serves as a comprehensive reference guide, lab manual, and collection of production-ready Kubernetes YAML templates for DevOps engineers, cloud architects, and Kubernetes practitioners.

---

## 📌 Repository Overview

This project covers the full spectrum of Kubernetes concepts—from basic Pod creation to advanced workload orchestration, scheduling rules, networking, persistent storage, autoscaling, and cluster provisioning using **KIND (Kubernetes in Docker)**.

```
yaml for kubernetes/
├── ⚙️ Autoscaling/            # HorizontalPodAutoscaler (HPA) manifests
├── 🔄 Daemonset/              # DaemonSet definitions (e.g., logging agents)
├── 📦 Deployment/             # Kubernetes Deployment configurations
├── 🏥 Health Probes/          # Liveness, Readiness, and HTTP/TCP probe examples
├── 🏗️ KIND-SETUP/             # KIND multi-node cluster configurations
├── 📍 Manual Scheduling/      # Node binding using nodeName
├── 🎯 NodeAffinity/           # Node affinity rules and matchExpressions
├── 🧪 Practice/               # Weekly hands-on lab exercises and custom deployments
├── 🔁 ReplicaController/      # Legacy ReplicationController templates
├── 📊 Request-and-limits/     # Container resource limits, requests & Metrics Server
├── 🌐 Service/                # ClusterIP, NodePort, and LoadBalancer configurations
├── 🚫 Taints and Tolerations/ # Node taints, tolerations, and nodeSelectors
├── ⏱️ init/                   # InitContainer patterns and multi-container pods
├── ♻️ life_cycle/              # Pod lifecycle hook configurations
├── ⚡ one-shot/                # Production-grade combined manifests (Ingress, PV/PVC, CronJobs)
├── 📂 replicaSet/             # ReplicaSet definitions with label selectors
└── 📄 first_yaml.yaml         # Introductory standalone Nginx Pod definition
```

---

## 🛠️ Key Kubernetes Concepts & Directory Guide

### 1. 🏗️ Cluster Provisioning (`KIND-SETUP/`)
Deploy multi-node local Kubernetes clusters using [KIND (Kubernetes in Docker)](https://kind.sigs.k8s.io/).
- `kind.yaml`: Configures a 3-node cluster (1 control-plane, 2 worker nodes) with custom host port mappings (`30080:30080`).

```bash
# Create cluster using KIND configuration
kind create cluster --config KIND-SETUP/kind.yaml
```

---

### 2. 📦 Workload Orchestration
- **Pods (`first_yaml.yaml`)**: Basic containerized application unit.
- **Deployments (`Deployment/`)**: Declarative updates for Pods and ReplicaSets.
- **ReplicaSets (`replicaSet/`)**: Maintains a stable set of replica Pods running at any given time.
- **ReplicationController (`ReplicaController/`)**: Legacy controller for pod redundancy.
- **DaemonSets (`Daemonset/`)**: Ensures all (or selected) nodes run a copy of a Pod (e.g., Fluentd, Prometheus node-exporter).
- **Jobs & CronJobs (`one-shot/nginx/`)**: One-time execution tasks and scheduled batch workloads.

---

### 3. 🌐 Networking & Service Discovery (`Service/` & `one-shot/ingress/`)
Includes examples for exposing applications within and outside the cluster:
- **`service-ClusterIP.yaml`**: Exposes service on an internal IP within the cluster (default).
- **`service-NodePort.yaml`**: Exposes service on each node's IP at a static port.
- **`service-LoadBalance.yaml`**: Integrates with cloud provider load balancers.
- **`one-shot/ingress/usage.yaml`**: Layer 7 HTTP/HTTPS routing using Kubernetes Ingress rules (`/foo`, `/bar`).

```bash
# Apply ingress routing definition
kubectl apply -f one-shot/ingress/usage.yaml
```

---

### 4. 💾 Storage & Persistence (`one-shot/nginx/`)
Configurations for persistent container state management:
- **PersistentVolume (PV)**: Cluster-wide storage resource provisioning.
- **PersistentVolumeClaim (PVC)**: User request for storage resources.
- **Pod with Volume (`one-shot/nginx/Pod With Volume/`)**: Mounts PVC to deployment containers.

---

### 5. 🎯 Advanced Pod Scheduling & Node Placement
Control where and how pods are placed onto cluster nodes:
- **Manual Scheduling (`Manual Scheduling/manual.yaml`)**: Direct pod-to-node assignment using `nodeName`.
- **Node Affinity (`NodeAffinity/main.yaml`)**: Soft and hard constraints (`requiredDuringSchedulingIgnoredDuringExecution`) targeting node labels (`disktype: ssd`).
- **Taints & Tolerations (`Taints and Tolerations/`)**: Repel pods from specific nodes unless explicitly tolerated (e.g., `gpu=true:NoSchedule`).

---

### 6. 📊 Resource Management & Autoscaling (`Request-and-limits/` & `Autoscaling/`)
- **Container Limits & Requests**:
  - `mem.yaml` / `mem2.yaml`: Prevents resource contention by specifying CPU and memory boundaries.
- **Metrics Server (`metrics-server.yaml`)**: Deploys Kubernetes Metrics Server for monitoring cluster resource usage (`kubectl top`).
- **Horizontal Pod Autoscaler (`php-apache.yaml`)**: Automatically scales pod replicas based on CPU target utilization.

---

### 7. 🏥 Health Probes & Lifecycle Hooks (`Health Probes/`, `init/`, `life_cycle/`)
- **Liveness Probes**:
  - `liveness.yaml`: Command execution probe (`cat /tmp/healthy`).
  - `liveness-tcp.yaml`: TCP socket checks.
  - `liveness-https.yaml`: HTTP GET requests.
- **Init Containers (`init/init.yaml`)**: Runs initialization scripts (e.g., DNS dependency check `nslookup`) before app container startup.

---

## ⚡ Quick Start Guide

### Prerequisites
- [Kubectl CLI](https://kubernetes.io/docs/tasks/tools/) installed.
- Access to a Kubernetes cluster ([Minikube](https://minikube.sigs.k8s.io/), [KIND](https://kind.sigs.k8s.io/), or cloud K8s cluster like EKS/GKE/AKS).

### Deploying Manifests

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/kashifhm333/Kubernetes_For_DevOps.git
   cd "yaml for kubernetes"
   ```

2. **Deploy a Sample Nginx Pod**:
   ```bash
   kubectl apply -f first_yaml.yaml
   kubectl get pods
   ```

3. **Deploy a Service**:
   ```bash
   kubectl apply -f Service/service-NodePort.yaml
   kubectl get svc
   ```

4. **Deploy Horizontal Pod Autoscaler (HPA)**:
   ```bash
   kubectl apply -f Request-and-limits/metrics-server.yaml
   kubectl apply -f Autoscaling/php-apache.yaml
   kubectl get hpa
   ```

5. **Clean Up Resources**:
   ```bash
   kubectl delete -f <manifest-file.yaml>
   ```

---

## 🧪 Hands-On Practice Labs (`Practice/`)

The `Practice/` directory contains structured exercises divided into weekly milestones:
- **`first-week-practice/`**: Core deployments, multi-tier services, namespaces, and initialization containers.
- **`own_image_launch/`**: Deploying custom container images into cluster environments.
- **`third-week-practice/`**: Advanced deployment rollouts and strategy testing.

---

## 📄 License & Author

Maintained for learning, DevOps training, and practical Kubernetes engineering.
Free to use and adapt for personal or professional projects!
