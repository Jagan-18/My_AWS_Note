# AWS CloudFront
---
# Content Delivery Networks (CDN)
1.	Imagine you have a website with **lots of cool content, like images, videos, and documents.** When a user visits your site from a different location far away from your server, the content might take a long time to load. That's where CDN comes to the rescue!

2.	**A CDN is like a network of servers spread across various locations worldwide. These servers store a copy of your website's content.** When a user requests your website, the content is delivered from the server closest to the user, making it super-fast! It's like having a local store for your website content everywhere in the world.

---
## 🌐 **What is AWS CloudFront?**
1.	CloudFront is **AWS's global content delivery network (CDN) service.** It accelerates the delivery of your web content (such as images, videos, static and dynamic files) to users worldwide with low latency and high transfer speeds.

2.	CloudFront is that securely delivers data, videos, applications, and APIs to customers globally with low latency and high transfer speeds

---
## 🏗️ **How Does CloudFront Work?**

1. **You store content** (like images, videos, or websites) in an origin (e.g., S3 bucket, EC2 instance, or custom HTTP server).
2. **A user requests the content** (e.g., via a website).
3. CloudFront checks its **edge cache** (nearest location to user):

   * ✅ If the content exists (cache hit), it delivers it instantly.
   * ❌ If not (cache miss), it retrieves from the origin, caches it, and delivers to the user.
4. All further user requests are served from the cache (until TTL expires).
---
> **Let's understand how CloudFront works with a simple example:**
> Imagine you have a website with images stored on an Amazon S3 bucket (a cloud storage service). When a user requests an image, the request goes to CloudFront first.

> **Here's how the process flows:**

> **Step 1:** CloudFront checks if it already has the requested image in its cache (storage). If it does, great! It sends the image directly to the user. If not, it proceeds to Step 2.
> **Step 2:** CloudFront fetches the image from the S3 bucket and stores a copy in its cache for future requests. Then, it sends the image to the user.

> The next time someone requests the same image, CloudFront will deliver it from its cache, making it super fast and efficient!


---
## ⚙️ **Key Features of CloudFront**
| Feature                     | Description                                                                     |
| --------------------------- | ------------------------------------------------------------------------------- |
| **Global Edge Locations**   | 600+ locations across continents for ultra-low latency                          |
| **Origin Support**          | Works with S3, EC2, ALB, Route 53, or custom servers                            |
| **HTTPS Support**           | Delivers content securely using SSL/TLS                                         |
| **DDoS Protection**         | Integrated with AWS Shield for security                                         |
| **Caching**                 | Configurable cache behaviors and TTL                                            |
| **Lambda\@Edge**            | Run custom code at edge locations (for personalization, A/B testing, redirects) |
| **Signed URLs and Cookies** | Restrict access to paid or confidential content                                 |
| **Logging & Metrics**       | Integrates with CloudWatch for real-time monitoring                             |

---
## 🧱 **CloudFront Architecture Components**
1. **Origin** – The source of your files (e.g., S3, EC2)
2. **Edge Location** – CDN server closer to the user
3. **Distribution** – The configuration for delivering content

   * **Web distribution** (for websites, APIs)
   * **RTMP distribution** (for streaming, deprecated)
4. **Cache Behavior** – Rules for content types, methods, TTLs
5. **Access Control** – Signed URLs, Geo-restrictions, WAF

---
## 🚀 **Benefits of Using CloudFront**
* ✅ **Fast Content Delivery:** CloudFront ensures your content reaches users with minimal delay, making your website lightning fast.
* ✅ **Global Reach:** With servers in various locations worldwide, CloudFront brings your content closer to users, regardless of where they are.
* ✅ **Security:** CloudFront provides security features like DDoS protection and SSL/TLS encryption to keep your content and users safe.
* ✅ **Scalability:** CloudFront can handle traffic spikes effortlessly, ensuring a smooth experience for your users.
* ✅ **Cost-Effective:** Pay only for the data transfer and requests made, making it cost-effective for businesses of all sizes.

---

## 💼 **Real-World Use Case**
**A video streaming platform** uses:

* **S3** to store videos
* **CloudFront** to distribute them globally with low latency
* **Signed URLs** to allow access only to paying users
* **Lambda\@Edge** to rewrite requests and add authentication

---

## 🧪 **Sample Setup: Creating a CloudFront Distribution (via Console)**

1. Go to **AWS Console → CloudFront**
2. Click **Create Distribution**
3. Under “Origin domain”, select an S3 bucket or your custom origin
4. Set **Viewer protocol policy** (Redirect HTTP to HTTPS recommended)
5. Set **Caching policy** (Default, or customize TTLs)
6. Optionally add **WAF**, **Geo restrictions**, or **Lambda\@Edge**
7. Click **Create**

