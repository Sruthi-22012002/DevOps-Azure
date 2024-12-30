<div align="center"><h1>Connect Web Tier with SSH Via Bastion VM</h1></div>

## Bastion
> A bastion is a specialized server or resource designed to act as a gateway and provide secure access to a private network from an external network, such as the internet.

## Architecture Diagram
![image](https://github.com/user-attachments/assets/5e78b863-6f0b-4eee-ab19-0d020277ccc0)


### Login Azure portal
### Create Resource group
Follow these steps to create Resource group :[Resource Group](https://github.com/Sruthi-22012002/DevOps-Azure/blob/main/Azure/connect%20VM%20to%20ssh.md)

![image](https://github.com/user-attachments/assets/92b02129-84f0-41a4-8dae-8d4ef575203b)

### Create Virtual network
Follow steps to create Vnet :[Vnet](https://github.com/Sruthi-22012002/DevOps-Azure/blob/main/Azure/connect%20VM%20to%20ssh.md)
#### Create Vm for Bastion Host subnet
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

##### Create a virtual networks
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

📌 If you choose you vnet once, it will take the public ip automatically.
* Finally Review + Create
* Download the private key
#### Review + Create
### Create a VM for Web Tier
Follow the steps above.
### Connect with SSH
* Open terminal
* Establish a Connection <b>with bastion subnet</b>
```bash
 shh username@bastionpublicip
```
![image](https://github.com/user-attachments/assets/008f4b98-733b-4c48-b350-e0ae31f0c981)

* Establish a connect <b>Bastion to Web Tier</b>

 ```bash
  shh username@webtierprivateip
 ```

![image](https://github.com/user-attachments/assets/00cf7180-3d06-446f-b76d-ee54574e46aa)

> <h2>Succesfully connected</h2>

![image](https://github.com/user-attachments/assets/59145273-3a86-4b2f-ae41-8a68806bd683)

 

