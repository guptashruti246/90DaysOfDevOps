# Day 50 — Kubernetes Architecture & Cluster Setup

## Overview

Kubernetes is a container orchestration platform used to automate the deployment, scaling, networking, and management of containerized applications.

For this task, I explored Kubernetes architecture and inspected my local Kubernetes cluster created using `kind`.

### Environment

* Windows
* Docker Desktop
* kind
* kubectl
* Kubernetes

---

## 1. Kubernetes Architecture

A Kubernetes cluster consists mainly of a **Control Plane** and **Worker Nodes**.

```text
                    Kubernetes Cluster
                           |
              +------------+------------+
              |                         |
        Control Plane              Worker Nodes
        (Cluster Brain)            (Run Applications)
```

### Control Plane Components

#### kube-apiserver

The Kubernetes API Server is the main entry point for communication with the cluster.

Commands such as:

```bash
kubectl get pods
kubectl get nodes
kubectl apply -f deployment.yml
```

communicate with the API Server.

The API Server validates requests and communicates with the other Kubernetes components.

---

#### etcd

`etcd` is the distributed key-value store used by Kubernetes.

It stores the cluster's state, including information about:

* Nodes
* Pods
* Deployments
* Services
* Configurations
* Desired state

```text
Kubernetes Cluster State
          |
         etcd
```

---

#### kube-scheduler

The scheduler decides which worker node should run a newly created Pod.

```text
New Pod
   |
Scheduler
   |
Suitable Worker Node
```

It considers factors such as available resources and scheduling constraints.

---

#### kube-controller-manager

Controllers continuously compare the desired state with the current state.

For example, if a Deployment specifies:

```yaml
replicas: 3
```

but only two Pods are running, Kubernetes works to create another Pod.

```text
Desired State
      |
      v
Controller
      |
      v
Current State
      |
      v
Make them match
```

This continuous reconciliation is a core Kubernetes concept.

---

## 2. Worker Node Components

Worker nodes run application workloads.

```text
Worker Node
|
+-- kubelet
+-- kube-proxy
+-- Container Runtime
+-- Pods
```

### kubelet

The kubelet is the Kubernetes agent running on every worker node.

It ensures that Pods assigned to the node are running and healthy.

```text
Scheduler
    |
    v
Worker Node
    |
  kubelet
    |
    v
Container Runtime
    |
    v
Pod
```

---

### Container Runtime

The container runtime is responsible for running containers.

Common container runtimes include:

* containerd
* CRI-O

In my local environment, Kubernetes runs through `kind` using Docker Desktop.

---

### kube-proxy

`kube-proxy` provides node-level networking functionality and helps implement Kubernetes Services and traffic forwarding.

---

## 3. CoreDNS

CoreDNS provides DNS-based service discovery inside the Kubernetes cluster.

For example, in my BankApp project:

```yaml
MYSQL_HOST: mysql-service
```

The application can use the Service name instead of directly using a Pod IP.

```text
BankApp Pod
     |
     v
mysql-service
     |
     v
MySQL Pod
```

---

## 4. How kubectl Works

When I run:

```bash
kubectl get pods
```

the request is sent to the Kubernetes API Server.

```text
kubectl
   |
   v
API Server
   |
   +---- etcd
   |
   +---- Controllers
   |
   +---- Scheduler
   |
   v
Worker Nodes
```

`kubectl` does not directly create or manage containers. It communicates with the Kubernetes API Server.

---

## 5. What Happens When a Deployment Is Created?

For example:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx
spec:
  replicas: 3
```

When I run:

```bash
kubectl apply -f deployment.yml
```

the general flow is:

```text
kubectl
   |
   v
API Server
   |
   v
Cluster State / etcd
   |
   v
Controller Manager
   |
   v
ReplicaSet
   |
   v
Pods
   |
   v
Scheduler
   |
   v
Worker Node
   |
   v
kubelet
   |
   v
Container Runtime
   |
   v
Container
```

Kubernetes continuously works to make the actual state match the desired state.

---

## 6. Local Kubernetes Cluster Using kind

`kind` stands for **Kubernetes IN Docker**.

It allows Kubernetes nodes to run as Docker containers, making it useful for local Kubernetes learning and testing.

My local setup:

```text
Windows Laptop
      |
      v
