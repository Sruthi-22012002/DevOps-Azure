<div align="center"><h2>Virtual Machine Scale Sets</h2></div>

> A VMSS offers automatic scaling and performance optimization, infrastructure flexibility, and options to mix VM sizes, zones, and fault domains—all with simple, centralized group VM management. Already have VMs? Just create a new flexible VMSS, and attach existing VMs to your new scale set to get enhanced availability, resiliency, and capacity and cost optimization.Azure Virtual Machine Scale Sets let you create and manage a group of load balanced VMs. The number of VM instances can automatically increase or decrease in response to demand or a defined schedule

## Why VMSS ?
*  Automatic Scaling
*  High Availability & Fault Tolerance
*  Load Balancing
*  Container Orchestration & Microservices

## Orchestration modes

**Uniform orchestration** ensures consistency by using a predefined virtual machine profile to deploy identical instances within a scale set. While some customization of individual VMs is possible, Uniform orchestration primarily manages VMs as a group.

**Flexible orchestration** is that it provides orchestration features over standard Azure IaaS VMs, instead of scale set child virtual machines.

## Architecture of VMSS for 3-tier-application with load balancer
<img src="https://github.com/user-attachments/assets/69a8ddc5-2e7f-4fa1-85c2-c61a78b72ce3" alt="Description" width="500" height="500">

## Implementation of Application 

🔵 **Step 1 : Create resource group**

🔵 **Step 2 : Create Vnet**

🔵 **Step 3 : Create VMSS**

 #### 3️⃣.1️⃣ Create Frontend VMSS

* In the Azure portal search bar, search for and select Virtual Machine Scale Sets.

* Select Create on the Virtual Machine Scale Sets page.

* In the Basics tab, under Project details, make sure the correct subscription is selected and create a new resource group called myVMSSResourceGroup.

* Under Scale set details, set myScaleSet for your scale set name and select a Region that is close to your area.

* Under Orchestration, select Flexible.

* Under Instance details, select a marketplace image for Image. Select any of the Supported Distros.

* Under Administrator account configure the admin username and set up an associated password or SSH public key.

  > A Password must be at least 12 characters long and meet three out of the four following complexity requirements: one lower case character, one upper case character, one number, and one special character. For more information, see username and password requirements.
 
  > If you select a Linux OS disk image, you can instead choose SSH public key. You can use an existing key or create a new one. In this example, we will have Azure generate a new key pair for us. For more information on generating key pairs, see create and use SSH keys.

 ![image](https://github.com/user-attachments/assets/8eb04a2d-da34-46db-8906-77f690781448)

* Select Next: **Disks** to move the disk configuration options. For this quickstart, leave the default disk configurations.

* Select Next: **Networking** to move the networking configuration options.

* On the Networking page, under Load balancing, select the Use a load balancer checkbox to put the scale set instances behind a load balancer.

* In Load balancing options, select Azure load balancer.

* In Select a load balancer, select a load balancer or create a new one.

* For Select a backend pool, select Create new, type myBackendPool, then select Create.

![image](https://github.com/user-attachments/assets/9a7d4aa2-257b-4999-8122-1f55a90277a1)

* Select Next: **Scaling** to move to the scaling configurations.

* On the Scaling page, set the initial instance count field to 5. You can set this number up to 1000.

* For the Scaling policy, keep it Manual.

![image](https://github.com/user-attachments/assets/d8c5c435-d8f0-45eb-8006-c88cf4976c08)

* When you're done, select Review + create.
  
* After it passes validation, select Create to deploy the scale set.
