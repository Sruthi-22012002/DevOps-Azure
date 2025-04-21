<div align ="center"><h2>Kubernetes</h2></div>

<img src="https://raw.githubusercontent.com/kubernetes/kubernetes/master/logo/logo.png" alt="Kubernetes Logo" width="20"/> **Kubernetes**
> Kubernetes is an open-source container orchestration platform used to automate the deployment, scaling, and management of containerized applications. It simplifies the process of managing applications by automating tasks like scaling, monitoring, and updating, making it easier to run distributed applications at scale.

## Architecture Diagram

<img src="https://github.com/user-attachments/assets/12e47b31-be28-4798-a8b1-5555ac64052e" alt="kubernetes" width="700"/>

### Kubernetes Master Node
In Kubernetes (k8s), a master node is the **control plane component** responsible for managing the cluster. It coordinates and schedules tasks, maintains cluster state, and monitors node health. It includes components like <b>API server, scheduler, etcd and controller manager</b>, ensuring overall cluster functionality and orchestration of containerized applications.

#### API Server
* The API server `(kube-apiserver)` exposes the Kubernetes API to enable **requests** to the cluster from **inside and outside** of the cluster.

#### etcd
* etcd is a highly available key-value store that helps **maintain** the **state** of your Kubernetes cluster and configuration  details like subnets and config maps in Kubernetes database. 

#### Schedular
* `Kube-scheduler` assigns **tasks** to worker nodes and manages **new requests** from the API Server, ensuring they are directed to healthy nodes.

#### Controller Manager
* `Kube Controller Manager` task is to **retrieve** the desired **state** from the API Server.

<i>If the desired state does not match the current state of the object, corrective steps are taken by the control loop to align the current state with the desired state.</i>

### Kubernetes Worker Node
Worker nodes in a cluster are machines or servers running applications, controlled by the Kubernetes master. Multiple nodes connect to the master. On each node, multiple [pods](#pods) and containers operate.

#### Kubelet
* Kubelet an **agent** on each node, **communicates** with the master. It ensures pod **containers health**, executing tasks like deploying or destroying containers, reporting back to the Master.

#### Kube-proxy
* Kube-proxy enables worker node communication, managing **network rules**. It ensures rules are set for containers to communicate across nodes.

#### container Runtime
* Container Runtime, **responsible** for container **execution**, supports multiple runtimes: Docker, containers.
  
<b>Guide:</b> [Kubernetes](https://k21academy.com/docker-kubernetes/kubernetes-architecture-components-overview-for-beginners/)

## Node pools
* In AKS, nodes of the **same configuration** such as machine size, CPU, memory, and disk specifications are **grouped** together into node pools. These node pools contain the underlying virtual machine scale sets and virtual machines (VMs) that run your applications.

## Name Space
* Kubernetes Namespace is a mechanism that enables you to organize resources. It is like a virtual cluster inside the cluster.
* A namespace isolates the resources from the resources of other namespaces.
* Each namespace has its own set of policies, resources, and access controls making them ideal for the environments such as development, staging and production.
### Kubernetes Namespaces
> When the kubernetes cluster is setup, at that time 4 kubernetes namespaces are created, each with some specific purpose. Those are as follows:

* **kube-system:** System processes like **Master and kubectl processes** are deployed in this namespace; thus, it is advised not to create or modify the namespace.
* **kube-public:** This namespace contains **publicly accessible data** like a [configMap](#configmap) containing cluster information.
* **kube-node-lease:** This namespace is the **heartbeat** of nodes. Each node has its associated lease object. It determines the availability of a node.
* **default:** This is the namespace that you use to create your resources by default.
### Create namespace
```bash
kubectl create namespace your-namespace
```
### Sample code
  ```bash
    apiVersion: v1
    kind: Namespace
    metadata:
      name: test-ns
      labels:
        team: testingteam
  ```
### Run namespace
  ```bash
  kubectl get namespace
  ```
### Blue-Green Deployment
> The blue/green deployment technique enables you to release applications by shifting traffic between two identical environments that are running different versions of the application.

**Blue Deployment(Production) : Current live version.**

<img src="https://github.com/user-attachments/assets/a586dd8c-f46c-429c-95c0-5c1f366ae412" alt="blue" width="700"/>

**Green Deployment(Staging) : New version to be deployed.**

<img src="https://github.com/user-attachments/assets/bb7487f0-059c-4092-8c7a-7cf9b7a20bdf" alt="green" width="700"/>

## Pods
* A Kubernetes pod is a **set of containers** on a single host, sharing storage and network.
* A pod is the smallest unit that exists in Kubernetes. It is similar to that of tokens in C or C++ languages.
* It includes specifications for container execution, enabling easy inter-container communication.

### Pods in two many ways
* **Pods that run a single container.** The `one-container-per-Pod` model is the most common Kubernetes use case; in this case, you can think of a Pod as a wrapper around a single container; Kubernetes manages Pods rather than managing the containers directly.

* **Pods that run multiple containers** that need to work together. A Pod can **encapsulate** an application composed of multiple co-located containers that are tightly coupled and need to share resources. These co-located containers form a single cohesive unit.

### Sample pod .yaml file
#### Create
```bash
kubectl create -f simple-pod.yml
```
#### Script
```bash
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - name: nginx
    image: nginx:1.14.2
    ports:
    - containerPort: 80
```
#### Run
```bash
kubectl apply -f simple-pod.yaml
```

## Kubernetes Service

### 1. Deploy application (new)
> Purpose: Deploy your application directly to a Kubernetes cluster.

* This is a wizard-based tool to help you deploy containerized applications quickly to AKS (Azure Kubernetes Service).
* You can specify container images, replica count, ports, and other settings.
* It simplifies the process of writing yaml manifests manually.

### 2. Kubernetes cluster
> Purpose: Create a fully managed AKS cluster.

* This is the option to create an Azure Kubernetes Service (AKS) cluster.
* You get full control over the cluster configuration, including:
    * Node pools
    * Networking
    * Monitoring
    * Authentication
* Best suited for production environments needing scalability and customization.

### 3. Automatic Kubernetes cluster (preview)
> Purpose: Quickly deploy a Kubernetes cluster with automated settings (currently in preview).

* Automatically provisions the AKS cluster using best practice defaults.
* Minimizes setup time for developers who want to focus on deploying apps rather than managing infrastructure.
* May include built-in GitOps, monitoring, etc.
* Preview means it's in a testing phase and may change.

### 4. Add a Kubernetes cluster with Azure Arc
> Purpose: Connect an existing on-premises or multi-cloud Kubernetes cluster to Azure.

* Azure Arc lets you manage non-Azure Kubernetes clusters from within Azure.
* Useful for hybrid or multi-cloud scenarios.
* Provides visibility and governance using Azure tools (like Policy, Monitor, etc.)

### 5. Create a Kubernetes cluster with Azure Arc
> Purpose: Use Azure Arc to provision a Kubernetes cluster outside of Azure (e.g., on your VM or bare metal).

* You can create and onboard a new Kubernetes cluster that’s not in Azure but still manageable from Azure.
* Useful for organizations with existing infrastructure outside Azure wanting centralized control.
  
## configMap
* In Kubernetes, Configmap is an API object that is mainly used to store non-confidential data. The data that is stored in ConfigMap is stored as key-value pairs.
