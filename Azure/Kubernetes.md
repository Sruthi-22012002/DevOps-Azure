<div align ="center"><h2>Kubernetes</h2></div>

<img src="https://github.com/user-attachments/assets/f2448f9c-e78f-4f4e-afd0-004f838dbc0c" alt="Kubernetes Logo" width="60"/>**Kubernetes**
> In organizations, multiple numbers of containers run on multiple hosts at a time. So it becomes very hard to manage all the containers together, a simple solution to this would be Kubernetes. Kubernetes is an open-source platform for managing containerized workloads and services. Kubernetes take care of scaling and failover for our application running on the container.


## Architecture Diagram

<img src="https://github.com/user-attachments/assets/12e47b31-be28-4798-a8b1-5555ac64052e" alt="kubernetes" width="20"/>

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

<img src="https://github.com/user-attachments/assets/a586dd8c-f46c-429c-95c0-5c1f366ae412" alt="blue" width="20"/>

**Green Deployment(Staging) : New version to be deployed.**

<img src="https://github.com/user-attachments/assets/bb7487f0-059c-4092-8c7a-7cf9b7a20bdf" alt="green" width="20"/>

## Pods
* A Kubernetes pod is a **set of containers** on a single host, sharing storage and network.
* A pod is the smallest unit that exists in Kubernetes. It is similar to that of tokens in C or C++ languages.
* It includes specifications for container execution, enabling easy inter-container communication.

## configMap
* In Kubernetes, Configmap is an API object that is mainly used to store non-confidential data. The data that is stored in ConfigMap is stored as key-value pairs.
