
# ✅ AWS EC2 (Elastic Compute Cloud): 
---
# 🔷 What is EC2?
**EC2 (Elastic Compute Cloud)** is a **virtual server** in AWS that lets you **run applications on the cloud**. It provides **resizable compute capacity** and allows you to **launch, manage, and terminate servers (instances)** on demand.

> 💡 Think of EC2 as a virtual computer in the cloud.

---
## 🔷 Why is EC2 Important?
* No need to buy physical servers
* Highly scalable & flexible
* Supports automation (with scripts, AMIs, Auto Scaling)
* Pay-as-you-go (billed per second or hour)
---
## 🔷 Key EC2 Concepts
------------------------------------------------------------------------------------------------------------------
| Component                       | Description                                                                  |
| ------------------------------- | ---------------------------------------------------------------------------- |
| **AMI**                         | Amazon Machine Image – template used to launch EC2 instances (OS + software) |
| **Instance Type**               | Defines hardware (CPU, RAM, storage) — e.g., `t2.micro`, `m5.large`          |
| **EBS**                         | Elastic Block Store — provides persistent storage for EC2                    |
| **Key Pair**                    | Used for secure SSH access to instances                                      |
| **Security Group**              | Acts like a virtual firewall to control traffic                              |
| **Elastic IP**                  | A static public IP address for EC2                                           |
| **User Data**                   | Script executed at instance launch (e.g., install packages)                  |
| **Elastic Load Balancer (ELB)** | Distributes traffic across multiple EC2 instances                            |
------------------------------------------------------------------------------------------------------------------
---

## 🔷 EC2 Lifecycle: End-to-End Steps:
--------------------------------------
### ✅ Step 1: Choose AMI

* Select an **Amazon Machine Image** (e.g., Amazon Linux, Ubuntu, Windows).
* AMI includes OS + preinstalled software.

### ✅ Step 2: Choose Instance Type

* Select based on required resources (e.g., `t2.micro` for free tier).
* Instance types vary by CPU, memory, and network performance.

### ✅ Step 3: Configure Instance Details

* Number of instances
* Network settings (VPC, subnet)
* IAM role (optional)
* Add bootstrap scripts in **User Data** (e.g., install Apache automatically)

### ✅ Step 4: Add Storage

* Choose root volume (EBS) size
* Optionally add additional volumes

### ✅ Step 5: Add Tags

* Add tags like `Name: MyServer` for easy management

### ✅ Step 6: Configure Security Group

* Define inbound/outbound rules (e.g., allow SSH on port 22, HTTP on port 80)

### ✅ Step 7: Review and Launch

* Select or create a **Key Pair** (used for SSH login)
* Launch the instance

---

## 🔷 After Launch: What Can You Do?
---------------------------------------------------------------------------------
| Task                     | Description                                         |
| ------------------------ | --------------------------------------------------- |
| **Connect via SSH**      | Use private key to log in to Linux EC2              |
| **Install Software**     | Use `yum`, `apt`, or run scripts                    |
| **Host Websites**        | Set up Apache/Nginx + DNS + domain                  |
| **Monitor Usage**        | Use **CloudWatch** to track CPU, memory, etc.       |
| **Auto Scaling**         | Automatically increase/decrease instances           |
| **Create AMI**           | Save your setup as a custom AMI for reuse           |
| **Stop/Start/Terminate** | Manage lifecycle and billing                        |
| **Attach Elastic IP**    | To make instance accessible with a public static IP |
---------------------------------------------------------------------------------
---

## 🔷 EC2 Pricing Options
---------------------------------------------------------------------------------------
| Option                 | Description                                                |
| ---------------------- | ---------------------------------------------------------- |
| **On-Demand**          | Pay per second/hour — no commitment                        |
| **Reserved Instances** | Commit to 1–3 years — big discount                         |
| **Spot Instances**     | Bid for unused capacity — cheapest but not always reliable |
| **Savings Plans**      | Flexible pricing model — cheaper over time                 |
--------------------------------------------------------------------------------------
---

## 🔷 Best Practices

* Use **IAM Roles** for secure access to other AWS services
* Always use **Security Groups** with least privilege
* Regularly **create AMIs** and **backups**
* Use **Auto Scaling + Load Balancers** for high availability
* Enable **CloudWatch Alarms** for monitoring and alerts

---

## ✅ Summary

* **EC2 = Virtual Server in AWS**
* You choose OS, CPU, storage, and network settings
* Easily scalable, highly customizable, pay-as-you-go
* Integrates with **S3**, **RDS**, **Load Balancer**, **IAM**, **CloudWatch**, etc.

---
#  Launching an EC2 Instance
1. **Choose an AMI:** Select an OS and software stack.
2. **Pick Instance Type:** Match hardware specs to your workload.
3. **Configure Instance:** Set network, IAM role, and advanced options.
4. **Add Storage:** Attach EBS volumes for persistent data.
5. **Set Security Group:** Specify inbound/outbound rules.
6. **Review & Launch:** Confirm settings and launch. Download the key pair for SSH.
---