Docker Desktop
      |
      v
kind Cluster
      |
      +-- Control Plane
      |
      +-- Worker Node(s)
```

---

## 7. Commands Used

### kubectl

Check client version:

```bash
kubectl version --client
```

Check the current context:

```bash
kubectl config current-context
```

List all contexts:

```bash
kubectl config get-contexts
```

Check cluster information:

```bash
kubectl cluster-info
```

List nodes:

```bash
kubectl get nodes
```

Get detailed node information:

```bash
kubectl describe node <node-name>
```

List Pods:

```bash
kubectl get pods
```

List Pods across all namespaces:

```bash
kubectl get pods -A
```

List Pods in the `kube-system` namespace:

```bash
kubectl get pods -n kube-system
```

Get all resources in `kube-system`:

```bash
kubectl get all -n kube-system
```

Describe a Pod:

```bash
kubectl describe pod <pod-name> -n kube-system
```

---

### kind

Check kind version:

```bash
kind version
```

List kind clusters:

```bash
kind get clusters
```

Create a kind cluster:

```bash
kind create cluster
```

Create a kind cluster using a configuration file:

```bash
kind create cluster --config kind-config.yml
```

Delete a kind cluster:

```bash
kind delete cluster
```

> I did not delete my working cluster during this task because it contains other Kubernetes practice work.

---

## 8. Kubernetes System Components

To inspect Kubernetes system components:

```bash
kubectl get pods -n kube-system
```

Typical components include:

| Component               | Purpose                           |
| ----------------------- | --------------------------------- |
| kube-apiserver          | Main Kubernetes API entry point   |
| etcd                    | Stores cluster state              |
| kube-scheduler          | Assigns Pods to nodes             |
| kube-controller-manager | Maintains desired state           |
| kube-proxy              | Node networking                   |
| CoreDNS                 | Cluster DNS and service discovery |

---

## 9. Desired State and Reconciliation

Kubernetes follows a declarative model.

For example:

```yaml
replicas: 3
```

means that I want three replicas of the application.

If one Pod crashes:

```text
Desired = 3
Current = 2
```

Kubernetes detects the difference and creates another Pod.

```text
Desired State
      |
      v
Controllers
      |
      v
Current State
      |
      v
Reconciliation
```

The goal is always to bring the current state back to the desired state.

---

## 10. Connection With My BankApp Project

I have already used several Kubernetes concepts while deploying my BankApp.

The application uses:

* Deployments
* Pods
* Services
* ConfigMaps
* Secrets
* PersistentVolumes
* PersistentVolumeClaims
* kind
* kubectl
* Pod logs and troubleshooting

The BankApp uses three replicas:

```text
BankApp Deployment
        |
        +-- Pod 1
        +-- Pod 2
        +-- Pod 3
```

The BankApp communicates with MySQL through a Kubernetes Service:

```text
BankApp Pod
     |
     v
mysql-service
     |
     v
MySQL Pod
```

The application uses:

```yaml
MYSQL_HOST: mysql-service
```

instead of directly using a MySQL Pod IP.

This demonstrates Kubernetes Service discovery and cluster networking.

---

## 11. Key Learnings

* Kubernetes is a container orchestration platform.
* A Kubernetes cluster consists of a control plane and worker nodes.
* The API Server is the main communication endpoint.
* `etcd` stores Kubernetes cluster state.
* The scheduler assigns Pods to suitable nodes.
* Controllers maintain the desired state.
* kubelet manages Pods on worker nodes.
* The container runtime runs containers.
* kube-proxy provides node-level networking functionality.
* CoreDNS provides service discovery through DNS.
* `kubectl` communicates with the API Server.
* `kind` allows Kubernetes clusters to be created locally using Docker.
* Kubernetes follows a declarative and reconciliation-based model.

---

## 12. Architecture Summary

```text
                         Kubernetes Cluster
                                |
              +-----------------+-----------------+
              |                                   |
        CONTROL PLANE                        WORKER NODE
              |                                   |
       +------+-------+                    +------+-------+
       |      |       |                    |      |       |
      API    etcd  Scheduler             kubelet kube-  Runtime
     Server         Controller                    proxy
                    Manager                         |
                                                     |
                                                    Pods
```

The control plane makes decisions and maintains the desired state, while worker nodes run the application workloads.
