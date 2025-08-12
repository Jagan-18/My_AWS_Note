# Secret Management on AWS

## **Secret Management on AWS**
Managing sensitive information such as passwords, API keys, database credentials, and tokens securely is critical in cloud environments. AWS provides multiple services to store, retrieve, and manage secrets securely with encryption and access control.

---

## **1. Why Secret Management is Important**

Without proper secret management, sensitive data can be:

* **Leaked** through code repositories (e.g., GitHub).
* **Exposed** in logs, environment variables, or misconfigured servers.
* **Misused** by unauthorized users or malicious actors.

**Goals:**

* **Confidentiality** – Only authorized entities can access secrets.
* **Integrity** – Secrets cannot be altered without detection.
* **Availability** – Secrets should be available to authorized workloads when needed.

---

## **2. AWS Services for Secret Management**

### **A. AWS Secrets Manager**

* Purpose-built for storing and managing secrets.
* Features:

  * Automatic rotation of secrets.
  * Fine-grained IAM access control.
  * Encrypted at rest using AWS KMS.
  * Integrated with RDS, Redshift, and other AWS services.
* Example Use Cases:

  * Database credentials for RDS.
  * API keys for external services.

---

### **B. AWS Systems Manager Parameter Store**

* Stores configuration data and secrets as parameters.
* Two types:

  * **Standard Parameters** – For non-sensitive data.
  * **SecureString Parameters** – For encrypted sensitive data.
* Encrypted using AWS KMS.
* Features:

  * Versioning of parameters.
  * Integration with AWS services like Lambda, EC2, and ECS.
* Example Use Cases:

  * Application configuration values.
  * Service tokens.

---

### **C. AWS Key Management Service (KMS)**

* Manages encryption keys used by Secrets Manager and Parameter Store.
* Features:

  * Customer-managed or AWS-managed keys.
  * Audit logs via AWS CloudTrail.
* Example Use Cases:

  * Encrypt/decrypt data manually.
  * Create CMKs (Customer Master Keys) for secret encryption.

---

## **3. Best Practices**

1. **Never hard-code secrets** in application code.
2. **Use IAM roles** to grant applications permissions to retrieve secrets.
3. **Enable automatic secret rotation** in Secrets Manager.
4. **Restrict access** using least privilege principle.
5. **Audit secret access** using AWS CloudTrail.
6. **Separate environments** (Dev, Staging, Prod) to isolate secrets.

---

## **4. How to Store a Secret in AWS Secrets Manager**

**Step 1:** Go to AWS Secrets Manager → “Store a new secret”
**Step 2:** Select “Other type of secret” or specific database credentials.
**Step 3:** Enter key-value pairs for your secret (e.g., username, password).
**Step 4:** Choose an encryption key (default or custom KMS key).
**Step 5:** Name the secret and add tags.
**Step 6:** Review and store the secret.

---

## **5. Accessing a Secret (Example: Python)**

```python
import boto3
import json

client = boto3.client('secretsmanager', region_name='us-east-1')

response = client.get_secret_value(SecretId='my-database-secret')
secret = json.loads(response['SecretString'])

print(secret['username'], secret['password'])
```

---

## **6. Using SSM Parameter Store for Secrets**

**Store a SecureString:**

```bash
aws ssm put-parameter \
  --name "DB_PASSWORD" \
  --value "MySecurePassword123" \
  --type "SecureString" \
  --key-id "alias/aws/ssm"
```

**Retrieve a SecureString:**

```bash
aws ssm get-parameter \
  --name "DB_PASSWORD" \
  --with-decryption
```

---

## **7. Choosing Between Secrets Manager and Parameter Store**

| Feature             | AWS Secrets Manager | AWS SSM Parameter Store          |
| ------------------- | ------------------- | -------------------------------- |
| Automatic Rotation  | ✅ Yes               | ❌ No                             |
| Cost                | Higher              | Lower (free for standard params) |
| Secret Versioning   | ✅ Yes               | ✅ Yes                            |
| KMS Encryption      | ✅ Yes               | ✅ Yes                            |
| Integrated with RDS | ✅ Yes               | ❌ No                             |

**Rule of Thumb:**

* Use **Secrets Manager** when you need automatic rotation and tight integration.
* Use **Parameter Store** for general configuration and low-cost secret storage.

---
