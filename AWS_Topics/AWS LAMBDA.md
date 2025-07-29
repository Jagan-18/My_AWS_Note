# AWS Lambda
---
# What is serverless computing? 
1.	Serverless computing is a cloud computing model where the cloud provider manages the infrastructure and dynamically allocates computing resources as needed. 
2.	This allows developers to write and deploy code without worrying about server management, scaling, or provisioning. 
3.	In serverless computing, the cloud provider is responsible for running and managing the servers, and the developer only pays for the compute time consumed by their code
4.	Serverless computing allows developers to focus on writing code and delivering business value without the overhead of managing infrastructure, leading to improved scalability, cost efficiency, and faster time-to-market for applications.

---
# 🟣  What is AWS Lambda?
1. AWS Lambda is a **serverless computing service provided** by Amazon Web Services (AWS). 
2. Users of AWS Lambda create functions, self-contained applications written in one of the supported languages and runtimes, and upload them to AWS Lambda, which executes those functions in an efficient and flexible manner.
3. The Lambda functions can perform any kind of computing task, **from serving web pages and processing streams of data to calling APIs and integrating with other AWS services.**

---

## 🔧 **How AWS Lambda Works**
* **Trigger-based execution**: You configure Lambda to automatically run code in response to events (like an S3 upload, API Gateway call, DynamoDB change, etc.).
* **Stateless functions**: Each invocation of a Lambda function is stateless and isolated.
* **Automatic scaling**: AWS handles scaling—invoking the function as many times as needed to handle the workload.
* **Short-lived**: Lambda is designed for short tasks (max **15 minutes per invocation**).

---
# What is default execution time for lambda?
1.	Default Execution Time: 3 seconds
2.	Max Execution Time: 15 minutes (900 seconds)
3.	Min Execution Time:1 millisecond

---
# What is an AWS Lambda function?
1. An AWS Lambda function is a piece of code that runs in response to events. 
2. It's a serverless compute service provided by Amazon Web Services (AWS) where you can upload your code and Lambda executes it in response to triggers such as changes to data in an S3 bucket, updates in a DynamoDB table, HTTP requests via API Gateway, or events from other AWS services.

#### Key characteristics of AWS Lambda functions include:
1.	Serverless Code: A piece of code that runs in response to events.
2.	Event-Driven: Triggered by events like changes in data, HTTP requests, or scheduled tasks.
3.	Managed Compute: AWS handles the infrastructure, scaling, and availability.
4.	Multiple Languages: Supports languages like Node.js, Python, Java, etc.
5.	Pay-Per-Use: You pay based on compute time and requests.

---
## 🧩 **Key Components**

| Component                | Description                                                                                  |
| ------------------------ | -------------------------------------------------------------------------------------------- |
| **Function**             | The actual code you want to run.                                                             |
| **Event Source**         | The AWS service/event that triggers the function (e.g., S3, API Gateway, CloudWatch).        |
| **Runtime**              | Lambda supports multiple runtimes like Node.js, Python, Java, Go, .NET, and custom runtimes. |
| **Execution Role (IAM)** | IAM Role assigned to Lambda for permissions to access other AWS resources.                   |
| **Layers**               | Used to manage shared libraries and code across multiple Lambda functions.                   |
| **Concurrency**          | Number of executions that can run in parallel. You can set limits.                           |

---
## 💼 **Common Use Cases**
* **Web backend** via API Gateway
* **Real-time file processing** (e.g., resize images after S3 upload)
* **Automated tasks** (e.g., CloudWatch alarms, CRON jobs)
* **ETL** (Extract, Transform, Load) in Data Pipelines
* **Chatbots or voice services**
* **Security automation** (e.g., auto-remediate IAM policies)

---
## ✅ Benefits of using AWS Lambda:
1.	**Serverless Architecture:** No need to provision or manage servers. AWS Lambda handles all infrastructure management.
2.	**Cost-Effective:** Pay only for the compute time consumed by your functions, with no charges when code is idle.
3.	**Automatic Scaling:** Scales automatically in response to incoming traffic, ensuring high availability and performance.
4.	**Integrations:** Easily integrates with other AWS services, simplifying the development of event-driven applications.
5.	**Flexibility:** Supports multiple programming languages and allows for custom runtimes, giving developers flexibility in coding.


---
## ⚠️ Limitations of AWS Lambda:
1.	Execution Duration: Limited to a maximum of 15 minutes per invocation.
2.	Memory and CPU: Functions are limited by allocated memory and CPU resources.
3.	Stateless: Functions are stateless, so they don't retain data between invocations.
4.	Cold Starts: Occurs when a function is invoked after being idle, leading to increased latency for the first request.

---
## 🔁 **Lambda Execution Flow (Simplified)**

```
Event → Triggered Lambda → Code executes → Returns result (or stores to DB, S3, etc.)
```
---
## 🛠️ **Basic Example (Python Lambda triggered by S3)**
```python
def lambda_handler(event, context):
    bucket = event['Records'][0]['s3']['bucket']['name']
    file_key = event['Records'][0]['s3']['object']['key']
    print(f"New file uploaded: {file_key} in bucket {bucket}")
    return {
        'statusCode': 200,
        'body': f"File {file_key} processed successfully."
    }
```
---
# What languages does AWS Lambda support?
AWS Lambda natively supports Java, Go, PowerShell, Node.js, C#, Python, and Ruby code, and provides a Runtime API which allows you to use any additional programming languages to author your functions. Please read our documentation on using **Node.js, Python, Java, Ruby, C#, Go, and PowerShell.**

---
## How does AWS Lambda secure my code?
AWS Lambda stores code in Amazon S3 and encrypts it at rest. AWS Lambda performs additional integrity checks while your code is in use.


