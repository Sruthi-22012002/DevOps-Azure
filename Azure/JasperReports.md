<div align ="center"><h2>JasperReports® Server</h2></div>

 ## Introduction
* JasperReports® Server builds on the `JasperReports® Library` as part of a comprehensive family of Business Intelligence (BI) products`, providing robust static and interactive reporting, reportserver, and data analysis capabilities.
* These capabilities are available as either stand-alone(only one tool) products, or as part of an integrated end-to-end BI suite(all tools together).
* The products utilize common metadata(common data definitions) and provide shared services, such as security, a repository, and scheduling.
* This enables seamless integration with other applications and the capability to add custom functionality with ease.

### `The heart of the Jaspersoft® BI Suite is the JasperReports server`, which provides the ability to:
 * Easily create reports based on views designed in an intuitive, web-based, drag and drop tool(Ad Hoc Editor).
 * Efficiently and securely manage many reports.
 * Interact with reports, including sorting, changing formatting, entering parameters, and drilling on data.
 * Schedule reports for distribution through email and storage in the repository.
 * Combine reports and visual elements to create interactive dashboards that clearly show business trends.
## Architecture diagram
<p align="center"><img src="https://github.com/user-attachments/assets/700e4640-803a-4b2d-ada1-3e49c5d5291d" alt="managed cluster" width="400"/></div>

## JasperReports Server Distributions
> JasperReports Server is a web application that runs in an app server and uses an external database to store its repository.

JasperReports Server is available in two distributions: a **binary installer** for evaluation and a **WAR file** for production.
### Binary Installer
* The `binary installer` is an executable file that includes the **Tomcat application server and PostgreSQL database** so that it is fully self-contained.
*  The installer software leads you through the options and installs Tomcat and PostgreSQL with default settings for JasperReports Server to use.
*  The binary installer runs on desktops and laptops under Linux, MacOS, and Windows (64-bit), so you can quickly install an instance of JasperReports Server and explore all of its features.
### WAR file
* The WAR (web archive) file is a zipped file containing only the JasperReports Server web app.
* To install the WAR file in production, you must first install and configure one of the supported app servers (for example Tomcat, JBoss, WebLogic, or Websphere) and one of the supported databases (most major relational databases)
* The WAR file distribution includes scripts that you edit to specify your app server and database.
* When you run these scripts, they create the necessary tables in your database and copy the files of the web app to your app server.
 > To install TIBCO(is the company that owns and develops JasperReports Server) for enterprise production environments, use the **stand-alone WAR file distribution**, which is the official TIBCO JasperReports Server installer.

#### Download 
[Jaspersoft](https://www.jaspersoft.com/support) -> Products -> community edition -> Download Now

<p align="center"><img src="https://github.com/user-attachments/assets/3c96649e-f0fb-4d3b-8a93-439a5c732fd1" alt="managed cluster" width="400"/></div>

## System Requirements
 The following table contains the minimum and recommended resources for a full installation that includes PostgreSQL and an application server.
 
 <p align="center"><img src="https://github.com/user-attachments/assets/70f26645-eb22-46d0-8c05-7390c6748b63" alt="managed cluster" width="400"/></div>

##  Installation Types
 As of version 8.0, JasperReports Server supports the following installations:
 * **Compact installation:** The Repository, Audit, Access, and Monitoring tables are created in a single repository database. This is the same configuration as previous versions.
> The Access and Audit events are now processed asynchronously using a thread pool. The default installation is the Compact installation.

 * **Split installation:** Only the Repository tables are created in the repository database. The Audit, Access, and Monitoring tables are created in a separate audit database.
> The binaryinstaller does not support split installation. For split installation, use the stand-alone WAR file distribution, which is the official JasperReports Server installer

##  The Setup
> We are setting up JasperReports Server (Java-based Business Intelligence tool) on Azure Kubernetes Service (AKS) using the WAR file distribution. This means:

* The application will be containerized using Docker (Tomcat + WAR).
* It will be deployed into a Kubernetes cluster (AKS).
* A persistent database (e.g., Azure Database for PostgreSQL) will store metadata and repository data.
* Access to the server will be exposed using Ingress Controller or LoadBalancer.
* Kubernetes PersistentVolumeClaims will be used to retain logs and repository content.

##  Tools Required
* Docker: To build and test container images.
* kubectl: To interact with the AKS cluster.
* Azure Kubernetes Service (AKS)
* Azure Container Registry (ACR)
* Azure Database for PostgreSQL / MySQL
* Azure Files or Disks for persistent storage

## Step 1: Prerequisites

Make sure you have these installed:

- Minikube – runs Kubernetes locally

- kubectl – CLI to interact with Kubernetes

- Docker – builds & pulls container images

Check with:
```
minikube version
kubectl version --client
docker --version
```
## Step 2: Start Minikube
```
minikube start
```
This will create a local Kubernetes cluster.

## Step 3: Enable Ingress (optional but useful)
```
minikube addons enable ingress
```
This allows you to access JasperReports through a friendly URL (or just use service port).

## Step 4: Deploy PostgreSQL as the database

1.Create a file postgres-deployment.yaml:

```
nano postgres-deployment.yaml
```
```
apiVersion: v1
kind: Service
metadata:
  name: postgres
