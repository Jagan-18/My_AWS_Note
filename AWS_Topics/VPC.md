<img width="859" height="398" alt="image" src="https://github.com/user-attachments/assets/c8d07c6c-379e-41fc-b582-2956c0044b6d" /># AWS VPC
---------
## 🔵 What is a VPC (Virtual Private Cloud)?
1. A virtual private cloud is a virtual network that closely resembles a traditional networking that you operate in your own data centre, with the benefits of using the scalable infrastructure of AWS.
2. VPC is a virtual network of data center inside AWS for one client.
3. It is logically isolated from other virtual network in the AWS cloud.
4. Maximum 5 VPC can be created in one region and 200 subnets in 1 VPC.
5. We can allocate maximum 5 Elastic IP. Once we created VPC, DHCP, NACL and security group will automatically created.
6. A VPC is confined to an AWS region and does not extend between regions.
7. Once the VPC is created you cannot change its CIDR block range.
8. If you need a different CIDR size create a new VPC.
9. The different subnets within a VPC cannot overlap.
<img width="513" height="540" alt="Image" src="https://github.com/user-attachments/assets/7e9f2745-3da1-4b4e-a468-065d1f2a20b9" />

### Using VPC, you can define:
* IP address ranges (using **CIDR** blocks)
* Subnets (public & private)
* Route tables
* Gateways (Internet, NAT, VPN)
* Security rules
---
# Types of VPC
1. Default VPC:
    * 	Created in each AWS region when an AWS account is created.
    * Has default CIDR, security group, NACL and route table settings. It an internet gateway by default.
2. Custom VPC:
    * It is a VPC and AWS account owner creates.
    * AWS user creating the Custom VPC can decide the CIDR.
    * It has its own default security group, NACL and route tables.
	* It doesn’t have an internet gateway by default, one needs to be created if needed.

# Components of VPC:
1. CIDR and IP address subnets
2. Implied Router and Routing table
3. Internet Gateway
4. Security Group
5. NACL
6. Virtual Private Gateway
7. Peering Connectors
8. Elastic IP
<img width="859" height="398" alt="Image" src="https://github.com/user-attachments/assets/bf64fe21-bfbd-4622-a8fb-da7bacfd3ffe" />
<img width="998" height="423" alt="Image" src="https://github.com/user-attachments/assets/3ca0205b-7d24-4c35-8993-300da7bdfbfe" />
<img width="648" height="691" alt="Image" src="https://github.com/user-attachments/assets/0a697f3a-5e2d-44da-abbf-061b8d0c3113" />

---
## 🔸 Why is VPC Important?
| Benefit                   | Description                                                          |
| ------------------------- | -------------------------------------------------------------------- |
| **Security**              | Total control over inbound and outbound traffic                      |
| **Isolation**             | Resources in your VPC are isolated from others                       |
| **Customizable**          | Define your own subnets, IP ranges, and routing rules                |
| **Scalable & Elastic**    | Expand VPCs, add NAT, VPN, gateways, more subnets as needed          |
| **Supports Hybrid Cloud** | Use AWS Direct Connect or VPN to integrate with on-prem data centers |
---

## 🔹 Key Components of a VPC
| Component                  | Purpose                                                             |
| -------------------------- | ------------------------------------------------------------------- |
| **CIDR Block**             | IP range of the VPC (e.g., 10.0.0.0/16)                             |
| **Subnets**                | Logical divisions of VPC — can be **Public** or **Private**         |
| **Route Tables**           | Define routing rules for subnets                                    |
| **Internet Gateway (IGW)** | Enables access to internet for public subnets                       |
| **NAT Gateway**            | Allows private subnets to access the internet (outbound only)       |
| **Security Groups**        | Instance-level firewall                                             |
| **Network ACLs**           | Subnet-level firewall rules                                         |
| **Elastic IPs**            | Static public IPv4 addresses                                        |
| **VPC Endpoints**          | Connect privately to AWS services without using the public internet |

---
#### CIDR – Classless Inter Domain Routing.

