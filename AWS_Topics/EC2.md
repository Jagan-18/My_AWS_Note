
# ✅ AWS EC2 (Elastic Compute Cloud): 
---
# 🔷 What is EC2?
**EC2 (Elastic Compute Cloud)** is a **virtual server** in AWS that lets you **run applications on the cloud**. It provides **resizable compute capacity** and allows you to **launch, manage, and terminate servers (instances)** on demand.

> 💡 Think of EC2 as a virtual computer in the cloud.

- Amazon Elastic Compute Cloud (Amazon EC2) is a web service that provides secure, resizable compute capacity in the cloud.
- Access reliable, scalable infrastructure on demand. Scale capacity within minutes with SLA commitment of 99.99% availability.
- Provide secure compute for your applications. Security is built into the foundation of Amazon EC2 with the AWS Nitro System.
- Optimize performance and cost with flexible options like AWS Graviton-based instances, Amazon EC2 Spot instances, and AWS Savings Plans.
---
## 🔷 Why is EC2 Important?
* No need to buy physical servers
* Highly scalable & flexible
* Supports automation (with scripts, AMIs, Auto Scaling)
* Pay-as-you-go (billed per second or hour)
---
## 🔷 Key EC2 Concepts
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

---
## 🔷 EC2 Pricing Options

| Option                 | Description                                                |
| ---------------------- | ---------------------------------------------------------- |
| **On-Demand**          | Pay per second/hour — no commitment                        |
| **Reserved Instances** | Commit to 1–3 years — big discount                         |
| **Spot Instances**     | Bid for unused capacity — cheapest but not always reliable |
| **Savings Plans**      | Flexible pricing model — cheaper over time                 |

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

# ✅ **EC2 Instance Types Explained (with Use Cases)**

Amazon EC2 offers **different instance types** to match various workloads. Each type is optimized for specific use cases like general purpose, compute-heavy tasks, memory-intensive applications, etc.

---
## 🔷 1. **General Purpose Instances**
- It is designed to deliver a balance of compute, memory, and network resources. They are suitable for a wide range of applications, including web servers, small databases, development and test environments, and more.

| Instance Family | Examples                 | Use Cases                            |
| --------------- | ------------------------ | ------------------------------------ |
| `t` (Burstable) | `t2.micro`, `t3.small`   | Web servers, Dev/Test, microservices |
| `m` (Balanced)  | `m5.large`, `m6i.xlarge` | Small/medium databases, app servers  |
---
## 🔷 2. **Compute Optimized Instances**
- It's provide a higher ratio of compute power to memory. They excel in workloads that require high-performance processing such as batch processing,  scientific modeling, gaming servers, and high-performance web servers.

| Instance Family | Examples                 | Use Cases                                                                           |
| --------------- | ------------------------ | ----------------------------------------------------------------------------------- |
| `c`             | `c5.large`, `c6g.xlarge` | High-performance web servers, gaming servers, batch processing, scientific modeling |

---
## 🔷 3. **Memory Optimized Instances**
- This are designed to handle memory-intensive workloads. They are suitable for applications that require large amounts of memory, such as in-memory databases, real-time big data analytics, and high-performance computing.

| Instance Family | Examples                 | Use Cases                                              |
| --------------- | ------------------------ | ------------------------------------------------------ |
| `r`             | `r5.large`, `r6i.xlarge` | In-memory databases (Redis, Memcached), big data       |
| `x`             | `x1e.8xlarge`            | SAP HANA, high-performance databases                   |
| `z`             | `z1d.large`              | Electronic design automation (EDA), financial modeling |

---
## 🔷 4. **Storage Optimized Instances**
- It are optimized for applications that require high, sequential read and write access to large datasets.  They are ideal for tasks like data warehousing, log processing, and distributed file systems.

| Instance Family | Examples     | Use Cases                                  |
| --------------- | ------------ | ------------------------------------------ |
| `i`             | `i3.large`   | NoSQL databases (Cassandra, MongoDB), OLTP |
| `d`             | `d2.xlarge`  | Data warehousing, Hadoop clusters          |
| `h`             | `h1.2xlarge` | High-density storage, file servers         |

