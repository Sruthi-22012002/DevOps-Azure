<div align="center"><h2>Azure Database for MySQL Flexible Server</h2></div>

> Azure Database for MySQL is a managed service for running, managing, and scaling highly available MySQL servers in the cloud. This article shows you how to use the Azure portal to create an Azure Database for MySQL Flexible Server instance.

## Create an Azure Database for MySQL Flexible Server

* Create the server within an Azure resource group.

* Complete these steps to create an Azure Database for MySQL Flexible Server:

* In the Azure portal, search for and then select Azure Database for MySQL Flexible Servers.

![image](https://github.com/user-attachments/assets/8a747d81-60e9-41d2-9d06-2d4ddedbaabf)

* Select Create.

* On the Select **Azure Database for MySQL deployment** option pane, select Flexible server as the deployment option:

![image](https://github.com/user-attachments/assets/42e01804-9a2f-4fb8-862b-89e8842b62cc)

* On the **Basics** tab, enter or select the following information:

    <table border="1">
    <tr>
    <th>Setting</th>
    <th>Suggested Value</th>
    <th>Description</th>
    </tr>
    <tr>
    <td>Subscription</td>
    <td>Your subscription name</td>
    <td>The Azure subscription you want to use for your server. Choose the subscription for which you want to be billed for the resource if you have multiple subscriptions.</td>
    </tr>
    <tr>
    <td>Resource group</td>
    <td>myresourcegroup</td>
    <td>Create a new resource group name, or select an existing resource group from your subscription.</td>
    </tr>
    <tr>
    <td>Server name</td>
    <td>mydemoserver-quickstart</td>
    <td>A unique name that identifies your instance of Azure Database for MySQL - Flexible Server. The domain name mysql.database.azure.com is appended to the server name you enter. The server name can contain only lowercase letters, numbers, and the hyphen (-) character. It must contain between 3 and 63 characters.</td>
    </tr>
    <tr>
    <td>Region</td>
    <td>The region closest to your users</td>
    <td>The location closest to your users.</td>
    </tr>
    <tr>
    <td>MySQL version</td>
    <td>8.0</td>
    <td>The major engine version.</td>
    </tr>
    <tr>
    <td>Workload type</td>
    <td>Development</td>
    <td>For production workload, you can select Small/Medium-size or Large-size depending on max_connections requirements.</td>
    </tr>
    <tr>
    <td>Compute + storage</td>
    <td>Burstable, Standard_B1ms, 10 GiB, 100 iops, 7 days</td>
    <td>The compute, storage, input/output operations per second (IOPS), and backup configurations for your new server. On the Configure server pane, the default values for Compute tier, Compute size, Storage size, IOPS, and Retention period (for backup) are Burstable, Standard_B1ms, 10 GiB, 100 IOPS, and 7 days. You can keep the default values or modify these values. For faster data loads during migration, we recommend increasing IOPS to the maximum size supported for the compute size you selected. Later, scale it back to minimize cost. To save the compute and storage selection, select Save to continue with the configuration.</td>
    </tr>
    <tr>
    <td>Availability zone</td>
    <td>No preference</td>
    <td>If your application client is provisioned in a specific availability zone, you can set your Azure Database for MySQL Flexible Server to the same availability zone to colocate the application and reduce network latency.</td>
    </tr>
    <tr>
    <td>High availability</td>
    <td>Cleared</td>
    <td>For production servers, choose between zone-redundant high availability and same-zone high availability. We recommend high availability for business continuity and protection against virtual machine (VM) failure.</td>
    </tr>
    <tr>
    <td>Authentication method</td>
    <td>MySQL and Microsoft Entra authentication</td>
    <td>Select the authentication methods you would like to support for accessing this MySQL server.</td>
    </tr>
    <tr>
    <td>Admin username</td>
    <td>mydemouser</td>
    <td>Your sign-in account is to be used when you connect to the server. The admin username can't be azure_superuser, admin, administrator, root, guest, sa, or public. The maximum number of characters that are allowed is 32.</td>
    </tr>
    <tr>
    <td>Password</td>
    <td>Your password</td>
    <td>A new password for the server admin account. It must contain between 8 and 128 characters. It also must contain characters from three of the following categories: English uppercase letters, English lowercase letters, numbers (0 through 9), and nonalphanumeric characters (!, $, #, %, and so on).</td>
    </tr>
    </table>

* Next, configure **networking** options.

* On the Networking tab, set how your server is accessed. Azure Database for MySQL - Flexible Server offers two ways to connect to your server:

    > Public access (allowed IP addresses)
    
    > Private access (virtual network integration)

![image](https://github.com/user-attachments/assets/f2b3dab2-1a9b-4521-ae80-25f284038a82)

* Select **Review + create** to review your Azure Database for MySQL Flexible Server configuration.

* Select **Create** to provision the server. Provisioning might take a few minutes.

