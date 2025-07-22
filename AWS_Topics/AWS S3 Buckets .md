# AWS S3  (Simple Storage Service) :
------------------------------------
# What is Amazon S3?
1. Simple Storage Service is a scalable, Highly Available , Cost effective and secure cloud storage service provided by Amazon Web Services (AWS). It allows you to store and retrieve any amount of data from anywhere on the web.
2. It is designed for:
 - **High durability** (11 nines: 99.999999999%)
 - **Scalability** (stores trillions of objects)
 - **Low latency and high throughput**

**(OR)**
> *Amazon Simple Storage Service (Amazon S3) is a scalable object storage service designed to store and retrieve any amount of data from anywhere on the web. It's commonly used to store files, backups, images, videos, and more.
> * It looks similar to your Google drive/ one drive and also allow unlimited amount of data (Highly scalable – Up to 5TD per file).

---
# What are S3 buckets? / What can you store in these S3?
1. S3 buckets are containers for storing objects (files, images, videos, and more.) in Amazon S3. Each bucket has a unique name globally across all of AWS. 
2. You can think of an S3 bucket as a top-level folder that holds your data

**OR**
> * An **S3 Bucket** is a **container for storing objects (files/data)**.
> * All objects are stored **inside buckets**.
> * Each bucket must have a **globally unique name**.
> * Buckets live **within regions** (e.g., `us-east-1`), which determines **latency and data residency**.

<img>


#### 🧾 Object Basics:
* **Object** = Data + Metadata + Key (name)
* Each object is identified by a **key** (filename/path inside the bucket).
* Objects can be up to **5 TB** in size.
---
# Why use S3 buckets?
1.S3 buckets provide a reliable and highly scalable storage solution for various use cases.
2. They are commonly used for backup and restore, data archiving, content storage for websites, and as a data source for big data analytics.

**Key benefits of S3 buckets (S3 buckets offer several advantages,) including:**
1. **Durability and availability:** S3 provides high durability and availability for your data.
2. **Scalability:** You can store and retrieve any amount of data without worrying about capacity constraints.
3. **Security:** S3 offers multiple security features such as encryption, access control, and audit logging.
4. **Performance:** S3 is designed to deliver high performance for data retrieval and storage operations.
5. **Cost-effective:** S3 offers cost-effective storage options and pricing models based on your usage patterns.

---
### 🔒 S3 Security:
| Feature                 | Description                                               |
| ----------------------- | --------------------------------------------------------- |
| **Bucket Policies**     | JSON-based policies to control access at the bucket level |
| **IAM Policies**        | Grant fine-grained access using IAM roles/users           |
| **ACLs (Legacy)**       | Object and bucket-level permissions (not recommended)     |
| **Encryption**          | SSE-S3, SSE-KMS, SSE-C, client-side encryption            |
| **Block Public Access** | Prevent accidental public exposure (recommended)          |

---
## 🚀 Key Features:
✅ **Durability and Availability**

* **99.999999999% (11 9’s) durability**
* **99.99% availability** SLA
---
## ✅ **Storage Classes**
| Class                  | Use Case                                | Durability | Cost        |
| ---------------------- | --------------------------------------- | ---------- | ----------- |
| S3 Standard            | General-purpose storage                 | 11 9s      | 💰 Normal   |
| S3 Intelligent-Tiering | Automatically moves data to lower tiers | 11 9s      | 💰 Smart    |
| S3 Standard-IA         | Infrequent access data                  | 11 9s      | 💵 Lower    |
| S3 One Zone-IA         | Same as above but 1 AZ only             | 99.5%      | 💸 Lower    |
| Glacier                | Archival (minutes to hours retrieval)   | 11 9s      | 💲 Low      |
| Glacier Deep Archive   | Archival (12+ hour retrieval)           | 11 9s      | 🪙 Cheapest |

✅ **Versioning**
* Keep **multiple versions** of objects to protect from accidental deletes or overwrites.

✅ **Lifecycle Rules**
* Automatically **transition storage class**, **expire/delete** objects based on age.

✅ **Replication**
* **Cross-Region Replication (CRR)** or **Same-Region Replication (SRR)** for disaster recovery or compliance.

✅ **Logging & Monitoring**
* **Server Access Logging** (records requests)
* **S3 Event Notifications** (trigger Lambda, SQS, SNS)
* **CloudTrail** logs for auditing
* **CloudWatch Metrics**

---
## 🌐 Access Options
* **HTTPS URL Access** for public objects.
* **Pre-Signed URLs** for temporary access to private objects.
* **Static Website Hosting** (for frontend websites from S3).
---
## 🛡️ Use Cases
* Hosting static websites
* Storing backups, logs, and audit trails
* Media storage for web/mobile apps
* Big data analytics
* Data lake for ML pipelines
---