# What is CIDR? - All IP address is private only.
> **Classless Inter-Domain Routing (CIDR) is an IP address allocation method that improves data routing efficiency on the internet. Every machine, server, and end-user device that connects to the internet has a unique number, called an IP address, associated with it**. Devices find and communicate with one another by using these IP addresses. Organizations use CIDR to allocate IP addresses flexibly and efficiently in their networks.
<img width="750" height="488" alt="Image" src="https://github.com/user-attachments/assets/d40516f5-a47f-4efa-843a-568aea67b60e" />
---

# IP- Address:
You can assign IP addresses, both IPv4 and IPv6, to your VPCs and subnets. You can also bring your public IPv4 and IPv6 GUA addresses to AWS and allocate them to resources in your VPC, such as EC2 instances, NAT gateways, and Network Load Balancers.

<img>

### What is IP?
 > IP stands for Internet Protocol, a set of rules governing how devices on a network communicate with one another.

### What is IPv4?
 > IPv4, or Internet Protocol version 4, is a version of the Internet Protocol (IP) that uses a number identifier to identify devices on a network. IPv4 addresses are 32-bit IP addresses written in decimal notation.

### What is IPv6?
> IP version 6 is the new version of Internet Protocol, which is way better than IP version 4 in terms of complexity and efficiency. IPv6 is written as a group of 8 hexadecimal numbers separated by colon (:). It can be written as 128 bits of 0s and 1s.

---

# Sub-Net:
A subnet is a range of IP addresses in your VPC. A subnet must reside in a single Availability Zone. After you add subnets, you can deploy AWS resources in your VPC.
<img>
---

## 🧱 Public vs Private Subnet:
------------------------------
| Type        | Description                                                                                                                         |
| ----------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| **Public**  | Subnet associated with a route to an Internet Gateway (IGW). Resources (like EC2) in this subnet can be accessed from the internet. |
| **Private** | No direct route to IGW. Used for backend servers, databases, internal services. Can go outbound using NAT Gateway.                  |

# Public Subnet:
- **If a subnet’s traffic is routed to an internet gateway, the subnet is known as public subnet.** If you want your instance in a public subnet to communicate with the internet over IPV4, it must have a public IPV4 address or an Elastic IP address.
 
# Private Subnet: 
- **If a subnet doesn’t have a route to the internet gateway, the subnet is known as private subnet.** When you create a VPC you must specify an IPV4 CIDR block for the VPC. The allowed blocks size is between /16 to /28 networks. The first four and last IP address of subnet cannot be assigned.

- The instances in the public subnet can send outbound traffic directly to the internet, but instances in private subnet can’t.

**For e.g: 10.0.0.0- network address:**
•  10.0.0.1- reserved by AWS for the VPC router.
•  10.0.0.2- reserved by AWS the IP address of DNS server.
•  10.0.0.3- reserved for future use.
•  10.0.0.255- broadcast address

# Note: AWS do not support broadcast in a VPC but reserve this address.
---
# Routing and Routing Table:
1. Use route tables to determine where network traffic from your subnet or gateway is directed.

2.A Route table contains a set of rules, called routes, that are used to determine where the data packets of the network traffic are directed. 
  • It is the central routing function.
  •	It connects the different AZ together and connects the VPC to the internet gateway.
  •	You can have up to 200 route tables per VPC.
  •	You can have up to 50 routes entries per route table.
  • Each subnet must be associated with only one route table at any given time only.
  •	If you don’t specify a subnet to route table association, the subnet will be associated with the default VPC route table.
  •	You can also edit the main route table if you need but you cannot delete the main route table.

---
# Internet Gateway: ----> It will give public access and internet.
<img>

1. An internet Gateway (IGW) is a logical connection between an Amazon VPC and the internet. It is not a physical device. Only one can be associated with each VPC. It does not limit the bandwidth of internet connectivity.
2. Ensure that your subnet’s route table points to the internet gateway.
3. It performs NAT between your private and public IPV4 address.
4. It supports both IPV4 and IPV6.
---

