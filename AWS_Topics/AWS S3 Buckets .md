# AWS S3  (Simple Storage Service) :
------------------------------------
# What is Amazon S3?
1. Simple Storage Service is a scalable, Highly Available , Cost effective and secure cloud storage service provided by Amazon Web Services (AWS). It allows you to store and retrieve any amount of data from anywhere on the web.
2. It is designed for:
 - **High durability** (11 nines: 99.999999999%)
 - **Scalability** (stores trillions of objects)
 - **Low latency and high throughput**

**(OR)**
> * Amazon Simple Storage Service (Amazon S3) is a scalable object storage service designed to store and retrieve any amount of data from anywhere on the web. It's commonly used to store files, backups, images, videos, and more.
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
1. S3 buckets provide a reliable and highly scalable storage solution for various use cases.
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
# Pre-signed URL in S3:
1. A pre-signed URL uses security credentials to grant time-limited permission to download objects. The URL can be entered in a browser or used by a program to download the object. A pre-signed URL is signed with your credentials and can be used by any user.
2. A pre-signed URL uses three parameters to limit the access to the user.
 * **Bucket:** The bucket that the object is in (or will be in)
 * **Key:** The name of the object
 * **Expires:** The amount of time that the URL is valid
---
## Public and private access in S3.
1.	An S3 bucket is considered as Private if that does not have any public access provided to any of its ACL or bucket policy.
2.	S3 is bucket if it has provided access for external people to read/write/upload content files.
3.	A public bucket is one that everyone can access from the internet. A private one is not.
4.	Private buckets are accessible only to authorized users, while public buckets can be accessed by anyone with the bucket's URL.
5.	There are three levels’ to counted public.
  •  **Service level** – Default public.
  •	 **Bucket level** – Public.
  •	 **Object level** – Private.
---
# Creating and Configuring S3 Buckets: 
#### A..Creating an S3 bucket:
To create an S3 bucket, you can use the
1.	 AWS Management Console.
2.	AWS CLI (Command Line Interface), or AWS SDKs (Software Development Kits). 
       •	You need to specify a globally unique bucket name and select the region where you want to create the bucket.

### B.Choosing a bucket name and region:
1.	The bucket name must be unique across all existing bucket names in Amazon S3. 
2.	It should follow DNS naming conventions, be 3-63 characters long, and contain only lowercase letters, numbers, periods, and hyphens.
3.	The region selection affects data latency and compliance with specific regulations.

### C.Bucket properties and configurations -
**Versioning:** Versioning allows you to keep multiple versions of an object in the bucket. It helps protect against accidental deletions or overwrites.

### D.Bucket-level permissions and policies -
- Bucket-level permissions and policies define who can access and perform actions on the bucket. You can grant permissions using IAM (Identity and Access Management) policies, which allow fine-grained control over user access to the bucket and its objects.
---
# Uploading and Managing Objects in S3 Buckets:
**1.Uploading objects to S3 buckets:**
- You can upload objects to an S3 bucket using various methods, including the AWS Management Console, AWS CLI, SDKs, and direct HTTP uploads. Each object is assigned a unique key (name) within the bucket to retrieve it later.

**2.Object metadata and properties:**
- Object metadata contains additional information about each object in an S3 bucket. It includes attributes like content type, cache control, encryption settings, and custom metadata. These properties help in managing and organizing objects within the bucket.

**3.File formats and object encryption:**
- S3 supports various file formats, including text files, images, videos, and more. You can encrypt objects stored in S3 using server-side encryption (SSE). SSE options include SSE-S3 (Amazon-managed keys), SSE-KMS (AWS Key Management Service), and SSE-C (customer-provided keys).

**4.Lifecycle management:**
- Lifecycle management allows you to define rules for transitioning objects between different storage classes or deleting them automatically based on predefined criteria. For example, you can move infrequently accessed data to a lower-cost storage class after a specified time or delete objects after a certain retention period.

**5.Multipart uploads:**
- Multipart uploads provide a mechanism for uploading large objects in parts, which improves performance and resiliency. You can upload each part in parallel and then combine them to create the complete object. Multipart uploads also enable resumable uploads in case of failures.

**6.Managing large datasets with S3 Batch Operations:**
- S3 Batch Operations is a feature that allows you to perform bulk operations on large numbers of objects in an S3 bucket. It provides an efficient way to automate tasks such as copying objects, tagging, and restoring archived data.
---
# Advanced S3 Bucket Features:
**S3 Storage Classes** S3 offers multiple storage classes, each designed for different use cases and performance requirements:
<img>

---
# 1. S3 Replication:
- S3 replication enables automatic and asynchronous replication of objects between S3 buckets in different regions or within the same region. Cross-Region Replication (CRR) provides disaster recovery and compliance benefits, while Same-Region Replication (SRR) can be used for data resilience and low-latency access.

# 2. S3 Event Notifications and Triggers:
- S3 event notifications allow you to configure actions when specific events occur in an S3 bucket. For example, you can trigger AWS Lambda functions, send messages to Amazon Simple Queue Service (SQS), or invoke other services using Amazon SNS when an object is created or deleted.

