# AWS Load Balancers (Elastic Load Balancing - ELB):
Elastic Load Balancing (ELB) automatically distributes incoming application traffic across multiple targets, such as Amazon EC2 instances, containers, IP addresses, and Lambda functions, in one or more Availability Zones (AZs).

It improves **availability, fault tolerance, and scalability**.

---
## **Types of AWS Load Balancers:**
<img width="1536" height="1024" alt="Image" src="https://github.com/user-attachments/assets/bc45e502-7b50-4cb7-9aaa-890778567bc5" />

1. **Application Load Balancer (ALB):**

   * Works at **Layer 7 (HTTP/HTTPS)**.
   * Ideal for **web applications**.
   * Supports **path-based & host-based routing**.
   * Supports **WebSocket, gRPC, HTTP/2**.
   * Good for **microservices, APIs, and container-based apps (ECS/EKS)**.

   ✅ Example: `/api/*` routes to API servers, `/images/*` routes to image servers.

---
2. **Network Load Balancer (NLB):**

   * Works at **Layer 4 (TCP/UDP/TLS)**.
   * Handles **millions of requests per second**.
   * Provides **static IP** and supports **Elastic IPs**.
   * Used for **low latency and high throughput apps** (e.g., financial systems, gaming).

   ✅ Example: Routing raw TCP traffic for a trading app.

---
3. **Gateway Load Balancer (GWLB):**

   * Works at **Layer 3 (IP packet)**.
   * Used for **third-party virtual appliances** (firewalls, intrusion detection, packet inspection).
   * Ensures transparent traffic inspection.

   ✅ Example: Deploying a firewall cluster to monitor all VPC traffic.
---
4. **Classic Load Balancer (CLB)** *(Legacy)*

   * Works at both **Layer 4 & Layer 7**, but **limited features**.
   * AWS recommends using ALB or NLB for new applications.

---
## **Features of ELB:**
* **High Availability** – Distributes traffic across multiple AZs.
* **Health Checks** – Routes traffic only to healthy targets.
* **SSL/TLS Termination** – Offloads SSL certificates.
* **Auto Scaling Integration** – Works with EC2 Auto Scaling to handle variable workloads.
* **Security** – Integrates with AWS WAF (Web Application Firewall).

---
## **Simple Architecture Example:**
```
User -> ALB (Layer 7) -> EC2 Instances in multiple AZs
```

or

```
User -> NLB (Layer 4) -> ECS Tasks (Containers)
```
---
### ⚙️ **Core AWS Load Balancer Types:**
|      **Type**                       |     **Layer**          |           **Best For**                 |         **Key Features**                                                                            |
|-------------------------------------|------------------------|----------------------------------------|-----------------------------------------------------------------------------------------------------|
| **Application Load Balancer (ALB)** | Layer 7 (Application)  | HTTP/HTTPS traffic                     | Content-based routing (URL paths, host headers), WebSocket support, native integration with AWS WAF |
| **Network Load Balancer (NLB)**     | Layer 4 (Transport)    | Ultra-low latency, TCP/UDP traffic     | Handles millions of requests per second, static IP support, great for real-time apps                |
| **Gateway Load Balancer (GWLB)**    | Layer 3 (Network)      | Deploying & scaling virtual appliances | Transparent network gateway, integrates with firewalls, intrusion detection systems                 |
| **Classic Load Balancer (CLB)**     | Layer 4 & 7 (Legacy)   | Older apps on EC2-Classic              | Basic load balancing, limited features — AWS recommends migrating to ALB/NLB                        |

---

### 🚀 **Why Use AWS Load Balancers:**
- **Automatic Scaling** – Adjusts capacity to match traffic spikes or dips.
- **Health Checks** – Routes traffic only to healthy targets.
- **Security Offload** – Terminates SSL/TLS so backend servers can focus on app logic.
- **Multi-AZ Resilience** – Distributes traffic across Availability Zones for high uptime.

---

### 🛠 **How It Works:**
1. **Listener** receives client requests on a specific port/protocol.
2. **Routing Algorithm** (e.g., round robin, least connections) picks a healthy target.
3. **Target Group** processes the request and sends the response back via the load balancer.

---