# NAT Gateway:
NAT Gateway is a highly available AWS managed service that makes it easy to connect to the Internet from instances within a private subnet in an Amazon Virtual Private Cloud (Amazon VPC). Previously, you needed to launch a NAT instance to enable NAT for instances in a private subnet.

               **(OR)**

NAT Gateway service can use a NAT gateway so that instances in a private subnet can connect to services outside your VPC, but external services cannot initiate a connection with those instances.
    • No need to assign public IP address to your private instance.
	• After you have created a NAT gateway you must update the route table associated with one or more of your private subnets to point internet bound traffic to the NAT gateway.This enables instances in your private subnet to communicate with the internet.
	• Deleting a NAT gateway, disassociates its elastic IP address, but does not release the address from your account.

- **Security group** is the firewall of EC2 Instances.
- **Network ACL** is the firewall of the VPC Subnets.
---

# Security group:
A security group acts as a virtual firewall for your EC2 instances to control incoming and outgoing traffic. Both inbound and outbound rules control the flow of traffic to and traffic from your instance, respectively, Security groups allow you to define rules that permit or restrict traffic based on protocols, ports, and IP addresses.  
   • It is a virtual firewall works at ENI level.
   • Up to 5 security groups per EC2 instance interface can be applied.
   • Can only have permit rules, cannot have deny rules.
   • Stateful, return traffic of allowed inbound traffic is allowed even if there are no rules to allow it.

---
# Network Access Control Lists (NACLs):
1.	It is a function performed on the implied router.
2.	NACL is an optional layer of security for your VPC that acts as a firewall for controlling traffic in and out of one or more subnets.
3.	Your VPC automatically comes with a modifiable default NACL. By default, it allows all inbound and outbound IPV4 traffic and if applicable IPV6 traffic.
4.	You can create a custom NACL and associate it with a subnet. By default, each NACL denies all inbound and outbound traffic until you add rules.
5.	Each subnet in your VPC must be associated with a NACL. If you don’t explicitly associate a subnet with a NACL, the Subnet is automatically associated with the default NACL.
6.	It functions at the subnet level. NACL are stateless, outbound traffic for an allowed inbound traffic must be explicitly allowed too. 
7.	You can have permit and deny rules in a NACL.
---
## 🔐 Difference Between Security Group and NACL

| Security Group                                         | NACL (Network Access Control List)                           |
|--------------------------------------------------------|--------------------------------------------------------------|
|1. Operates at the **instance** level                   | 1. Operates at the **subnet** level                          |
|2. Supports **allow** rules only                        | 2. Supports **allow** and **deny** rules                     |
|3. **Stateful**–return traffic is allowed automatically | 3. **Stateless** – return traffic must be explicitly allowed |
|4. Applies to **individual instances**                  | 4. Applies to **all instances** in the subnet                |
---
# VPC Peering: 
1.	A VPC peering connection is a network connection between two VPC that enables you to route traffic between them using private IPV4 addresses or IPV6 addresses. 
2.	Instances in either VPC can communicate with each other as if they are within the same network. 
3.	You can create a VPC peering connection between your own VPC or with a VPC in another AWS account. The VPC can be in different region.

<img>
---
# VPC Endpoint:
> A VPC endpoint enables you to privately connect your VPC to supported AWS services, instances in your VPC do not require public IP address to communicate with resources in the service. Endpoints are virtual devices.

**OR**
> These allow private connections between your VPC and supported AWS services, reducing the need to send traffic over the internet.
---
#### What is VPC peering connection?
> 1. Requester
> 2.Acesspter.
#### Can we do VPC Peering b/w VPC which are in different Regions?
**We can do this:**
1. same Account same region.
2. same account different region
3. Diff Account same region
4. different account different region  
---
#### VPC Flow Logs
> A flow log captures information about the IP traffic going to and from network interfaces in your VPC.
---
#### Traffic Mirroring
> Copy network traffic from network interfaces and send it to security and monitoring appliances for deep packet inspection.
---
#### Transit gateways
>  Use a transit gateway, which acts as a central hub, to route traffic between your VPCs, VPN connections, and AWS Direct Connect connections.
---
### VPN connections
> Connect your VPCs to your on-premises networks using AWS Virtual Private Network (AWS VPN).
---
#### Elastic IP address
> It is a static public IPv4 address associated with your AWS account in a specific region. Unlike an auto-assigned public IP address, an Elastic IP address is preserved after you stop and start your instance in a virtual private cloud (VPC).