---
## Real-World Use Cases
Now, let's explore some real-world use cases to better understand how AWS Lambda can be applied:

**1.Automated Image Processing:** Imagine you have a photo-sharing app, and users upload images every day. You can use Lambda to automatically resize or compress these images as soon as they are uploaded to S3.

**2.Chatbots and Virtual Assistants:** Build interactive chatbots or voice-controlled virtual assistants using Lambda. These assistants can perform tasks like answering questions, fetching data, or even controlling smart home devices.

**3.Scheduled Data Backups:** Use Lambda to create scheduled tasks for backing up data from one storage location to another, ensuring data resilience and disaster recovery.

**4. Real-Time Analytics:** Lambda can process streaming data from IoT devices, social media, or other sources, allowing you to perform real-time analytics and gain insights instantly.

**5. API Backends:** Develop scalable API backends for web and mobile applications using Lambda. It automatically handles the incoming API requests and executes the corresponding functions.

---
# How Lambda Functions Fit into the Serverless World
At the heart of AWS Lambda are "Lambda functions." These are individual units of code that perform specific tasks. Think of them as small, single-purpose applications that run independently.

**Here's how Lambda functions fit into the serverless world:**

**1.Event-Driven Execution:** Lambda functions are triggered by events. An event could be anything, like a new file being uploaded to Amazon S3, a request hitting an API, or a specific time on the clock. When an event occurs, Lambda executes the corresponding function.

**2.No Server Management:** As a developer, you don't need to worry about managing servers. AWS handles everything behind the scenes. You just upload your code, configure the trigger, and Lambda takes care of the rest.

**3.Automatic Scaling:** Whether you have one user or one million users, Lambda scales automatically. Each function instance runs independently, ensuring that your application can handle any level of incoming traffic without manual intervention.

**4.Pay-per-Use:** One of the most attractive features of serverless computing is cost efficiency. With Lambda, you pay only for the compute time your code consumes. When your code isn't running, you're not charged.

**5.Supported Languages:** Lambda supports multiple programming languages like Node.js, Python, Java, Go, and more. You can choose the language you are comfortable with or that best fits your application's needs.

---

# 🧠  HOW DEVOPS ENGINEERS USE SERVERLESS ARCHITECTURE ?
**Serverless** means you **don’t manage servers** — cloud providers like AWS automatically provision, scale, and manage the infrastructure. You focus **only on code and logic**, and you’re billed **per execution or usage**, not uptime.

---
## 🔧 **How DevOps Engineers Use Serverless Architecture**
#### ✅ 1. **Automating CI/CD Pipelines**

* **Lambda + CodePipeline + CodeBuild**:

  * Run build, test, and deployment steps using **serverless services**.
  * Example: Trigger a Lambda function to validate code or deploy when new code is pushed to GitHub.
* **Serverless Framework**, **SAM (Serverless Application Model)**, or **Terraform** used for IaC.

---
#### ✅ 2. **Event-Driven Automation**
* DevOps teams often set up **event-based triggers** using Lambda:

  * Auto-tagging EC2 or S3 resources.
  * Auto-remediating security violations (like public S3 buckets).
  * Cleaning up unused resources daily.

---
#### ✅ 3. **Infrastructure as Code (IaC)**
* Use **AWS CloudFormation or Terraform** to deploy **serverless stacks**:

  * APIs (API Gateway)
  * Functions (Lambda)
  * Storage (S3)
  * Databases (DynamoDB)

Example: Deploying a whole monitoring app with 1 command.

---
#### ✅ 4. **Monitoring & Logging**
* Use **CloudWatch + Lambda** to:

  * Auto-restart services based on metrics.
  * Send alerts (e.g., Slack notifications for failed deployments).
  * Parse and push logs to S3, Elasticsearch, or external tools.

---
### ✅ 5. **Scheduled Tasks / Cron Jobs**
* Replace traditional cron jobs with **CloudWatch Events + Lambda**:

  * Run nightly backups.
  * Rotate IAM keys.
  * Sync data between services.

---
### ✅ 6. **Microservices / APIs**
* DevOps can design **REST APIs** using:

  * **API Gateway** (frontend)
  * **Lambda** (backend logic)
  * **DynamoDB / RDS** (database)

Great for internal tools, dashboards, and automation portals.

---
### ✅ 7. **Serverless CI/CD for Containers**
* Use **AWS Fargate** (serverless containers) with:

  * ECS (Elastic Container Service)
  * GitHub Actions / CodePipeline

Build, scan, and deploy containerized apps **without managing EC2 instances**.

---
## 📦 **Popular Serverless Services Used by DevOps Engineers**
| Service                | Purpose                            |
| ---------------------- | ---------------------------------- |
| **AWS Lambda**         | Run custom scripts and automation  |
| **Amazon S3**          | Store artifacts, backups, and logs |
| **API Gateway**        | Trigger Lambda via REST APIs       |
| **DynamoDB**           | Store job statuses, config data    |
| **AWS Step Functions** | Orchestrate complex workflows      |
| **CloudWatch**         | Logging, monitoring, alerts        |
| **SNS / SQS**          | Messaging and notifications        |
| **Fargate**            | Run containers serverlessly        |

---
## 🧪 **Real-World Use Case**
#### 🔁 *Automated Backup System*

* **Trigger**: CloudWatch Event at 1 AM daily.
* **Lambda**: Script to snapshot RDS and copy it to S3.
* **S3 Lifecycle Rules**: Auto-delete after 30 days.
* **CloudWatch Alarm**: Notify via SNS if Lambda fails.

No servers. Fully automated. Costs <\$1/month.

---