# 3. S3 Batch Operations:
- S3 Batch Operations allow you to perform large-scale batch operations on objects, such as copying, tagging, or deleting, across multiple buckets. It simplifies managing large datasets and automates tasks that would otherwise be time-consuming.
---
# Security and Compliance in S3 Buckets:
**1. S3 bucket security considerations:** Ensure that S3 bucket policies, access control, and encryption settings are appropriately configured. Regularly monitor and audit access logs for unauthorized activities.
**2.Data encryption at rest and in transit:** Encrypt data at rest using server-side encryption options provided by S3. Additionally, enable encryption in transit by using SSL/TLS for data transfers.
**3.Access logging and monitoring:** Enable access logging to capture detailed records of requests made to your S3 bucket. Monitor access logs and configure alerts to detect any suspicious activities or unauthorized access attempts.

---
# S3 Bucket Management and Administration:
**1.S3 bucket policies:** Create and manage bucket policies to control access to your S3 buckets. Bucket policies are written in JSON and define permissions for various actions and resources.
**2.S3 access control and IAM roles:** Use IAM roles and policies to manage access to S3 buckets. IAM roles provide temporary credentials and fine-grained access control to AWS resources.
**3.S3 APIs and SDKs:** Interact with S3 programmatically using AWS SDKs or APIs. These provide libraries and methods for performing various operations on S3 buckets and objects.
**4.Monitoring and logging with CloudWatch:** Utilize Amazon CloudWatch to monitor S3 metrics, set up alarms for specific events, and collect and analyze logs for troubleshooting and performance optimization.
**5.S3 management tools:** AWS provides multiple management tools, such as the AWS Management Console, AWS CLI, and third-party tools, to manage S3 buckets efficiently and perform operations like uploads, downloads, and bucket configurations.

---
# Troubleshooting and Error Handling:
**1.Common S3 error messages and their resolutions:** Understand common S3 error messages like access denied, bucket not found, and exceeded bucket quota. Troubleshoot and resolve these errors by checking permissions, bucket configurations, and network connectivity.
**2.Debugging S3 bucket access issues:** Investigate and resolve issues related to access permissions, IAM roles, and bucket policies. Use tools like AWS CloudTrail and S3 access logs to identify and troubleshoot access problems.
**3.Data consistency and durability considerations:** Ensure data consistency and durability by understanding S3's data replication and storage mechanisms. Verify that data is correctly uploaded, retrieve objects using proper methods, and address any data integrity issues.
**4.Recovering deleted objects:** If an object is accidentally deleted, you can often recover it using versioning or S3 event notifications. Additionally, consider enabling Cross-Region Replication (CRR) for disaster recovery scenarios.

---
## Life Cycle management In S3:
1. An Amazon S3 Lifecycle rule configures predefined actions to perform on objects during their lifetime. You can create a lifecycle rule to optimize your objects storage costs throughout their lifetime.
2. You can define the scope of the lifecycle rule to all objects in your bucket to objects with a shared prefix, certain object tags, or a certain object size.
<img>

---
## Access control list (ACL) overview:
Amazon S3 access control lists (ACLs) enable you to manage access to buckets and objects. Each bucket and object has an ACL attached to it as a sub resource. It defines which AWS accounts or groups are granted access and the type of access. When a request is received against a resource, Amazon S3 checks the corresponding ACL to verify that the requester has the necessary access permissions.

<img>

---
## Static website hosting in S3:
1. You can use Amazon S3 to host a static website. On a static website, individual webpages include static content.
2. Using this option, you can get better management capabilities. 
---
## Encryption: 
1.	Encryption is a way of scrambling data so that only authorized parties can understand the information.
2.	In technical terms, it is the process of converting human-readable plaintext to ciphertext.
3.	In simpler terms, encryption takes readable data and alters it so that it appears random.
4.	Encryption requires the use of a cryptographic key.
<img>

---
## cross-origin resource sharing (CORS):
Cross-origin resource sharing (CORS) defines a way for client web applications that are loaded in one domain to interact with resources in a different domain. With CORS support, you can build rich client-side web applications with Amazon S3 and selectively allow cross-origin access to your Amazon S3 resources.
<img>

---
# How can you control access to objects in S3?
Access to S3 objects can be controlled using bucket policies, access control lists (ACLs), and IAM (Identity and Access Management) policies. You can define who can read, write, and delete objects.

---
# What is the difference between S3 Standard, S3 Intelligent-Tiering, and S3 One Zone-IA storage classes?
1. **S3 Standard:** Offers high durability, availability, and performance.
2. **S3 Intelligent-Tiering:** Automatically moves objects between two access tiers based on changing access patterns.
3. **S3 One Zone-IA:** Stores objects in a single availability zone with lower storage costs, but without the multi-AZ resilience of S3 Standard.

---
# What Is an S3 Bucket Policy?
An S3 bucket policy is an object that allows you to manage access to specific Amazon S3 storage resources. You can specify permissions for each resource to allow or deny actions requested by a principal (a user or role). When you create a new Amazon S3 bucket, you should set a policy granting the relevant permissions to the data forwarder’s principal roles.

---
# S3 Versioning:
1. S3 Versioning helps to keep multiple variants of an object in the same bucket and can be used to preserve, retrieve, and restore every version of every object stored in the S3 bucket.
2. S3 Object Versioning can be used to protect from unintended overwrites and accidental deletions.
3. After versioning is enabled for a bucket, if Amazon S3 receives multiple write requests for the same object simultaneously, it stores all those objects having different version id.
**An s3 bucket can be in three states:**
  1.	Un-versioned state (by default)  
  2.	Version-enabled state 
  3.	Version-suspended state

**(OR)**
> S3 versioning is a feature that allows you to preserve, retrieve, and restore every version of every object in a bucket. It helps protect against accidental deletion and overwrite.