---
## 🔷 5. **Accelerated Computing Instances**
- Accelerated Computing Instances typically come with one or more types of accelerators, such as Graphics Processing Units (GPUs), Field Programmable Gate Arrays (FPGAs), or custom Application Specific Integrated Circuits (ASICs). 
- These accelerators offload computationally intensive tasks from the main CPU, enabling faster and more efficient processing for specific workloads.

| Instance Family | Examples      | Use Cases                                       |
| --------------- | ------------- | ----------------------------------------------- |
| `p`             | `p3.2xlarge`  | Deep learning, training models                  |
| `g`             | `g4dn.xlarge` | Graphics, video processing, ML inference        |
| `f`             | `f1.2xlarge`  | Hardware acceleration using FPGA (custom logic) |

---
## 🔷 6. **High Performance / Specialized Instances**

| Instance Family | Use Case                                      |
| --------------- | --------------------------------------------- |
| `u`             | Ultra-high memory for SAP HANA workloads      |
| `inf`           | High throughput inference (machine learning)  |
| `metal`         | Bare metal access — direct access to hardware |

---
## 🧠 Tips to Choose the Right EC2 Type

* For **general web apps or small workloads** → `t3.micro`, `t3.small`, `m5.large`
* For **CPU-bound tasks** → `c6g.large`, `c5.xlarge`
* For **RAM-heavy workloads** → `r5.xlarge`, `x1e.large`
* For **fast local disk I/O** → `i3.large`, `d2.xlarge`
* For **AI/ML & GPU tasks** → `g4dn`, `p3`
---
## ✅ Summary Table

| Type              | Family        | Focus Area         | Example Use Cases                |
| ----------------- | ------------- | ------------------ | -------------------------------- |
| General Purpose   | `t`, `m`      | Balanced workloads | Web apps, Dev/Test               |
| Compute Optimized | `c`           | High CPU           | Gaming, ML inference, batch jobs |
| Memory Optimized  | `r`, `x`, `z` | High RAM           | In-memory DBs, SAP               |
| Storage Optimized | `i`, `d`, `h` | Fast local storage | Databases, data warehousing      |
| Accelerated Comp  | `p`, `g`, `f` | GPU/FPGA tasks     | Deep learning, rendering, AI     |

