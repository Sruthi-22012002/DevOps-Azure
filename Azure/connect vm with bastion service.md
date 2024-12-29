<div align="center"><h2>Conenct Web Tier VM to SSH Via Bastion Service</h2></div>

## Architecture Diagram

![image](https://github.com/user-attachments/assets/7f4563ed-a96a-44cc-9c1d-9422359a999a)

To connect Web-tier VM with SSH via <b>Bastion Service</b>

### Login Azure portal
### Create Resource group
Follow these steps to create Resource group :[Resource Group](https://github.com/Sruthi-22012002/DevOps-Azure/blob/main/Azure/connect%20VM%20to%20ssh.md)

![image](https://github.com/user-attachments/assets/92b02129-84f0-41a4-8dae-8d4ef575203b)

### Create Bastion
* Search for Bastion
* Create a new bastion <u>+ Create</u>

![image](https://github.com/user-attachments/assets/c71c0db0-39bb-4a82-b7c1-b2b616800c61)

#### Basics
##### Project details
* Choose Resource group
##### Instance details
* Enter name
* Choose Region , default East US
* Choose Availability zone
* Choose Tier <b>Basic</b>
##### Configure virtual networks
* Create Virtual network as new.

  ![image](https://github.com/user-attachments/assets/ea5e6ceb-c805-4673-a3e6-714e7083efcc)

* Enter Virtual network name
###### Address space
* Enter new address
###### Subnet
* Enter subnet name as <b>AzureBastionSubnet</b>
* calculate the subnet in Visual subnet calculator
📌 Address Range must be /26 or above /26
* click add
* Click Review + Create
### Create Virtual network
Follow steps to create Vnet :[Vnet](https://github.com/Sruthi-22012002/DevOps-Azure/blob/main/Azure/connect%20VM%20to%20ssh.md)

### Create Vm
> A Virtual Machine (VM) is a software-based emulation of a physical computer. It runs an operating system (OS) and applications just like a physical machine but is completely isolated and operates within a host environment.

* search for virtual machine
* Click <a href="#" style="display: inline-block; padding: 10px 20px; font-size: 14px; color: white; background-color: gray; text-align: center; text-decoration: none; border-radius: 5px;">+ Create</a>
![image](https://github.com/user-attachments/assets/3809fa94-0b39-4e39-bd63-f2b46138b758)

* Choose "Azure virtual machine"
![image](https://github.com/user-attachments/assets/b6be1131-a7ad-47d5-9179-461e83986982)

#### Basics
##### Project Details
* Chhose Resource group
##### Instance details
* Enter Virtual machine name
* Choose Region
* Choose iamge "Ubuntu Server 24.04 LTS - x64 Gen2(free services eligible)"
* Choose free size
##### Administrator account
* Choose authentication type
    * Authentication type
        * SSH Public Key
          ![image](https://github.com/user-attachments/assets/3e91572f-5cd8-438d-93cd-531494be42e6)
        * Enter user name
        * SSH public key source : Generate new key pair
        * SSH Key Type : RSA SSH Format / Ed25519 SSH Format
        * Enter key pair name
#### Networking
![image](https://github.com/user-attachments/assets/8618a620-19ed-4fc6-9fac-99484ad29988)

📌 If you choose you vnet once, it will take the public ip automatically.
* Finally Review + Create
* Download the private key
#### Review + Create

### Connect VM via Bastion Service to SSH
* Click the web-tier VM
![image](https://github.com/user-attachments/assets/70a7c28f-5eb1-48ca-b7c3-41d2421fa847)

* Select <u>+ Connect</u>
* Choose <b>Connect with Bastion</b>

![image](https://github.com/user-attachments/assets/66697994-369f-46b6-b4d2-03ebc1855faa)

* Choose Authentication Type as <b>"VM Password"</b>
* Enter Username of the VM
* Enter the password
* Click Connect
![bastion to ssh](https://github.com/user-attachments/assets/93af909d-3c87-493f-b266-2cb95cab1dd1)




