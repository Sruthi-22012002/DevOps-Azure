<div align="center"><h1>Domain Name Server</h1></div>

> DNS is an industry-standard protocol providing computer name-to-IP address mapping and name resolution services to computers and users. DNS is the default name resolution service used in Windows networks. DNS is part of the TCP/IP protocol suite and all TCP/IP network connections are by default configured with the IP address of at least one DNS server in order to perform name resolution on the network.

 ### DNS Architecture
![image](https://github.com/user-attachments/assets/99fd34df-b010-417f-bff1-3487f722903c)

### DNS record types
| Resource Record Type  | Description |
|----------------------|-------------|
| Host (A, AAAA) records | Maps a hostname to an IP address. |
| Alias (CNAME) records | Forwards an alias domain name or subdomain to another primary or canonical name. Allows multiple DNS names to point to a single host. |
| |Mail exchanger (MX) records | Specifies the name of a computer that exchanges or forwards mail. Used to locate mail servers based on a DNS domain name. Preference values determine mail server priority. |
| Pointer (PTR) records | Used for reverse DNS lookups to map an IP address to a domain name. Requires a reverse lookup zone on the DNS server. |
| Service location (SRV) records | Specifies the host, port, and protocol for a service. Commonly used for Active Directory domain controllers. |
| Name server (NS) records | Specifies the authoritative name servers for a domain. |
| Text (TXT) records | Enables the publication of text in a DNS record. Often used for domain ownership verification and email authentication. |
| Delegation name (DNAME) records | Provides an alias for a domain, like a CNAME record, but includes all subdomains. |
| Start of authority (SOA) records | Provides authoritative information about a DNS zone, including primary name server, administrator contact, and refresh settings. |

### Time to Live(TTL)
> Time to Live (TTL) is a number in a DNS record that specifies how long a DNS server can cache a record. It's like an expiration date for a DNS record.

![image](https://github.com/user-attachments/assets/db6cff89-123f-455f-9851-c503c3852380)

### Demo work
> Search for **"DNS Zones"** in azure portal

<h4>A DNS zone is used to host the DNS records for a particular domain. For example, the domain 'contoso.com' may contain a number of DNS records such as 'mail.contoso.com' (for a mail server) and 'www.contoso.com' (for a web site). Azure DNS allows you to host your DNS zone and manage your DNS records, and provides name servers that will respond to DNS queries from end users with the DNS records that you create. </h4>

![image](https://github.com/user-attachments/assets/120b2829-9908-445b-84d1-a977f77f2156)

> Click <a href="#" style="display: inline-block; padding: 10px 20px; font-size: 14px; color: white; background-color: gray; text-align: center; text-decoration: none; border-radius: 5px;">+ Create</a>

![image](https://github.com/user-attachments/assets/5dfd7d51-6f19-4a5d-8663-294d1ebd0b8b)

> Choose the **resource group**

> Enter the name for the service

> click Review + Create

<h3>open the DNS which was created </h3>

> Click recordsets under **"DNS Management"**

<h5>A record set is a collection of records in a zone that have the same name and are the same type. You can search for record sets that have been loaded on this page. If you don’t see what you’re looking for, you can try scrolling to allow more record sets to load.</h5>
 
![image](https://github.com/user-attachments/assets/658e18eb-769a-4505-bdb2-f7aaa13d8f8d)

> Register the NS values in DNS providers (e.g., GoDaddy, Cloudflare, Namecheap).

> Enter the new recordsets with your ip address,

![image](https://github.com/user-attachments/assets/69d541cc-408a-4ebc-9433-a67b113a09ae)

> Enter name and IP address and click "add"

**Access your domain with sub domain name http://frontend.react.dreamteamit.in/**



