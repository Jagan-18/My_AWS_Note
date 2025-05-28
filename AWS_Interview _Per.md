## AWS
## What do you understand by NACL in AWS?**
- NACL stands for **Network Access Control List**. It’s a **stateless**, **firewall-level** security layer in AWS that controls **inbound and outbound traffic** at the **subnet level** within a VPC.
**Key points:**
  - * It allows or denies traffic **based on rules** (IP, protocol, port).
* **Stateless**: Unlike security groups, it doesn’t track traffic state — return traffic must be explicitly allowed.
* **Rules are evaluated in order**, starting from the lowest number.
* Every subnet must be associated with a NACL — by default, subnets use the default NACL which allows all traffic.

---

### 🧠 Bonus (if asked):

* Use NACLs to provide **an extra layer of security**, especially when securing public/private subnets.
* Good for **blocking specific IPs or CIDRs** across multiple resources.

---

Let me know if you want a comparison with security groups — it's a common follow-up!

