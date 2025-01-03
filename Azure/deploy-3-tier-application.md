<div align="center"><h2>Deploy 3-tier-application</h2></div>

### Requirements
1. Create a virtual network for the 3-tier application.
2. Set up three subnets for the frontend, backend, and database.
3. Create three virtual machines (VMs), one for each subnet, and configure a Network Security Group (NSG) for each subnet.
   > Ensure the following access and restrictions:

        * Frontend: Allow browser access from the public network. The frontend VM will act as the entry point or gateway.
        * Backend to Database: Restrict access from the public network.
        * Frontend to Backend: Allow SSH access. 
        * Backend to Database: Allow SSH access. 
   <b>Frontend to Database: Do not allow SSH access for security reasons.</b>  
### Architecture Diagram
![image](https://github.com/user-attachments/assets/ed98a300-6907-4509-acbd-27b02592ad83)

### NAT Gateway
> A NAT Gateway (Network Address Translation Gateway) is a service in cloud environments (such as AWS, Azure, or Google Cloud) that allows instances in a private subnet to connect to the internet while preventing inbound internet traffic from directly accessing those instances.
### Run the application
> To run a 3-tier-application, follow [Run Application](https://github.com/Sruthi-22012002/DevOps-Azure/tree/main/3-tier-application)

Check once if the backend properly stored the data in database.
![image](https://github.com/user-attachments/assets/e4e51e34-fb9f-4424-a522-0eb0f562a00b)

![image](https://github.com/user-attachments/assets/e86d8539-48e1-47e9-9713-9fc6a7bfa8de)