---
# ✅ **EC2 Instance Naming Convention (Explained)**
![image](https://github.com/iam-veeramalla/aws-devops-zero-to-hero/assets/43399466/fc8e083c-dba5-41a6-94b9-14ebef0255c1)

- Each EC2 instance type name (e.g., `c5n.xlarge`) is structured to convey the **family**, **generation**, **capabilities**, and **size**.

### 📌 Format:

```
<family><generation><additional capabilities>.<size>
```

---
## 🔷 1. **Instance Families**
These indicate the **main purpose or workload focus** of the instance:

| Code  | Family                             | Purpose                                                |
| ----- | ---------------------------------- | ------------------------------------------------------ |
| `C`   | Compute                            | High-performance CPU, compute-intensive tasks          |
| `D`   | Dense storage                      | High storage capacity (HDD-based)                      |
| `F`   | FPGA                               | Hardware acceleration via FPGAs                        |
| `G`   | GPU                                | Graphics or ML inference (GPU-based)                   |
| `Hpc` | High Performance Computing         | Ultra high-speed networking, tightly-coupled workloads |
| `I`   | I/O Optimized                      | High random I/O performance (NVMe SSDs)                |
| `Inf` | Inferentia                         | Machine learning inference (AWS chip)                  |
| `M`   | General Purpose ("Most use cases") | Balanced compute, memory, and networking               |
| `P`   | GPU                                | Deep learning training (GPU-heavy)                     |
| `R`   | Memory (RAM) Optimized             | For memory-intensive apps (databases, analytics)       |
| `T`   | Burstable / Turbo                  | Low-cost general purpose with burstable CPU            |
| `Trn` | Tranium                            | AWS custom chip for ML training                        |
| `U`   | Ultra-high memory                  | For SAP HANA and massive in-memory DBs                 |
| `VT`  | Video Transcoding                  | Optimized for video encoding                           |
| `X`   | Extra-large memory                 | In-memory workloads requiring huge RAM                 |
---
## 🔷 2. **Additional Capabilities (Optional Suffix Letters)**
These give more detail about the **underlying hardware or performance enhancements**:
| Code | Meaning                         | Explanation                                     |
| ---- | ------------------------------- | ----------------------------------------------- |
| `a`  | AMD processor                   | Uses AMD EPYC CPU                               |
| `g`  | AWS Graviton processor          | Uses AWS’s ARM-based Graviton CPUs              |
| `i`  | Intel processor                 | Uses Intel Xeon CPUs                            |
| `d`  | Includes instance store volumes | Has local NVMe or SSD disks (ephemeral storage) |
| `n`  | Network and EBS optimized       | High network bandwidth & EBS throughput         |
| `e`  | Extra storage or memory         | Enhanced EBS or RAM                             |
| `z`  | High performance                | High-frequency CPU cores (GHz boost)            |
---
## 🔷 3. **Instance Generation**
* The number (like `5` in `c5n`) represents the **generation**.

  * Newer generations = better performance, more efficiency
  * Example: `c5` → 5th generation of compute-optimized
---
## 🔷 4. **Instance Size**
After the dot (`.`), the size defines the **amount of vCPU and memory**:

| Size                     | Description                     |
| ------------------------ | ------------------------------- |
| `nano`                   | Smallest                        |
| `micro`                  | Very small (free tier eligible) |
| `small`                  | Small                           |
| `medium`                 | Moderate                        |
| `large`                  | Standard                        |
| `xlarge`                 | 2× resources of large           |
| `2xlarge` ... `24xlarge` | Higher CPU/memory               |
---
## ✅ Example: `c5n.xlarge`

* **`c`** → Compute optimized
* **`5`** → 5th generation
* **`n`** → Network optimized (high bandwidth, better EBS I/O)
* **`xlarge`** → 4 vCPU, \~8 GB RAM (approx., varies by instance type)
---

## ✅ Summary Mind Bullet Points:
* Instance type = **family + generation + capabilities + size**
* Choose instance based on **workload needs**: CPU, memory, storage, GPU, etc.
* **Graviton (`g`) = cost-efficient + better for ARM-native apps**
* **`n` = high-speed network**, **`d` = local disks**, **`z` = high GHz cores**

---
# ✅ How to Connect to an EC2 Instance via SSH (Linux/Mac/WSL)

#### 🔷 Prerequisites:
----------------------
1. ✅ You launched a **Linux-based EC2 instance**
2. ✅ You have the **`.pem` key pair file** (private key) you selected at launch
3. ✅ The instance has a **public IP** or **Elastic IP**
4. ✅ The **Security Group** allows inbound **SSH traffic on port 22**
5. ✅ You’re using a terminal (Mac/Linux/WSL) or Git Bash (Windows)

---
# 🔷 Step-by-Step Instructions:
### ✅ Step 1: Locate the Public IP of Your Instance

* Go to **EC2 Dashboard → Instances**
* Copy the **Public IPv4 address**
---
### ✅ Step 2: Open Your Terminal

Go to your terminal or Git Bash.
---
### ✅ Step 3: Navigate to the Directory Containing Your `.pem` File

```bash
cd /path/to/your/keypair/
```
---
### ✅ Step 4: Set Permissions on the `.pem` File
```bash
chmod 400 your-key-name.pem
```
> This ensures the private key is **readable only by you** (required by SSH).

---
### ✅ Step 5: Connect Using SSH

Use the following command to connect:

```bash
ssh -i your-key-name.pem ec2-user@<public-ip>
```
### 🔹 Example:

```bash
ssh -i mykey.pem ec2-user@3.110.45.123
```

> 💡 Replace `ec2-user` with the correct **default username** based on the AMI:

| AMI                 | Default SSH Username |
| ------------------- | -------------------- |
| Amazon Linux / RHEL | `ec2-user`           |
| Ubuntu              | `ubuntu`             |
| CentOS              | `centos`             |
| Debian              | `admin` or `debian`  |
| SUSE                | `ec2-user`           |

---
## ✅ Common SSH Errors and Fixes:

| Error                          | Fix                                           |
| ------------------------------ | --------------------------------------------- |
| `Permission denied`            | Wrong username or key                         |
| `Timeout` or No response       | Check Security Group (port 22 open?)          |
| `Unprotected private key file` | Run `chmod 400 your-key.pem`                  |
| `Host key verification failed` | Run `ssh-keygen -R <IP>` to clear known hosts |

---
## ✅ Optional (for Windows users):

* Use **Git Bash**, **Windows Terminal**, or **PuTTY**
* If using PuTTY, convert `.pem` to `.ppk` using PuTTYgen
---
## ✅ Summary:
1. Make sure port 22 is open in the **security group**
2. Use the right **username** and **`.pem`** file
3. SSH command:

```bash
ssh -i your-key.pem ec2-user@your-public-ip
```
---
---
# Explain Auto Scaling in EC2 and how it helps ensure application availability.
- Auto Scaling is a service that allows you to automatically adjust the number of EC2 instances in response to changing application demands. 
- It helps maintain application availability, improves fault tolerance, and optimizes resource usage by scaling out during periods of high demand and scaling in during lower demand.

# Explain the differences between on-demand, reserved, and spot instances. (OR) what are the EC2 Purchasing Options?
1.	On-Demand Instances: Pay-as-you-go pricing with no upfront commitment.
2.	Reserved Instances: Provides capacity reservation at a lower cost in exchange for a commitment.
3.	Spot Instances: Allows users to bid on unused EC2 capacity, potentially leading to significantly lower costs.


# Explain the difference between public IP and Elastic IP in EC2.
1. A public IP is assigned to an instance at launch, but it can change if the instance is stopped and started. 
2. An Elastic IP is a static IP address that can be associated with an instance, providing a consistent public IP even after stopping and starting the instance.

# AMAZON EC2 AUTO-SCALING: 
1. Amazon EC2 Auto Scaling enables you to automatically add or remove Amazon EC2 instances across different AZs in response to changing application demand.
  •  Dynamic scaling responds to changing demand. 
  •	 Predictive scaling automatically schedules the right number of Amazon EC2 instances based on predicted demand.

2. To scale faster, you can use dynamic scaling and predictive scaling together.
3. By adding Amazon EC2 Auto Scaling to an application, you can add new instances to the application when necessary and terminate them when no longer needed.
 

4. If you do not specify the desired number of Amazon EC2 instances in an Auto Scaling group, the desired capacity defaults to your minimum capacity.
      Max = up to 4 EC2 instances

---
# What is Dedicated host in Aws?

---
# what are key-pair in aws?
1. A key pair is a combination of a public key that is used to encrypt data and a private key that is used to decrypt data.
2. A key pair is a set of cryptographic keys that consists of a public key and a private key. Key pairs are primarily used for secure authentication and access to Amazon Elastic Compute Cloud (Amazon EC2) instances.
3. When you create an EC2 instance, you can associate a key pair with it. The public key is placed on the instance, and the private key is kept securely by the user. When you want to connect to the instance, you use the private key to authenticate, ensuring secure access to your virtual server. 
4. Key pairs are crucial for securing access to EC2 instances and are an essential component of AWS's security infrastructure.
---
# Explain the concept of EC2 instance metadata and user data.
1. **EC2 Instance Metadata:** EC2 instances have metadata that provides information about the instance, such as instance ID, public IP address, and IAM role. This metadata can be accessed from within the instance. 
2. **User Data:** User data is a script or data that can be passed to an EC2 instance during launch. It is often used to perform instance-specific configuration and customization.
---






