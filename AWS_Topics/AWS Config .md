# AWS Config 

AWS **Config** is a **service that continuously monitors, records, and evaluates** the configurations of your AWS resources. It helps DevOps, security, and compliance teams ensure that infrastructure stays secure and compliant with best practices.

---
## **1. What is AWS Config?**
* A **configuration management & compliance** service.
* Tracks **resource inventory, configuration history, and changes**.
* Evaluates AWS resources against **rules** (e.g., “S3 buckets must not be public”).
* Provides a **timeline of changes** to resources for audit & troubleshooting.

---
## **2. Key Features**
✅ **Resource Inventory** – Lists all AWS resources in your account.
✅ **Configuration History** – Keeps a history of changes to each resource.
✅ **Configuration Snapshots** – Point-in-time view of resource configurations.
✅ **Compliance Evaluation** – Uses AWS Config **rules** to check compliance.
✅ **Integration with CloudTrail** – Track *who made the changes*.
✅ **Multi-Account Aggregation** – Centralize compliance view across accounts.

---
## **3. Common Use Cases**
* **Security & Compliance**:

  * Ensure IAM policies do not allow wildcards (`*`).
  * Check if S3 buckets are encrypted and not public.
  * Ensure EBS volumes are encrypted.

* **Auditing & Governance**:

  * Generate compliance reports for audits (HIPAA, PCI, SOC2).
  * Track who changed security group rules.

* **Troubleshooting**:

  * Rollback or investigate resource misconfigurations.

---
## **4. How AWS Config Works**
1. **Enable AWS Config** → Select region, resources, and S3 bucket for logs.
2. **AWS Config Recorder** → Records changes to resources.
3. **Config Rules** → Evaluates compliance (managed or custom).
4. **Compliance Dashboard** → Shows compliant vs non-compliant resources.
5. **Remediation** → Optionally auto-remediate non-compliance (via SSM Automation).

---
## **5. AWS Config Rules**
There are two types of rules:

* **Managed Rules (pre-built)** – Examples:

  * `s3-bucket-server-side-encryption-enabled`
  * `iam-password-policy`
  * `restricted-ssh`
* **Custom Rules** – Write rules in **AWS Lambda**.
  Example: Check if EC2 instance type is only `t3.micro`.

---
## **6. Example: Enable AWS Config (CLI)**
```bash
aws configservice put-configuration-recorder \
  --configuration-recorder name=default,roleARN=arn:aws:iam::123456789012:role/MyConfigRole

aws configservice start-configuration-recorder --configuration-recorder-name default
```

---
## **7. Example: Compliance Rule (S3 Bucket Encryption)**
```bash
aws configservice put-config-rule \
  --config-rule '{
    "ConfigRuleName": "s3-bucket-encryption-enabled",
    "Source": {
      "Owner": "AWS",
      "SourceIdentifier": "S3_BUCKET_SERVER_SIDE_ENCRYPTION_ENABLED"
    }
  }'
```
---
## **8. Pricing**

* **Pay per rule evaluation**.
* Free tier: 1,000 evaluations/month.
* After that, \~\$0.003 per evaluation.

---
## **9. Best Practices**
* Always enable AWS Config in **all regions**.
* Use **aggregators** for multi-account compliance view (via AWS Organizations).
* Store **Config history in S3 + CloudTrail** for audits.
* Use **auto-remediation** with SSM to fix non-compliance automatically.

---
✅ In short: **AWS Config = Track + Audit + Enforce compliance of AWS resources**.
It’s like having a **CCTV + compliance officer** for your AWS environment.

---

<img width="1536" height="1024" alt="Image" src="https://github.com/user-attachments/assets/f9a66c5a-4a17-4cce-90b5-39b8ba2b71ed" />

# 🚀 **DevOps Workflow with AWS Config**
Imagine your company is deploying workloads with **CI/CD pipelines (CodePipeline + Terraform/CloudFormation)**. You want to make sure every deployment stays **secure & compliant**.

---
## **Step 1 – CI/CD Deployment**
* Developer commits code → CodePipeline runs.
* Infrastructure is deployed using Terraform/CloudFormation.
* Example: Creates **S3 bucket + EC2 instance + IAM roles**.
---
## **Step 2 – AWS Config Recording**

* AWS Config is **enabled** in the account.
* It automatically records:

  * S3 bucket configuration (ACL, encryption).
  * EC2 instance type, tags, and security group rules.
  * IAM role policies.

---
## **Step 3 – Compliance Evaluation**
AWS Config runs **rules** (Managed or Custom):

* ✅ `s3-bucket-server-side-encryption-enabled` → Ensures all buckets have encryption.
* ✅ `restricted-ssh` → Ensures no security group has 0.0.0.0/0 for port 22.
* ✅ `ec2-instance-type-restriction` (custom) → Ensures only `t3.micro` instances are used in dev.

If resources **pass**, they’re marked **COMPLIANT**.
If they **fail**, they’re marked **NON-COMPLIANT**.

---
## **Step 4 – Alerting**
* Non-compliance triggers **CloudWatch Event → SNS notification → Slack/Email**.
* Example: “🚨 S3 Bucket `my-app-logs` is PUBLIC!”

---
## **Step 5 – Auto-Remediation (Optional)**
AWS Config can trigger **SSM Automation Documents** to **fix issues automatically**.

* If S3 bucket is public → Remove public access block.
* If EBS volume is unencrypted → Snapshot → create encrypted copy → replace.

---
## **Step 6 – Auditing & Reporting**
* Compliance dashboard in AWS Config shows **compliance score** (e.g., 92% compliant).
* Reports sent to security/compliance team weekly.
* For audits (e.g., PCI, HIPAA, ISO 27001), AWS Config provides **configuration history** + compliance evidence.

---
## **Example Workflow in Action**
👉 A developer creates a new S3 bucket `my-app-logs` **without encryption**.

* AWS Config detects the change.
* Marks bucket as **NON-COMPLIANT**.
* Sends **alert to DevOps Slack channel**.
* **SSM Automation** runs → Enables SSE-S3 encryption on the bucket.
* Within minutes, the bucket is compliant again.

---
✅ **This is how DevOps teams actually use AWS Config in real projects:**

* **Pipeline deploys infra → AWS Config evaluates → Auto-remediation + alerts → Audit evidence stored.**

---
