<div align ="center"><h2>Kubernetes</h2></div>

<img src="https://github.com/user-attachments/assets/f2448f9c-e78f-4f4e-afd0-004f838dbc0c" alt="Kubernetes Logo" width="60"/>**Kubernetes**
> In organizations, multiple numbers of containers run on multiple hosts at a time. So it becomes very hard to manage all the containers together, a simple solution to this would be Kubernetes. Kubernetes is an open-source platform for managing containerized workloads and services. Kubernetes take care of scaling and failover for our application running on the container.


## Architecture Diagram

https://github.com/user-attachments/assets/12e47b31-be28-4798-a8b1-5555ac64052e

### Kubernetes Master Node
In Kubernetes (k8s), a master node is the **control plane component** responsible for managing the cluster. It coordinates and schedules tasks, maintains cluster state, and monitors node health. It includes components like <b>API server, scheduler, etcd and controller manager</b>, ensuring overall cluster functionality and orchestration of containerized applications.

#### API Server
* The API server `(kube-apiserver)` exposes the Kubernetes API to enable **requests** to the cluster from **inside and outside** of the cluster.

#### etcd
* etcd is a highly available key-value store that helps **maintain** the **state** of your Kubernetes cluster and configuration  details like subnets and config maps in Kubernetes database. 

#### Schedular
* **Kube-scheduler** assigns **tasks** to worker nodes and manages **new requests** from the API Server, ensuring they are directed to healthy nodes.

#### Controller Manager
* **Kube Controller Manager** task is to **retrieve** the desired **state** from the API Server. 
<i>If the desired state does not match the current state of the object, corrective steps are taken by the control loop to align the current state with the desired state.</i>

### Kubernetes Worker Node
Worker nodes in a cluster are machines or servers running applications, controlled by the Kubernetes master. Multiple nodes connect to the master. On each node, multiple [pods](#pods) and containers operate.

#### Kubelet
* Kubelet an **agent** on each node, **communicates** with the master. It ensures pod **containers health**, executing tasks like deploying or destroying containers, reporting back to the Master.

#### Kube-proxy
* Kube-proxy enables worker node communication, managing **network rules**. It ensures rules are set for containers to communicate across nodes.

<b>Also Read:</b> [Container Runtime](#container-runtime)

#### Pods
* A Kubernetes pod is a **set of containers** on a single host, sharing storage and network. It includes specifications for container execution, enabling easy inter-container communication.

#### container Runtime
* Container Runtime, **responsible** for container **execution**, supports multiple runtimes: Docker, containers.

