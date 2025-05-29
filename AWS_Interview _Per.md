## AWS

## 1.What do you understand by NACL in AWS?**
NACL stands for **Network Access Control List**. It’s a **stateless**, **firewall-level** security layer in AWS that controls **inbound and outbound traffic** at the **subnet level** within a VPC.
**Key points:**
  * It allows or denies traffic **based on rules** (IP, protocol, port).
  * **Stateless**: Unlike security groups, it doesn’t track traffic state — return traffic must be explicitly allowed.
  * **Rules are evaluated in order**, starting from the lowest number.
  * Every subnet must be associated with a NACL — by default, subnets use the default NACL which allows all traffic.
---
######  Bonus (if asked):
* Use NACLs to provide **an extra layer of security**, especially when securing public/private subnets.
* Good for **blocking specific IPs or CIDRs** across multiple resources.

---
## 2. have you worked with the lambda function?
**Yes, I’ve worked with AWS Lambda in multiple projects.**
I’ve used it to run serverless tasks such as:
* Automating **infrastructure cleanup** (e.g., unused volumes or snapshots),
* Processing **S3 events** (like resizing images or log parsing),
* Triggering **CI/CD steps** through API Gateway or EventBridge,
* And integrating with **CloudWatch alarms** to handle alerts or scale other services.
I usually deploy Lambda using **Terraform** or **Serverless Framework**, and manage environment variables, IAM roles, and logging via **CloudWatch**."
---


