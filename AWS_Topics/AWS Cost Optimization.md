# AWS Cost Optimization

## 💰 **What is AWS Cost Optimization?**
#### Cost Optimization:
1.	By utilizing serverless functions like Lambda for event-driven tasks, we can eliminate the need for provisioning and managing servers, reducing costs associated with instance hours, maintenance, and upgrades.
2.	Additionally, leveraging S3 Glacier for cost-effective long-term storage of archived documents reduces storage costs by up to 90% compared to S3 Standard.
3.	This architecture provides a secure, scalable, and cost-effective solution for handling user document uploads, processing, and storage within an insurance microservice environment.


---
> # Strategies: Here are one-liner explanations for each of the AWS Cost Optimization strategies:
>1.	Reserved Instances (RIs): Commit to using EC2 instances for a 1- or 3-year term to reduce costs by up to 75%.
> 2.	Spot Instances: Use spare EC2 capacity at a lower cost, ideal for batch processing, data processing, or other non-critical workloads.
> 3.	Rightsizing: Match instance types and sizes to workload requirements, reducing costs by up to 50% and improving resource utilization.
> 4.	Idle Resource Identification: Identify and terminate unused or idle resources, such as EC2 instances, RDS instances, or S3 buckets, to eliminate unnecessary costs.
> 5.	Storage Optimization: Use cost-effective storage options, such as S3 Infrequent Access or Glacier, for infrequently accessed data to reduce storage costs.

---
## 🛠️ **5 Pillars of AWS Cost Optimization**

### 1. **Right-Sizing Resources**

* **Analyze usage** and resize underutilized EC2, RDS, or EBS volumes.
* Use **AWS Compute Optimizer** to get recommendations.
* Example: Downgrade from `m5.2xlarge` to `m5.large` if CPU is \~10%.

### 2. **Use Appropriate Pricing Models**

* **On-Demand**: For unpredictable workloads.
* **Reserved Instances (RI)**: Commit for 1–3 years and save up to 72%.
* **Savings Plans**: Flexible alternative to RI — applies across instance types.
* **Spot Instances**: Up to 90% discount for interruptible workloads (great for batch jobs, CI/CD, etc.)

### 3. **Auto Scaling**

* Set up **Auto Scaling Groups** to dynamically adjust capacity.
* Reduces waste during low traffic and scales during high traffic.

### 4. **Eliminate Unused Resources**

* Unattached **EBS volumes**, **idle Elastic IPs**, **stopped EC2 instances**, **old snapshots**, etc.
* Use **AWS Trusted Advisor** or **Cost Explorer** to detect unused resources.

### 5. **Storage Optimization**

* Use appropriate S3 storage classes:

  * **Standard** for frequent access.
  * **Infrequent Access** or **Glacier** for backups, logs, archives.
* Enable **S3 lifecycle rules** to transition or delete old objects.

---
## 📊 **Tools for Cost Monitoring and Optimization**
| Tool                       | Purpose                                        |
| -------------------------- | ---------------------------------------------- |
| **AWS Cost Explorer**      | Visualize spend, filter by service/account     |
| **AWS Budgets**            | Set custom alerts when usage crosses threshold |
| **AWS Trusted Advisor**    | Cost-saving and security recommendations       |
| **Compute Optimizer**      | Right-size compute resources                   |
| **AWS Savings Plans**      | Apply commitment-based savings across services |
| **Cost Anomaly Detection** | AI-powered alerts for unexpected cost spikes   |

---
## 💡 **Best Practices for Cost Optimization**

### ✅ Tagging

* Use **resource tags** (`Environment=Dev`, `Project=AppX`) to track spend per team/project.

### ✅ Schedule Non-Prod Environments

* Use **Instance Scheduler** to automatically shut down dev/test environments during off-hours.

### ✅ Consolidate Billing

* **Organizations** feature allows central management of multiple accounts with volume discounts.

### ✅ Use Serverless & Managed Services

* Pay only for usage (e.g., **Lambda**, **Fargate**, **RDS Aurora Serverless**, **S3**).

### ✅ Monitor Logs

* Set **retention periods** for CloudWatch logs.
* Stream logs to S3/Glacier for cheaper long-term storage.

---
### 🧪 **Example: Monthly Savings Opportunity**

| Optimization Step                      | Monthly Savings (Example) |
| -------------------------------------- | ------------------------- |
| Right-size EC2 instances               | \$200                     |
| Use Spot Instances for batch workloads | \$150                     |
| Move S3 logs to Glacier via lifecycle  | \$50                      |
| Delete unused EBS volumes              | \$30                      |
| Schedule dev EC2 shutdowns             | \$100                     |

**Total savings: \~\$530/month** — without impacting app performance.

---
## 🎯 Real-World Use Case:

**Company A** had 5 EC2 instances running 24x7 for QA, but only needed 8 hours/day.
They used AWS Instance Scheduler to stop instances after office hours.
→ Saved **70%** of the EC2 cost.

---
####  Cost Optimization Example:  When creating EC2 instances, it's common to automatically create EBS volumes and take snapshots of those volumes at regular intervals. 
* However, **when deleting the EC2 instances and their associated volumes, it's easy to forget to delete the EBS snapshots.** This oversight can lead to unnecessary costs, as the snapshots continue to occupy storage space and incur costs.
* To avoid these unnecessary costs, it's essential to **implement a process to automatically delete EBS snapshots when the associated EC2 instances and volumes are deleted.** This can be achieved through AWS services such as:

