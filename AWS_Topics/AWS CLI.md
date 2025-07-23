# AWS Command Line Interface (AWS CLI)

## ✅ What is AWS CLI?

**AWS CLI** is a **command-line tool** that allows you to **manage AWS services** by issuing commands in your terminal or scripts instead of using the AWS Management Console. It supports all AWS services and is ideal for automation, scripting, and CI/CD workflows.

**OR**

The **AWS Command Line Interface (AWS CLI)** is a unified tool that enables you to manage and automate AWS services and resources directly from your command line or terminal. With a single installation, you can configure the CLI to interact with more than 200 AWS services, making it a powerful asset for developers, DevOps engineers, and system administrators.

## Key Features:
- **Unified Management:** Control all AWS services from one terminal tool.
- **Automation:** Automate repetitive tasks and scripts for provisioning, deployment, and management.
- **Scripting Support:** Easily integrate AWS operations into shell or batch scripts.
- **Credential Management:** Use AWS credentials and profiles for secure access without repeatedly logging in.
- **Customization:** Output in multiple formats (JSON, text, table) for scripting and readability.
- **Multi-platform:** Available on Windows, macOS, and Linux.

---
# Why would you use the AWS CLI?
The AWS CLI provides a convenient way to automate tasks, manage AWS resources, and interact with services directly from the command line, making it useful for scripting and administration.

---
## Installation
You can install the AWS CLI on major operating systems using simple steps. Below is a summarized guide:

### For Windows
1. Download the **MSI installer** from the official AWS website.
2. Run the installer and complete the setup.
3. Confirm installation with:
   ```
   aws --version
   ```

### For Linux/macOS

1. Use `curl` to download the installation bundle:
   ```
   curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
   unzip awscliv2.zip
   sudo ./aws/install
   ```
2. Verify installation:
   ```
   aws --version
   ```
### For Source Installation:
Advanced users can build and install the AWS CLI from source for greater customization.

## Configuration
To start using the AWS CLI, configure your credentials:

```
aws configure
```
You'll be prompted for:
- **AWS Access Key ID**
- **AWS Secret Access Key**
- **Default region name (e.g., us-east-1)**
- **Default output format (json, text, table)**

These are saved in `~/.aws/credentials` and `~/.aws/config`.

## Common Usage Examples:
| Service     | Command Example                                                                                             | Description                          |
|-------------|-------------------------------------------------------------------------------------------------------------|--------------------------------------|
| EC2         | `aws ec2 run-instances --instance-type t2.micro --image-id ami-xxxxxx --region us-east-1`                   | Launch an EC2 instance               |
| S3          | `aws s3 ls``aws s3 cp file.txt s3://mybucket/`                                                              | List bucketsCopy files to S3         |
| IAM         | `aws iam create-user --user-name newuser`                                                                   | Create a new IAM user                |
| DynamoDB    | `aws dynamodb list-tables --region us-west-2`                                                               | List DynamoDB tables                 |
| CloudWatch  | `aws cloudwatch describe-alarms`                                                                            | List CloudWatch alarms               |
| Route 53    | `aws route53 list-hosted-zones``aws route53 create-hosted-zone --name example.com`                          | List/create Route 53 hosted zones    |
| RDS         | `aws rds create-db-snapshot --db-snapshot-identifier snap1 --db-instance-identifier db1`                    | Create DB snapshot                   |

## Benefits: 
- **Time Savings:** Rapidly perform complex operations with few commands[2][3].
- **Consistency:** Uniform command structure across services.
- **Integration:** Seamless integration with CI/CD pipelines and other automation tools.
- **Scalability:** Efficiently manage small to large-scale AWS environments from the terminal[2][3].


---
## 📘 Common AWS CLI Commands:

### ✅ S3 Commands
```bash
aws s3 ls                         # List all buckets
aws s3 mb s3://my-bucket          # Make bucket
aws s3 cp myfile.txt s3://my-bucket/   # Upload file
aws s3 sync ./backup s3://my-bucket/backup/  # Sync directory
```
---
### ✅ EC2 Commands
```bash
aws ec2 describe-instances
aws ec2 start-instances --instance-ids i-1234567890abcdef0
aws ec2 stop-instances --instance-ids i-1234567890abcdef0
```
---
### ✅ IAM Commands
```bash
aws iam list-users
aws iam create-user --user-name testuser
```
---
### ✅ CloudWatch Logs

```bash
aws logs describe-log-groups
aws logs get-log-events \
  --log-group-name "/aws/lambda/my-function" \
  --log-stream-name "2023/07/20/[$LATEST]abc123"
```
---
## 📌 AWS CLI Output Formats

* `json` (default)
* `table` (for human-readable tables)
* `text` (compact plain text)

Example:

```bash
aws ec2 describe-instances --output table
```

---
## 🧠 AWS CLI Profiles (Multiple Accounts)
You can create multiple profiles:

```bash
aws configure --profile dev
aws configure --profile prod
```

Then use:
```bash
aws s3 ls --profile dev
```

---
## 🛡️ Security Tip

Use **IAM roles** on EC2 instead of embedding long-term access keys in scripts.

---
## 🧪 Example: Create EC2 Instance via CLI:
```bash
aws ec2 run-instances \
  --image-id ami-0abcdef1234567890 \
  --instance-type t2.micro \
  --key-name my-key \
  --security-group-ids sg-0123456789abcdef0 \
  --subnet-id subnet-0123456789abcdef0
```
---
## 🤖 Use in Bash Scripts (Automation Example)
```bash
#!/bin/bash

DATE=$(date +%F)
FILE="/backup/db-${DATE}.sql"

mysqldump -u root -pMyPass mydb > $FILE

aws s3 cp $FILE s3://my-backup-bucket/db-backups/
```
---

