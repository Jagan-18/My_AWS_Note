# Security Groups and Network Access Control Lists (NACLs):
----------------------------------------------------------

### Security group is the firewall of EC2 Instances.
### Network ACL is the firewall of the VPC Subnets.

### 🔹 1. **Security Groups** (Instance-Level Firewall)

**What it is:**
A Security Group (SG) acts as a **virtual firewall** for **EC2 instances** (and other services like RDS or Lambda). It **controls inbound and outbound traffic at the instance level**.
- AWS Security is always a shared responsibility.

<img>

- Security Groups operate at the instance level and control traffic to and from individual EC2 instances.
- Scope of application: Security Groups apply to individual instances.
- NACLs operate at the subnet level and control traffic in and out of a VPC.
- Scope of application: NACLs apply to all instances in a subnet.

**Security group basically there two things **
1.	Inbound Traffic.
2.	Out bound Traffic.

<img>

Inbound rules control the incoming traffic to your instance.
**(OR)**
Inbound traffic refers to any traffic coming to your network, regardless of source or method. If the incoming request originates from any outside organization or user, it’s considered inbound traffic.
---
outbound rules control the outgoing traffic from your instance. When you launch an instance, you can specify one or more security groups.
**(OR)**
--------> Outbound traffic refers to traffic that originates from inside your own network. 
# NACL’s
NACL basically the primary purpose is you can deny what kind of traffic that you would want and to you can allow what kind of traffic you want.

<img>

---

**Key Features:**
* **Stateful:** If you allow inbound traffic, the outbound response is automatically allowed.
* Applied to **ENIs (Elastic Network Interfaces)** — typically attached to EC2.
* **Only allow rules** (no deny rules).
* You can **assign multiple SGs** to an instance.

**Use Case:**
```plaintext
- Allow inbound SSH (port 22) only from your office IP.
- Allow inbound HTTP (port 80) from anywhere.
- Allow outbound traffic on all ports.
```
**How to implement:**
1. Go to **EC2 Dashboard** → **Security Groups** → **Create Security Group**
2. Define **inbound** and **outbound** rules
3. Attach SG to EC2 instance during launch or later
---
---
### 🔸 2. **Network ACLs (NACLs)** (Subnet-Level Firewall)

**What it is:**
A NACL is a **stateless firewall** applied at the **subnet level**. It controls traffic entering and leaving a subnet.

**Key Features:**

* **Stateless:** Inbound and outbound rules are managed separately.
* Supports both **Allow** and **Deny** rules.
* Rules are evaluated in **order of rule number (lowest to highest)**.
* Applies to **all resources** within the subnet.

**Use Case:**

```plaintext
- Deny all traffic from a specific malicious IP address range
- Allow only HTTP/HTTPS traffic to your web subnet
```

**How to implement:**

1. Go to **VPC Dashboard** → **Network ACLs**
2. Create or modify a NACL
3. Add **inbound and outbound rules**
4. Associate it with the required **subnet(s)**

---
## 🔸 3. **IAM Policies** (Identity-Based Access Control)
**What it is:**
IAM Policies define **who can do what** on AWS. They are used to manage **user and service permissions** at a very granular level.

**Key Features:**

* Written in **JSON**
* Can be attached to **users**, **groups**, or **roles**
* Supports **Allow** and **Deny**
* Can restrict access to **specific resources**, **actions**, **conditions**

**Use Case:**

```json
{
  "Effect": "Allow",
  "Action": "ec2:DescribeInstances",
  "Resource": "*"
}
```
**How to implement:**
1. Go to **IAM Dashboard** → **Policies**
2. Create or edit a JSON policy
3. Attach the policy to a user/group/role

---
## 🔒 Mapping to CIA Triad
| Principle           | How AWS Helps                                                                                                                                            |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Confidentiality** | ✅ IAM Policies ensure only authorized users can access specific resources<br>✅ Security Groups restrict access to EC2 or databases only to known sources |
| **Integrity**       | ✅ IAM and NACLs prevent unauthorized modifications<br>✅ CloudTrail (optional) helps audit changes                                                        |
| **Availability**    | ✅ SG/NACL rules allow only required traffic, minimizing attack surface<br>✅ IAM ensures only needed permissions are granted, reducing accidental impact  |

---
## 🧪 Real-World Example: Web App Security
| Layer              | Resource                      | Rule Example                                                 |
| ------------------ | ----------------------------- | ------------------------------------------------------------ |
| **Security Group** | EC2 instance in Public Subnet | Allow `80/443` from `0.0.0.0/0` and SSH from `your IP`       |
| **NACL**           | Subnet containing EC2         | Allow inbound `80/443`, deny port `23 (telnet)`              |
| **IAM Policy**     | Developer Role                | Allow `ec2:StartInstances` but Deny `ec2:TerminateInstances` |

---
## ✅ Best Practices
* Least Privilege: **Only allow what is necessary**
* Use **Security Groups** for instance-level control
* Use **NACLs** for subnet-level protection (e.g., deny known attack IPs)
* Regularly audit IAM Policies with **IAM Access Analyzer**
* Enable **CloudTrail** for activity logging
* Tag SGs and NACLs for clarity and auditability

---
# Primary Difference Between Security Groups and NACLs:
| Feature                   | Security Group                                     | NACL (Network ACL)                                |
|---------------------------|----------------------------------------------------|---------------------------------------------------|
| **Scope**                 | Instance-level (applies to EC2 instances)          | Subnet-level (applies to entire subnets)          |
| **Type**                  | Stateful (return traffic is automatically allowed) | Stateless (must explicitly allow return traffic)   |
| **Rules Supported**       | Only "Allow" rules                                 | "Allow" and "Deny" rules                          |
| **Applies To**            | Attached to network interfaces/instances           | Attached to subnets (affects all in subnet)        |
| **Rule Evaluation**       | Evaluates all rules                                | Evaluates rules in order, stops at first match     |
| **Default Behavior**      | Denies inbound, allows outbound by default         | Allows all by default (default NACL); custom NACLs deny by default unless rules are added |
--
### 🧠 In Simple Terms:
* 🔒 **Security Group** is like a *door lock* on each **individual room (EC2)** — once someone enters, they’re allowed to exit freely.
* 🚪 **NACL** is like a *building gate* for the **whole floor (subnet)** — entry and exit both must be explicitly permitted.
---

