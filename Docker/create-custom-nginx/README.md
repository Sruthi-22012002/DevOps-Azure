## 3. Create a custom Dockerfile
> custom dockerfile is about to run /html file automatically
### 3.1. Create a simple index file in /html directory
```bash
<!DOCTYPE html>
<html>
<head>
    <title>Welcome to Custom Nginx!</title>
</head>
<body>
    <h1>Hello from Custom Nginx Container!</h1>
</body>
</html>
```
#### 3.2. Create a Nginx Dockefile
> Use the official Nginx image as the base
```bash
    FROM nginx:latest
```
> Copy your static files (optional)
```bash
    COPY ./html /usr/share/nginx/html
```
> Expose port 80 for web traffic
```bash
    EXPOSE 80
```
> Start Nginx
```bash
   CMD ["nginx", "-g", "daemon off;"]
```
### 3.3 Build and Run the Custom Nginx Container
> 3.1. Build the Docker image
```bash
    docker build -t custom-nginx .
```
> 3.2. Run the container
```bash
    docker run -d -p 80:80 custom-nginx
```
> 3.3. Access the Nginx server
* Open your browser and go to [localhost:8080](http://localhost:80).
### 3.4. sample page ⚠️ Warning: Whatever is on that index.html will come here
![Aspose Words c46c1ede-2ded-4176-b654-cdbce6cebf13 006](https://github.com/user-attachments/assets/6f020f05-70c5-478b-abcd-53bd33e5ce5d)

<div align="right">
    
### ---> [4. volume](https://github.com/Sruthi-22012002/DevOps-Azure/tree/main/Docker/volume)

</div>




