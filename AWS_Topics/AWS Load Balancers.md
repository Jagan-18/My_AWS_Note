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
# 👉 *“If someone sends a request, how does it flow through the seven layers of the OSI model?”*

## **Answer: Flow of a Request Through the OSI 7 Layers**
When a client (like a browser or mobile app) sends a request to a server (like a web app hosted on AWS), the request travels through the **OSI (Open Systems Interconnection) model**, which has **7 layers**:
<img width="1024" height="1536" alt="Image" src="https://github.com/user-attachments/assets/cfc72986-2ebb-4ef4-86ab-4290f69ee924" />

### **Step-by-Step Flow:**
1. **Application Layer (Layer 7)**

   * User interacts with an app (e.g., typing a URL in a browser).
   * Protocols: HTTP/HTTPS, FTP, DNS, SMTP.
   * The request is generated here.

2. **Presentation Layer (Layer 6)**

   * Data gets translated into a standard format.
   * Handles encryption (SSL/TLS) and compression.
   * Example: HTTPS request encryption.

3. **Session Layer (Layer 5)**

   * Manages sessions between client and server.
   * Ensures authentication, session establishment, and termination.
   * Example: Login session to a website.

4. **Transport Layer (Layer 4)**

   * Breaks data into segments.
   * Ensures reliable delivery using **TCP** (connection-oriented) or faster delivery using **UDP** (connectionless).
   * Example: TCP handshake (SYN, SYN-ACK, ACK).

5. **Network Layer (Layer 3)**

   * Adds logical addressing (IP addresses).
   * Determines the best route to the destination server.
   * Protocol: **IP (IPv4/IPv6)**, routing handled here.

6. **Data Link Layer (Layer 2)**

   * Adds **MAC addresses** (physical addressing).
   * Frames data for transmission over the physical network (LAN/Wi-Fi).
   * Switches operate here.

7. **Physical Layer (Layer 1)**

   * Converts data into electrical/optical/radio signals.
   * Physical transmission over cables, fiber optics, or wireless.
   * Example: Ethernet cable or Wi-Fi signals.

---
### **Reverse Flow (Server Response)**
When the server responds, the flow happens in **reverse order**:

* Starts at **Layer 7 (Application)** on the server → goes down to Layer 1 (Physical).
* Travels back over the network.
* At the client, it moves **upward from Layer 1 → Layer 7** until the user sees the response (e.g., a webpage).
---
✅ **Short Summary (for interviews):**
*A request starts at Layer 7 (Application) and travels down through the OSI layers until it becomes physical signals at Layer 1. On the receiving side, the process is reversed back up to Layer 7, where the application interprets the data.*

---