spec:
  type: ClusterIP
  ports:
    - port: 5432
  selector:
    app: postgres
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: postgres
spec:
  replicas: 1
  selector:
    matchLabels:
      app: postgres
  template:
    metadata:
      labels:
        app: postgres
    spec:
      containers:
        - name: postgres
          image: postgres:13
          env:
            - name: POSTGRES_DB
              value: jasperdb
            - name: POSTGRES_USER
              value: jasper
            - name: POSTGRES_PASSWORD
              value: jasper123
          ports:
            - containerPort: 5432

```
2.Apply it:
```
kubectl apply -f postgres-deployment.yaml
```
## Step 5: Deploy JasperReports Server

1.Create a file jasper-deployment.yaml: 

```
nano jasper-deployment.yaml
```
```
apiVersion: v1
kind: Service
metadata:
  name: jasperreports
spec:
  type: NodePort
  ports:
    - port: 8080
      targetPort: 8080
      nodePort: 30080
  selector:
    app: jasperreports
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: jasperreports
spec:
  replicas: 1
  selector:
    matchLabels:
      app: jasperreports
  template:
    metadata:
      labels:
        app: jasperreports
    spec:
      containers:
        - name: jasperreports
          image: bitnami/jasperreports:latest
          ports:
            - containerPort: 8080
          env:
            - name: JASPERREPORTS_DATABASE_TYPE
              value: postgresql
            - name: JASPERREPORTS_DATABASE_HOST
              value: postgres
            - name: JASPERREPORTS_DATABASE_PORT_NUMBER
              value: "5432"
            - name: JASPERREPORTS_DATABASE_NAME
              value: jasperdb
            - name: JASPERREPORTS_DATABASE_USER
              value: jasper
            - name: JASPERREPORTS_DATABASE_PASSWORD
              value: jasper123
            - name: JASPERREPORTS_USERNAME
              value: jasperadmin
            - name: JASPERREPORTS_PASSWORD
              value: jasperadmin

```
2. Apply it:
```
kubectl apply -f jasper-deployment.yaml
```
## Step 6: Check pods are in running state and service


## Commands use to Create and access jasperreport server
> list all the services
```
kubectl get svc
```
> Describe the services
```
kubectl describe svc jasperreports
```
> Status of minikube
```
minikube status
```
> watch your pods in real time.
```
kubectl get pods -w
```
## Step 7:Access JasperReports in Browser

1.Get the IP:
```
minikube ip
```
2.Access JasperReports using:
```
http://<minikube-ip>:30080
```
```
minikube service jasperreports
```
<p align="center"><img src="https://github.com/user-attachments/assets/e9db740b-6a84-4f6f-b62b-1a0dea0752b2" alt="managed cluster" width="400"/></div>

## page redirects to : 

<p align="center"><img src="https://github.com/user-attachments/assets/c646288b-b634-483b-9c44-72f24348388f" alt="managed cluster" width="400"/></div>

3.Log in with:

   - Username: jasperadmin

   - Password: jasperadmin

<p align="center"><img src="https://github.com/user-attachments/assets/3984e0e9-dafb-418d-892b-481501a229d6" alt="managed cluster" width="400"/></div>


