<div align="center"><h1>Azure Container App - Manual</h1></div>

> Azure Container Apps enables you to run microservices and containerized applications on a serverless platform. With Container Apps, you enjoy the benefits of running containers while leaving behind the concerns of manually configuring cloud infrastructure and complex container orchestrators.
### Common uses of Azure Container Apps include:
* Deploying API endpoints
* Hosting background processing jobs
* Handling event-driven processing
* Running microservices

![image](https://github.com/user-attachments/assets/aada39da-2bf2-4b5d-8320-3559b65ec447)

## Container registry
> Azure Container Registry allows you to build, store, and manage container images and artifacts in a private registry for all types of container deployments. Use Azure container registries with your existing container development and deployment pipelines. Use Azure Container Registry Tasks to build container images in Azure on-demand, or automate builds triggered by source code updates, updates to a container's base image, or timers.

### Create a container registry
> Search for **"Container Registry"** in azure portal

![image](https://github.com/user-attachments/assets/77b48c17-5df8-476d-a38c-7673ab9fbe5c)

![image](https://github.com/user-attachments/assets/f5a03ee3-e1bb-4ed1-8339-c9da6b029f5d)

> In the **Basics** tab, enter values for Resource group and Registry name.

> Accept default values for the remaining settings. Then select **Review + create**. After reviewing the settings, select **Create**. 

![image](https://github.com/user-attachments/assets/7ca04ed9-237a-42ad-a7b4-caf1d5b36109)

> When the **Deployment succeeded** message appears, select the container registry in the portal.

## Push the Docker image to container registry
> Create a docker image for frontend application, inside the **<i>react-hooks-frontend/</i>**
```bash
sudo nano Dockerfile
```

```bash
FROM node:16 AS build
WORKDIR /app
COPY package.json package-lock.json ./
RUN npm config set timeout 600000 \
&& npm config set registry https://registry.npmmirror.com \
&& npm config set strict-ssl false
COPY . .
RUN npm install --offline || npm install --legacy-peer-deps --force
RUN npm run build
FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```
> Create a docker image for backend application, inside the **<i>springboot-backend/</i>**
```bash
sudo nano Dockerfile
```
```bash
# Java 17
FROM openjdk:17-jdk-slim
# Set working directory
WORKDIR /app
# Install Maven
RUN apt-get update && apt-get install -y maven && rm -rf /var/lib/apt/lists/*
# Copy the Maven project files
COPY pom.xml .
COPY src ./src
# Build the application
RUN mvn clean package -DskipTests
# Copy the built JAR file to the final location
RUN mv target/springboot-backend-0.0.1-SNAPSHOT.jar /app/springboot-backend-0.0.1-SNAPSHOT.jar
# Expose the application port
EXPOSE 8080
# Run the application
ENTRYPOINT ["java", "-jar", "springboot-backend-0.0.1-SNAPSHOT.jar"]
```
### Create Azure mysql server

> update the **application.properties** file in springboot-backend
```bash
spring.datasource.url=jdbc:mysql://demo-server-sql-mysql.mysql.database.azure.com:3306/employees?useSSL=true&requireSSL=true&verifyServerCertificate=true
spring.datasource.username=demoserver22
spring.datasource.password=Sruthi@22012002
spring.jpa.properties.hibernate.dialect = org.hibernate.dialect.MySQLDialect
spring.jpa.hibernate.ddl-auto = update
```
### Create a docker-compose.yml to run job in github action

> Create a docker compose file for **both frontend and backend** to run the job, inside the **<i>ems-ops-phase-0/</i>**

```bash
mkdir .github
cd .github
mkdir workflow
cd .github/workflow
```

```bash
sudo nano docker-compose.yml
```
```bash
name: Build & Push to ACR

on:
  push:
    branches:
      - main

permissions:
  id-token: write
  contents: read

jobs:
  build-and-push:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout Repository
      uses: actions/checkout@v3

    # Login to Azure using OIDC authentication
    - name: Login to Azure
      uses: azure/login@v1
      with:
        client-id: ${{ secrets.AZURE_CLIENT_ID }}
        tenant-id: ${{ secrets.AZURE_TENANT_ID }}
        subscription-id: ${{ secrets.AZURE_SUBSCRIPTION_ID }}

    # Login to Azure Container Registry (ACR)
    - name: Login to Azure Container Registry (ACR)
      run: |
        echo "${{ secrets.REGISTRY_PASSWORD }}" | docker login ${{ secrets.ACR_NAME }}.azurecr.io -u ${{ secrets.REGISTRY_USERNAME }} --password-stdin

    # Build and Push Frontend Image
    - name: Build and Push Frontend
      run: |
        docker build -t ${{ secrets.ACR_NAME }}.azurecr.io/frontend:latest ./react-hooks-frontend
        docker push ${{ secrets.ACR_NAME }}.azurecr.io/frontend:latest

    # Build and Push Backend Image with Database Secrets
    - name: Build and Push Backend
      run: |
        docker build \
          --build-arg DB_HOST=${{ secrets.DB_HOST }} \
          --build-arg DB_PORT=${{ secrets.DB_PORT }} \
          --build-arg DB_USER=${{ secrets.DB_USER }} \
          --build-arg DB_PASSWORD=${{ secrets.DB_PASSWORD }} \
          --build-arg DB_NAME=${{ secrets.DB_NAME }} \
          -t ${{ secrets.ACR_NAME }}.azurecr.io/backend:latest ./springboot-backend

        docker push ${{ secrets.ACR_NAME }}.azurecr.io/backend:latest
```
### Push the image in github actions
```bash
git add .
```
```bash
git commit -m "docker image"
```
```bash
git push origin main
```
### List the container images
> To list the images in your registry, navigate to your registry in the portal and select **Repositories**,

![image](https://github.com/user-attachments/assets/18020b13-41ee-4e43-90d3-d031d8dc8fa4)

## Create container app
 > To create your container app, start at the Azure portal home page.
    * Search for Container Apps in the top search bar.
    * Select **Container Apps** in the search results.
    * Select the Create button.

![image](https://github.com/user-attachments/assets/5edc8f28-3979-41f6-926e-b501c631d43c)

![image](https://github.com/user-attachments/assets/296215be-f104-4fd7-b120-2e044b070fd6)

> In the **Basics** tab, do the following actions.

#### * Project details
![image](https://github.com/user-attachments/assets/dc3bf724-3cab-43e5-aa9e-753b7796edb8)

#### * Container Apps Environment
![image](https://github.com/user-attachments/assets/d98dad1d-a5c3-4f35-b0aa-24ae58c5f0f5)

> In the **Container** tab, do the following actions.

* Fill container details, others use default values
  
![image](https://github.com/user-attachments/assets/1305ebfd-fe7d-4d7c-8baf-939828ef0fdd)

> In the **ingress** tab, do the following actions.

* <b>Enable</b> the ingress
![image](https://github.com/user-attachments/assets/a2d6f898-b438-4f0e-aa9f-ee715ca4c2be)

* Fill the port number 80(frontend) and 8080(backend).

> Select **Review and create** at the bottom of the page.

## Verify deployment

> Select **Go to resource** to view your new container app.

> Select **Create**

> Select the link next to **Application URL** to view your application. The following message appears in your browser.

![image](https://github.com/user-attachments/assets/3c81f63f-aaf4-445c-b4d4-f16f39fc31ff)

 💡 **Tip:** After the backend container created, copy and paste the application URL in **EmployeeService.js** to access the backend
 
 ```bash
const EMPLOYEE_BASE_REST_API_URL = 'https://backend-container-app.salmonhill-fdb0b10f.eastus.azurecontainerapps.io/api/v1/employees';
```

## Final page

![image](https://github.com/user-attachments/assets/e6dbfd58-6a34-46ac-af48-298a44265b50)