You'll receive a **CloudFront domain name** like:
`d1xxyyzz.cloudfront.net` – use this in place of your S3 URL or backend domain

---

## 📌 Tips for Using CloudFront

* Set proper **cache-control headers** in your origin
* Use **invalidations** to refresh cache if needed
* Combine with **Route 53** for custom domain with CDN
* Secure with **AWS Certificate Manager** (for HTTPS/SSL)

---
# A step-by-step guide to integrate CloudFront with S3 or EC2.

## ✅ **Option 1: Integrate CloudFront with S3 Bucket**
#### 📂 Goal: Deliver static content (like images, CSS, JS, HTML) stored in S3 via CloudFront for better performance & security.
---
### 🔧 **Step-by-Step**
1. ### **Create an S3 Bucket**

   * Go to **S3 → Create bucket**
   * Name it (e.g., `my-static-content`)
   * Disable **Block All Public Access**
   * Optional: Enable versioning

2. ### **Upload Content**

   * Upload files you want to serve (HTML, images, etc.)
   * Set file permissions (either make public or use Origin Access Control)

3. ### **Set Permissions (Secure Way – Using OAC)**

   * Create **Origin Access Control (OAC)** in CloudFront
   * Update S3 bucket policy to **only allow access from CloudFront**

4. ### **Create CloudFront Distribution**

   * Go to **CloudFront → Create Distribution**
   * **Origin domain**: Choose your S3 bucket
   * Enable **Origin Access Control** (not public access)
   * Set **Viewer Protocol Policy** to “Redirect HTTP to HTTPS”
   * Choose **Caching Policy** (default or custom)
   * Add **Custom Domain** (optional) & SSL certificate (from ACM)

5. ### **Review & Create**

   * Click **Create Distribution**
   * Copy the **CloudFront Domain Name** (e.g., `d3xyz.cloudfront.net`)

6. ### **Test It**

   * Access content via the CloudFront URL:
     `https://d3xyz.cloudfront.net/index.html`

---
## ✅ **Option 2: Integrate CloudFront with EC2 Instance**

### 🖥️ Goal: Serve dynamic web applications running on EC2 via CloudFront (for latency & caching benefits)
---
### 🔧 **Step-by-Step**
1. ### **Launch EC2 Instance**

   * Choose Amazon Linux or Ubuntu
   * Install a web server (e.g., Apache or Nginx)
   * Example:

     ```bash
     sudo yum update -y
     sudo yum install httpd -y
     sudo systemctl start httpd
     sudo systemctl enable httpd
     ```
   * Place your web files in `/var/www/html`

2. ### **Security Group Settings**

   * Allow inbound **HTTP (port 80)** and **SSH (port 22)**
   * Optional: Enable **HTTPS (port 443)** if using SSL

3. ### **Ensure EC2 has a Public IP or Elastic IP**

4. ### **Create CloudFront Distribution**

   * Go to **CloudFront → Create Distribution**
   * **Origin domain**: Enter the EC2 public DNS or IP (e.g., `ec2-3-94-xyz.compute.amazonaws.com`)
   * **Origin Protocol Policy**: Choose “HTTP only” or “Match viewer”
   * Set **Viewer Protocol Policy** to “Redirect HTTP to HTTPS”
   * Enable caching (or disable if you want real-time dynamic content)

5. ### **Set Behavior**

   * If serving dynamic content, choose **cache based on all parameters** (headers, query strings)
   * Choose the appropriate TTL (set to 0 for dynamic content)

6. ### **Create and Deploy**

   * Click **Create Distribution**
   * Test it via the provided CloudFront URL

---
## 🔐 Optional Enhancements:
| Enhancement         | How to Add                                                           |
| ------------------- | -------------------------------------------------------------------- |
| **Custom domain**   | Use Route 53 or any DNS service to point your domain to CloudFront   |
| **HTTPS (SSL)**     | Use **AWS Certificate Manager (ACM)** to generate an SSL cert        |
| **WAF**             | Attach a **Web Application Firewall** to protect from common attacks |
| **Geo restriction** | Restrict access by region or country in CloudFront settings          |

---
## 📌 Tips
* Use **invalidations** to refresh cache if you update content
* Monitor usage via **CloudFront metrics in CloudWatch**
* Enable **access logs** for CloudFront in S3
* Use **Lambda\@Edge** for dynamic content transformation at the edge

---