---
## 🖼️ Diagram: Basic VPC Architecture

```
                          AWS VPC (10.0.0.0/16)
                                    |
                          ┌──────────────────────┐
                          │                      │
          ┌───────────────┴──────────────┐ ┌─────┴───────────────┐
 Public Subnet (10.0.1.0/24)         Private Subnet (10.0.2.0/24)
     - EC2 with Public IP               - EC2 without Public IP
     - Internet Gateway                 - NAT Gateway (for outbound)
          │                                   │
     (Accessible from Web)             (Internal only, secure)
                          │
                          └── Route Tables control traffic flow
```

---

## 🧪 Real-world Use Case:
--------------------------
### Scenario: Hosting a Secure Web Application

1. **Frontend** (React app, Nginx) is deployed in a **Public Subnet** with a public IP.
2. **Backend API** (Node.js, Java, etc.) is hosted in a **Private Subnet**.
3. **Database** (RDS, MongoDB, etc.) lives in the **Private Subnet** with no internet access.
4. A **NAT Gateway** in the Public Subnet allows backend/API servers to pull updates from the internet.
5. **Security Groups** and **NACLs** restrict traffic to allow only necessary communication.

✅ This setup ensures high security and separation of concerns.

---
## 🛠️ Steps to Create a Custom VPC from AWS Console:
--------------------------------------------------
### Step-by-Step Guide:
1. **Login to AWS Console** → Go to **VPC Dashboard**
2. Click **"Create VPC"**

   * Name: `MyVPC`
   * IPv4 CIDR block: `10.0.0.0/16`
   * Leave default for others

3. Create 2 Subnets:

   * `PublicSubnet` → `10.0.1.0/24`
   * `PrivateSubnet` → `10.0.2.0/24`

4. **Create Internet Gateway (IGW)**:

   * Attach IGW to your VPC

5. **Create Route Table for Public Subnet**:

   * Add route: `0.0.0.0/0` → IGW
   * Associate this route table with `PublicSubnet`

6. **Create NAT Gateway (Optional for private subnet)**:

   * Place it in the `PublicSubnet`
   * Allocate an Elastic IP
   * Attach it to a route table for the `PrivateSubnet`

7. **Launch EC2 Instances**:

   * In PublicSubnet (with public IP)
   * In PrivateSubnet (no public IP)

8. **Set Security Groups**:

   * Allow SSH (port 22) or HTTP/HTTPS for public EC2
   * Restrict private EC2 to allow only internal traffic
---
## ✅ Summary:
* **VPC** is your own secure cloud network.
* You can split your VPC into **public and private subnets** for isolation and security.
* Use **Internet Gateway** and **NAT Gateway** for controlled internet access.
* Everything is **customizable**: IPs, routing, firewall rules, and connections.

---
# Name and explain some security products and features available in VPC?
1. **Security groups** - This goes about as a firewall for the EC2 examples, controlling inbound and outbound traffic at the case level.
2. **Network access control lists** - It goes about as a firewall for the subnets, controlling inbound and outbound traffic at the subnet level.
3. **Flow logs** - These catch the inbound and outbound traffic from the system interfaces in your VPC.
---
# How do you monitor Amazon VPC?
You can use the following tools to monitor traffic or network access in your virtual private cloud (VPC).
 1. VPC Flow Logs - You can use VPC Flow Logs to capture detailed information about the traffic going to and from network interfaces in your VPCs.
 2. Amazon VPC IP Address Manager (IPAM) - You can use IPAM to plan, track, and monitor IP addresses for your workloads. For more information, see IP Address Manager.
 3. Traffic Mirroring
 4. Reachability Analyzer
 5. Network Access Analyzer
 6. CloudTrail logs


