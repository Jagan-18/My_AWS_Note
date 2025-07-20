
# Amazon Route 53  - Route 53 on AWS provides DNS as a service.

# What is DNS ?
1. DNS – Domain name system
2. The Internet’s DNS system works much like a phone book by managing the mapping between names and numbers. 
3. DNS servers translate requests for names into IP addresses, controlling which server an end user will reach when they type a domain name into their web browser. These requests are called queries.

<img>
---
# What is Route 53?
1. You can use Route 53 in the Networking and Content Delivery section in AWS Console.
2. Route 53 is a highly available and scalable DNS web Service by Amazon.
3. It is a scalable (DNS) service that provides a reliable way to redirect traffic to applications. To achieve this domain names are translated to IP addresses to help computers connect better.
4. It is possible to connect queries to entities like Elastic Load Balancers in AWS using Amazon Route 53.

<img>

#### Route 53 is mainly used for 3 purposes:-
**1.DNS Registration:** - Your website or web application needs a name; Route 53 lets you register a name for the same.
**2. Route Internet Traffic:**- Route 53 helps you connect with your website or web application when you search for your domain name on your browser.
**3.Check Health Status:** - Route 53 sends automated request over internet to check the availability of your website or web application and sends you notification if it is unavailable so that you can route the requests to a healthy resource.

#### It provides several key features:
**1.	DNS Management:** Route 53 translates domain names (like www.example.com) into IP addresses (like 192.0.2.1), allowing users to access websites and services using human-readable names rather than numeric IP addresses.
**2.	Domain Registration:** It allows users to register new domain names directly through the service or transfer existing ones from other registrars.
**3.	Traffic Routing:** Route 53 supports various routing policies, including simple routing, weighted routing, latency-based routing, failover routing, and geolocation routing. These policies help manage how traffic is distributed across different endpoints.
**4.	Health Checks:** It can perform health checks on resources to ensure that traffic is only routed to healthy endpoints.
**5.	Integration with AWS Services:** Route 53 integrates seamlessly with other AWS services, such as Amazon S3, Amazon CloudFront, and Amazon EC2, making it easier to manage and route traffic to your AWS-hosted resources.
**6.	Scalability and Reliability:** Route 53 is designed to handle large volumes of DNS queries and offers high availability, ensuring that your DNS infrastructure is resilient and reliable.

---
## 🧱 Core Components of Route 53

| Component               | Description                                                               |
| ----------------------- | ------------------------------------------------------------------------- |
| **Domain Registration** | Buy/manage domain names directly from AWS.                                |
| **Hosted Zones**        | Container for DNS records of a domain (like a DNS database).              |
| **DNS Records**         | Map domain names to IP addresses or AWS services.                         |
| **Routing Policies**    | Decide how traffic is routed (e.g., latency-based, weighted).             |
| **Health Checks**       | Monitor endpoint health to ensure traffic only reaches healthy resources. |

---

## 🧾 DNS Record Types (Important!)
| Record Type | Use Case                                                                        |
| ----------- | ------------------------------------------------------------------------------- |
| **A**       | Maps domain name to an IPv4 address.                                            |
| **AAAA**    | Maps domain name to an IPv6 address.                                            |
| **CNAME**   | Maps a domain name to another domain name.                                      |
| **MX**      | Mail exchange records (email).                                                  |
| **NS**      | Lists name servers for a hosted zone.                                           |
| **TXT**     | Text data, often used for verification (e.g., SPF).                             |
| **Alias**   | AWS-specific – maps to AWS resources like ELB, CloudFront (acts like A record). |

---
## 📍 Routing Policies in Route 53
| Policy                               | Description                              | Example Use            |
| ------------------------------------ | ---------------------------------------- | ---------------------- |
| **Simple**                           | One record, one endpoint                 | Static site            |
| **Weighted**                         | Traffic split based on weights           | A/B testing            |
| **Latency-based**                    | Routes to the region with lowest latency | Global app performance |
| **Failover**                         | Primary/secondary configuration          | High availability      |
| **Geolocation**                      | Based on user’s location (country)       | Localized content      |
| **Geoproximity (Traffic Flow only)** | Based on location + biasing              | Regional service load  |
| **Multivalue Answer**                | Returns multiple values for redundancy   | DNS-level round robin  |

---
## 🧪 Health Checks
* Monitor **HTTP, HTTPS, TCP**, or even custom endpoints.
* Can be used with **Failover Policy** to route traffic to a backup server if primary fails.
* Can monitor:

  * Public endpoints (e.g., websites)
  * Other health checks (calculated health check)
  * CloudWatch alarms

---

## ✅ Use Case Example
🔸 **Website Hosted on EC2 with Load Balancer:**

1. Register domain on Route 53 (`yourdomain.com`)
2. Create a hosted zone for that domain
3. Create an **Alias A record** pointing to your **Elastic Load Balancer**
4. Use **Latency-based routing** if your app is deployed in multiple regions
5. Add **Health Checks** to monitor EC2 instance health

---

## 🛠️ Route 53: Step-by-Step Domain Setup (Console)
1. **Buy/Register Domain:**

   * Route 53 → Domain Registration → Register Domain

2. **Create Hosted Zone:**

   * Route 53 → Hosted Zones → Create Hosted Zone → Enter domain name

3. **Add DNS Records:**

   * A/AAAA for IP addresses
   * CNAME for subdomains
   * MX for email routing (if needed)

4. **Configure Routing Policy:**

   * Choose based on your needs (Simple, Latency, Failover, etc.)

5. **(Optional) Set Health Checks:**

   * Route 53 → Health Checks → Create new health check
   * Link to DNS record using **Failover policy**

6. **Point Domain to AWS Name Servers:**

   * Copy NS records from hosted zone
   * Update these in your domain registrar if domain is external (e.g., GoDaddy)

---
## 🛡️ Benefits of Route 53
* High availability and low-latency global DNS
* Seamless integration with AWS services
* Easy traffic routing and failover configurations
* DNS-based load balancing
* Scalable and secure

---
### 🔄 How It Works (End-to-End Flow)

1. **User enters a domain name** in a browser.
2. **DNS resolver** sends a query to Route 53.
3. Route 53 checks its **hosted zone** for matching records.
4. If health checks are configured, it verifies the endpoint’s health.
5. Based on the **routing policy**, Route 53 returns the best IP address.
6. The browser connects to the resolved IP and loads the application.

---

### 🛡️ Advanced Features

- **Route 53 Resolver**
  - Provides recursive DNS resolution for VPCs and hybrid environments.

- **DNS Firewall**
  - Blocks queries to malicious domains.

- **Traffic Flow**
  - Visual tool to manage complex routing strategies.

- **Integration with IAM**
  - Controls access and permissions securely.
  
---
### 📈 Benefits
- **Highly reliable** and globally distributed.
- **Scalable** to handle millions of queries.
- **Cost-effective**—pay only for what you use.
- **Secure** with DNSSEC and IAM integration.
- **Fast setup** with visual tools and automation.
---

