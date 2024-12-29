![image](https://github.com/user-attachments/assets/7ccb0636-fd6a-43cf-a318-4ecf8733b2fe)<div align = "center"><h1>Connect vm to ssh server</h1></div>

## Architecture Diagram
![image](https://github.com/user-attachments/assets/471af189-6145-4dca-bff4-ab461786d649)


### Create resource group
1. Login to the azure account
2. Search for Resource group
3. Click <a href="#" style="display: inline-block; padding: 10px 20px; font-size: 14px; color: white; background-color: gray; text-align: center; text-decoration: none; border-radius: 5px;">+ Create</a>

![image](https://github.com/user-attachments/assets/c5901596-6696-473d-9e60-6412004e0f04)

4. > Under Project Details
     * Subscription : Free trail
     ❗ If payment was authorized, Free trail subscription will be added automatically
     * Enter resource group name

   > Under Resources Details
      * Leave region as it is.
5. Review + Create
![image](https://github.com/user-attachments/assets/93b4dd87-1298-410d-8bba-d6adb6fc4435)

### Create Vnet
> It is a cloud-based network that allows users to securely communicate between Azure resources, the internet, and on-premises networks. 

1. Search for Virtual networks 
2. Click <a href="#" style="display: inline-block; padding: 10px 20px; font-size: 14px; color: white; background-color: gray; text-align: center; text-decoration: none; border-radius: 5px;">+ Create</a>
![image](https://github.com/user-attachments/assets/3ac65cca-2411-48f3-8e07-8681398b00e6)

#### Basics
* Project Details
   * choose resource group
* Instance Details
    * Enter virtual machine name
#### IP Address
* Deafult address is already present.
    * If you want to add your IP, You can.
* If you want to add a subnet, Click <a href="#" style="display: inline-block; padding: 10px 20px; font-size: 14px; color: white; background-color: gray; text-align: center; text-decoration: none; border-radius: 5px;">+ Add Subnet</a>
![image](https://github.com/user-attachments/assets/c5b462d9-e265-4cac-8b36-17f8158f2333)

* Add the name of the subnet
* ##### IPv4
* For calculating the IP, Use Visual subnet calculator [Visual Subnet Calculator](https://www.davidc.net/sites/default/subnets/subnets.html)
  ![image](https://github.com/user-attachments/assets/55528da2-4f64-47f1-a5ba-a2f6d91a4a00)

    * Include an IPv4 address space "tick the checkbox"
    * IPv4 address range ,i.e. 10.0.0.0/16
    * Enter the starting range of IP address
    * choose the size of the IP
* Click add
3. Review + Create
### Create Virtual machine
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
![image](https://github.com/user-attachments/assets/83432818-cdb5-41da-85b7-927714215947)

* Finally Review + Create
* Download the private key
  > After successful deployment,
![image](https://github.com/user-attachments/assets/f928d778-8280-4f18-b73b-0b92369e6f0f)

### Open VScode 
* Move the path to .pem file
```bash
  /mnt/c/Users/Sreem/Downloads$ cp /mnt/c/Users/Sreem/Downloads/public-1.pem /home/sruthi/
```
* Login to vm with ssh keypair
```bash
  ssh -i public-1.pem Sruthi@135.237.147.75
```
  * keypair file
  * username
  * publickey of vm
#### Logged in
![image](https://github.com/user-attachments/assets/5b52ca4e-034d-43e4-a8d6-6b9d177f45ce)


