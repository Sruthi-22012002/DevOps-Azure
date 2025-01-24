<div align="center"><h2>Deploy 3-tier-application</h2></div>

### 1. Deploy and Validate Application on a Single Public Machine
         * Step 1: Install Database, Frontend, and Backend on a Single Instance
         * Step 2: Run the Application in the Browser
### 2. Set Up a 3-Tier Application in Azure
         * Step 1: Create Virtual Network and Subnets
            * Create Virtual Network (VNet):
            * Create Subnets:
               * Frontend Subnet
               * Backend Subnet
               * Database Subnet
         * Step 2: Deploy Virtual Machines (VMs)
            * Create VMs for each subnet
            * Configure Network Security Groups (NSGs):
                  * Frontend NSG : Allow SSH (port 22) access only from the frontend VM to the backend VM.
                  * Backend NSG  : Allow database communication only from the backend VM (restrict external access).
                  * Database NSG : Restrict SSH access to the database VM (only allow SSH access from the backend VM).
                  <b>Ensure no public access to the database.</b>
### Step 3: Configure Application Communication
      1.	Restrictions:
         * Ensure no direct SSH access from the frontend to the database for security reasons.
         * Public internet access should only be allowed to the frontend VM, which acts as the gateway.
         * Ensure that the backend and database VMs are isolated from direct internet access for enhanced security.
### Step 4: Final Verification
      1.	Test the Application.

### Architecture Diagram
![image](https://github.com/user-attachments/assets/83c172fb-ec46-4c11-97be-1fb9ff64f583)

| NAT Gateway     | Application Gateway     |
|--------------|--------------|
| Translates private IP addresses from instances in a private subnet to a public IP address, enabling outbound internet connectivity. | Web traffic load balancer work on Application Layer (Layer 7) and route traffic based on source ip address and port to   destionantion ip and port|
| ![image](https://github.com/user-attachments/assets/1d0901c8-f103-498f-a6bc-adbd2f57c96e) |![image](https://github.com/user-attachments/assets/388865c0-b4f6-4fb7-902a-8ce165e4f6f6) |

![image](https://github.com/user-attachments/assets/4afd2c28-1c0f-4b53-98b1-6de359e9cc7f)

### 1. Deploy the architecture
## 1.1 Create a resource group
> To create a resource group, folloe the following link : [How to create a resource groupt](https://github.com/Sruthi-22012002/DevOps-Azure/blob/main/Azure/connect%20VM%20to%20ssh.md)
![image](https://github.com/user-attachments/assets/5a6220ca-be64-41a0-9719-16873931ef9f)

## 1.2 Create a Virtual network
> Follow this steps : [How to create a vnet](https://github.com/Sruthi-22012002/DevOps-Azure/blob/main/Azure/connect%20VM%20to%20ssh.md)

![image](https://github.com/user-attachments/assets/d57c5fcd-a4e5-44bf-8c6d-5b0f4303adcc)

### 1.2.1 Create a subnet for each tier

![image](https://github.com/user-attachments/assets/fc98b31b-71b4-4376-a952-ade4dd40f973)

* select subnet
*  Click <a href="#" style="display: inline-block; padding: 10px 20px; font-size: 14px; color: white; background-color: gray; text-align: center; text-decoration: none; border-radius: 5px;">+ Add Subnet</a>
* Enter the name and IP
* Choose the required size of the host
* Create NSG and select the check box if the VM is private.
* Click ADD 

![image](https://github.com/user-attachments/assets/f807de86-c21a-4d66-a4b0-2612a45e732e)

### 1.3 Create Virtual machine
> Follow this steps : [How to create a VM](https://github.com/Sruthi-22012002/DevOps-Azure/blob/main/Azure/connect%20VM%20to%20ssh.md)

<b> 📌As per Spec : App tier VM and databse tier VM should in private network</b>
## 1.3.1 NSG for web-tier VM
![image](https://github.com/user-attachments/assets/84ca6377-72e2-4be6-a11c-a9053110b21e)

| port   | source   | Destination  |
|------------|------------|------------|
|80(internet)| any| any|
| 22(SSH)| any| ANY|
| 3000(frontend page)| any| any|

## 1.3.2 NSG for app-tier VM
![image](https://github.com/user-attachments/assets/8b641c3a-d479-445b-919c-a27b1831c074)

| Port   | Source   | Destination   |
|------------|------------|------------|
| 8080(backend)| app-tier vm(private IP)| Db-tier(private IP)|
| 22(SSH)| web-tier(Public IP)| app-tier(private IP)|

## 1.3.3 NSG for db-tier VM
![image](https://github.com/user-attachments/assets/bb642123-4eb6-455a-9832-3b5234e28a4e)

| Port   | Source   | Destination   | Action |
|------------|------------|------------|----------|
| 3306(database)| app-tier vm(private IP)| Db-tier(private IP)|Allow|
| 3000| db-tier(Private IP)| web-tier(public IP)|<b>DENY</b>|

### Connect with SSH
web-tier -> app-tier -> db-tier

```bash
ssh username@<IP>
```
![image](https://github.com/user-attachments/assets/ee8c6df7-8794-42ca-adc0-2946d112245c)

![image](https://github.com/user-attachments/assets/3f9c0e73-00f3-42d9-bb59-b6826bea2370)

![image](https://github.com/user-attachments/assets/eae6877c-da12-49ac-953a-d205a9581518)

### Check the deployment in chrome

```bash
http://172.174.234.169:3000
```