1.	**AWS CloudFormation:** Use CloudFormation to manage infrastructure as code, including EC2 instances, volumes, and snapshots. This ensures that all resources are properly cleaned up when deleted.

2.	**AWS Lambda:** Create a Lambda function that periodically checks for unused EBS snapshots and deletes them.

3.	**AWS CloudWatch:** Set up CloudWatch events to trigger a Lambda function or an AWS SDK call to delete snapshots when an EC2 instance is terminated.

* By implementing these strategies, you can avoid unnecessary costs associated with unused EBS snapshots and optimize your AWS storage costs.


---
# 🧾 **Sample AWS Monthly Cost Report – July 2025**

| **Category**             | **Service**    | **Spend (INR)** | **% of Total** | **Notes**                                      |
| ------------------------ | -------------- | --------------- | -------------- | ---------------------------------------------- |
| **Compute**              | EC2            | ₹23,000         | 38%            | On-Demand & Reserved Instances                 |
|                          | Lambda         | ₹2,000          | 3%             | Serverless APIs, pay-per-invocation            |
|                          | Auto Scaling   | ₹1,200          | 2%             | Saves \~₹3,000/month                           |
| **Storage**              | S3             | ₹5,500          | 9%             | Standard + Glacier via Lifecycle policy        |
|                          | EBS            | ₹4,000          | 6.5%           | Mostly gp3 volumes                             |
|                          | Snapshots      | ₹1,800          | 3%             | Weekly, need lifecycle policy                  |
| **Database**             | RDS            | ₹10,000         | 16%            | Multi-AZ Postgres DB, backup retention: 7 days |
| **Networking**           | NAT Gateway    | ₹3,600          | 6%             | Consider replacing with NAT instance           |
|                          | Data Transfer  | ₹2,300          | 4%             | Between AZs and S3                             |
| **Monitoring & Logging** | CloudWatch     | ₹1,700          | 2.5%           | Logs + custom metrics, consider log expiry     |
| **Developer Tools**      | CodePipeline   | ₹900            | 1.5%           | Basic usage                                    |
| **Others**               | Misc. Services | ₹2,000          | 3%             | SNS, SQS, IAM, Systems Manager                 |

### 🔸 **Total Monthly Spend**: **₹58,000**
---

## 📉 **Optimization Opportunities**
| **Area**    | **Action**                             | **Estimated Monthly Savings (INR)** |
| ----------- | -------------------------------------- | ----------------------------------- |
| EC2         | Right-size `m5.xlarge` to `t3.medium`  | ₹6,000                              |
| EBS         | Delete unattached volumes              | ₹1,200                              |
| Snapshots   | Enable lifecycle rules                 | ₹500                                |
| NAT Gateway | Replace with NAT instance for dev/test | ₹2,000                              |
| S3          | Move old logs to Glacier Deep Archive  | ₹1,000                              |
| CloudWatch  | Set 15-day retention + export to S3    | ₹700                                |

**🎯 Total Potential Savings: ₹11,400/month (\~20%)**

---
## 📈 **Spend Trend (Last 3 Months)**
| Month     | Spend (INR) | Change |
| --------- | ----------- | ------ |
| May 2025  | ₹63,000     |        |
| June 2025 | ₹60,200     | -4.4%  |
| July 2025 | ₹58,000     | -3.6%  |

---
## 🧩 **Recommendations**
* Set up **AWS Budgets** for compute and S3
* Automate instance scheduling for dev environment
* Review usage reports monthly with engineering leads
* Evaluate **Savings Plans** for long-term usage

---
# A script for scheduling EC2 shutdowns
### ✅ **1. Requirements**

* AWS CLI installed and configured (`aws configure`)
* EC2 instance IDs or tags
* IAM user/role with `ec2:StopInstances` permission

---
### 📝 **Step-by-Step Script: Schedule EC2 Shutdown**
```bash
#!/bin/bash

# Description: Stops specified EC2 instances based on tag or instance IDs

# Set AWS Region
AWS_REGION="ap-south-1"

# Define instance IDs (optional if using tag filter)
INSTANCE_IDS=("i-0abc123def456gh78" "i-0123example456")

# OR: Stop instances by tag (uncomment to use tag filter)
# TAG_KEY="Environment"
# TAG_VALUE="Dev"
# INSTANCE_IDS=$(aws ec2 describe-instances \
#   --region "$AWS_REGION" \
#   --filters "Name=tag:$TAG_KEY,Values=$TAG_VALUE" "Name=instance-state-name,Values=running" \
#   --query "Reservations[*].Instances[*].InstanceId" --output text)

# Stop instances
echo "Stopping instances: ${INSTANCE_IDS[@]}"
aws ec2 stop-instances --instance-ids ${INSTANCE_IDS[@]} --region "$AWS_REGION"

echo "Shutdown request sent at: $(date)"
```

---
### ⏰ **2. Automate with Cron (Linux/macOS)**
Edit crontab:

```bash
crontab -e
```

Add a daily 8PM shutdown (adjust time as needed):

```
0 20 * * * /path/to/shutdown_ec2.sh >> /var/log/ec2_shutdown.log 2>&1
```

---
### 🛡️ **IAM Permissions Required**
The script requires the following IAM permissions:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "ec2:StopInstances",
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": "ec2:DescribeInstances",
      "Resource": "*"
    }
  ]
}
```
---


