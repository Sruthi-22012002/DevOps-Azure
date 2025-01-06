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
![image](https://github.com/user-attachments/assets/ed98a300-6907-4509-acbd-27b02592ad83)

### NAT Gateway
> A NAT Gateway (Network Address Translation Gateway) translates private IP addresses from instances in a private subnet to a public IP address, enabling outbound internet connectivity.

| NAT Gateway     | Application Gateway     |
|--------------|--------------|
| Translates private IP addresses from instances in a private subnet to a public IP address, enabling outbound internet connectivity. | Web traffic load balancer work on Application Layer (Layer 7) and route traffic based on source ip address and port to   destionantion ip and port|
| ![image](https://github.com/user-attachments/assets/1d0901c8-f103-498f-a6bc-adbd2f57c96e) |![image](https://github.com/user-attachments/assets/388865c0-b4f6-4fb7-902a-8ce165e4f6f6) |
### Run the application
> To run a 3-tier-application, follow [Run Application](https://github.com/Sruthi-22012002/DevOps-Azure/tree/main/3-tier-application)

Check once if the backend properly stored the data in database.
![image](https://github.com/user-attachments/assets/e4e51e34-fb9f-4424-a522-0eb0f562a00b)

![image](https://github.com/user-attachments/assets/e86d8539-48e1-47e9-9713-9fc6a7bfa8de)






