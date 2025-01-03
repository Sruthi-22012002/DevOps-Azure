# 3-tier application
### Project Overview
Develop a 3 tier application and run in local machine. create a custom dockerfile for each tier.Create a volume and attach the database container.
## Features
* Add Employee list
* Show employee list
## 1. Installation 
### 1.1  Prerequisites
> 1. Java 17
> 2. Maven 3.8.8
> 3. NodeJs 14.x
> 4. MySQL 8.x
### 1.2 Setup Instructions
#### Step 1 : 
```bash
git clone https://github.com/username/project-name.git
cd project-name
```
#### Step 2 :
```bash
npm install
```
#### Step 3 :
> Environment setup
#### Step 4 :
```bash
npm start
```
## 2 . Architecture Overview
### Flow chart
#### Process flow
# Project File Structure - Process Flow

```mermaid
flowchart TD
    A[Project Root] --> B[ems-ops-phase-1]
    
    B --> C[react-hooks-frontend]
    B --> D[springboot-backend]

    C --> G[npm install]
    G --> H[npm run build]

    D --> I[target]
    I -->J[java -jar <*.jar>]
```

#### Work flow
```mermaid
flowchart TD
    A[Employee Management Application] --> B[List Employees Page]
    B --> C[Add Employee Button]
    C --> D[Open Add Employee Form]

    B --> E[Employee Table]
    E --> F[Update Button]
    F --> G[Open Update Employee Form]

    E --> H[Delete Button]
    H --> J[Delete Employee from Database]
```
## 3 . Roadmap
### 3.1 Plan
* Project overview and plan
* Installation & Environment Setup
* Build app and deploy
* Testing
* Documentation
* Review

### 3.2 Completed
* project overview and plan
   ```mermaid
  gantt
    title React App Development Timeline
    dateFormat  MM-DD-YYYY
    
    section Project Overview
    Project Overview    :done, a1, 11-24-2024, 11-24-2024
    
    section Setup and Installation
    Installation        :done, a2, 11-24-2024, 11-24-2024
    Environment Setup    :done, a3, 11-24-2024, 11-24-2024
    
    section Development and Deployment
    Build and Deploy    :done, a4, 11-25-2024, 11-26-2024
    Create Docker File  :done, a5, 11-26-2024, 11-27-2024
    
    section Testing and Review
    Testing and Review  :done, a6, 11-27-2024, 11-27-2024

  ```
## Run the application
* [Setup the backend](https://github.com/Sruthi-22012002/DevOps-Azure/blob/main/3-tier-application/react-backend.md)
* [Run the frontend](https://github.com/Sruthi-22012002/DevOps-Azure/blob/main/3-tier-application/run-frontend.md)
