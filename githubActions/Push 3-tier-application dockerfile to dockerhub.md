[3-tier-application](https://github.com/Sruthi-22012002/DevOps-Azure/tree/main/3-tier-application)
## 4. Push 3-tier-application frontend and backend dockerfile to dockerhub automatically
### 4.1. Create a new repository
```bash
mkdir .github
mkdir workflows
```
### 4.2 create a Dockerfile
```bash
sudo nano Dockerfile
```
### 4.3 Write the frontend and backend images need to build
```bash
 FROM node:16 AS build

     WORKDIR /app

   # Copy local node_modules to avoid network dependency issues
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

    # Use OpenJDK 17 as the base image
     FROM openjdk:17-jdk-slim

     # Set the working directory
     WORKDIR /app

     # Copy the JAR file of the Spring Boot application (after building it locally)
     COPY target/springboot-backend-0.0.1-SNAPSHOT.jar app.jar

    # Expose the port that the backend service will listen to
     EXPOSE 8080

    # Run the Spring Boot application
    CMD ["java", "-jar", "app.jar"]
```
### 4.4. Create a .yml for workflow
```bash
name: Build and Push Docker Image

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      # Step 1: Checkout code from the repository
      - name: Checkout code
        uses: actions/checkout@v3

      # Step 2: Set up Docker Buildx
      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v3

      # Step 3: Log in to Docker Hub
      - name: Log in to Docker Hub
        uses: docker/login-action@v3
        with:
          username: ${{ secrets.DOCKER_USERNAME }}
          password: ${{ secrets.DOCKER_PASSWORD }}

      # Step 4: Build the Docker image
      - name: Build the Docker image
        run: |
          docker build -t ${{ secrets.DOCKER_USERNAME }}/nginx-alpine:latest .

      # Step 5: Push the Docker image to Docker Hub
      - name: Push the Docker image
        run: |
          docker push ${{ secrets.DOCKER_USERNAME }}/nginx-alpine:latest
```
### 4.4.1 Need for create a secret dockurhub login
* Secrets and variables -> actions -> new repository secrets

![image](https://github.com/user-attachments/assets/8c9a0f0c-4e50-4c27-9d1c-d171b116661f)

  ![image](https://github.com/user-attachments/assets/621f1b40-bfb8-48a4-bc0f-c57bee4c0e77)
### 4.5. Commit and push your action
```bash
git add .
git commit -m "message"
git push origin main
```
> ### 4.6 Check the github action and dockerhub , image will be added in docker hub automatically, once the push happen.


