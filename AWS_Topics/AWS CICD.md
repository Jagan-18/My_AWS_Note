# AWS CI/CD (Continuous Integration / Continuous Delivery)
---
## 🚀 What is AWS CI/CD?
AWS CI/CD automates software build, test, and deployment workflows to help teams develop and deliver code reliably and rapidly. This approach streamlines releasing updates, improves quality, and minimizes manual errors through automation, feedback, and repeatable processes in the cloud.

- **Continuous Integration (CI):** Developers regularly merge code into a central repository, triggering automated builds and tests.

- **Continuous Delivery/Deployment (CD):** Successful builds proceed through automated testing and deployment stages, ready for release to production or pre-production environments—with optional manual approvals if required
<img width="940" height="454" alt="Image" src="https://github.com/user-attachments/assets/490cf3f1-f15d-4041-825b-82948b727b56" />

---
## ⚙️ CI vs CD:
| **Term**                                | **Meaning**                                                                |
| --------------------------------------- | -------------------------------------------------------------------------- |
| **CI (Continuous Integration)**         | Automate code builds and tests every time code is pushed (e.g., to GitHub) |
| **CD (Continuous Delivery/Deployment)** | Automatically deploy code to dev/test/staging/production environments      |

---
## CI vs. CD vs. Continuous Deployment:
| Concept                 | Focus                                            | Example AWS Tools           |
|-------------------------|--------------------------------------------------|-----------------------------|
| Continuous Integration  | Automated build, unit test on new code commits   | CodeBuild, CodePipeline     |
| Continuous Delivery     | Preps builds for deployment, approval steps      | CodeDeploy, CodePipeline    |
| Continuous Deployment   | Fully automates production deployments           | CodePipeline, CodeDeploy    |

---
## Key Features & Benefits:
- **Rapid, repeatable deployments** increase delivery velocity and reliability.
- **Reduced manual intervention** eliminates most human-driven errors.
- **Automated feedback** enables faster detection of bugs and integration failures.
- **Easy rollbacks** allow quick recovery from problematic releases.
- **Integrated monitoring & security** with AWS platforms for end-to-end governance.
- **Supports microservices, containers, and serverless** architectures.
---
## Core AWS CI/CD Service Suite:
| **Service**           | **Purpose**                                                               |
|-----------------------|---------------------------------------------------------------------------|
| **AWS CodeCommit**    | Managed Git-compatible source control repository for hosting code assets. |
| **AWS CodeBuild**     | On-demand build service to compile source code and run automated tests.   |
| **AWS CodePipeline**  | Orchestrates multi-stage pipelines for build, test, and deployment.       |
| **AWS CodeDeploy**    | Automates deployment to EC2, Lambda, ECS, or on-premises environments.    |
| **Amazon ECR**        | Managed Docker container registry for storing and managing images.        |
| **AWS CloudFormation**| Provisions infrastructure for CI/CD environments and apps using IaC.      |
| **CloudWatch**        | Logs, metrics, and alarms for pipeline monitoring                         |

These services can be integrated with popular third-party tools such as GitHub, Bitbucket, and Jenkins, offering flexibility for hybrid development environments.

---
## 📦 Example CI/CD Pipeline Flow:
**For a web application using AWS tools:**
1. **Developer pushes code to Git (CodeCommit / GitHub)**
2. **CodePipeline triggers build**
3. **CodeBuild compiles the code + runs unit tests**
4. **CodeDeploy deploys to EC2, Lambda, or ECS**
5. **Pipeline finishes — production updated**

> ✅ Optional: Use approval stages before deploying to production.

---
## Typical AWS CI/CD Pipeline:
1. **Source Stage:** Code is pushed to a repository (e.g., CodeCommit or GitHub).
2. **Build Stage:** Pipeline triggers CodeBuild or a similar service to compile code and run unit tests.
3. **Test Stage:** Additional automated tests validate code quality, security, and integration.
4. **Deploy Stage:** Passing artifacts are deployed to an environment (staging, production) using CodeDeploy or other deployment methods.
5. **Monitor & Rollback:** Application and pipeline health are monitored (e.g., via CloudWatch), with built-in rollback to recover from issues.
---
## 🧑‍💻 Use Case Example:
### Scenario: Node.js app deployed on EC2
* **Source**: GitHub repo connected to CodePipeline
* **Build**: CodeBuild compiles app and installs dependencies
* **Test**: Runs unit tests and checks for syntax
* **Deploy**: CodeDeploy installs the latest version on EC2 instances
* **Monitor**: CloudWatch tracks logs, errors, and deployment success

---

## 📜 Sample CI/CD YAML (CodeBuild `buildspec.yml`)

```yaml
version: 0.2
phases:
  install:
    runtime-versions:
      nodejs: 18
    commands:
      - echo Installing dependencies...
      - npm install
  build:
    commands:
      - echo Build started on `date`
      - npm run build
  post_build:
    commands:
      - echo Build completed on `date`
artifacts:
  files:
    - '**/*'
```
---
## ✅ Benefits of AWS CI/CD:
- Use **version control** (e.g., CodeCommit, GitHub) for all code and infrastructure definitions.
- Automate **build, test, and deploy** stages to maximize efficiency and quality.
- Integrate **approval and rollback steps** for risk management.
- Monitor pipeline health and deployments using **Amazon CloudWatch**.
- Apply **infrastructure as code** (CloudFormation, AWS CDK) for consistency and repeatability.
- Leverage modular infrastructure and service integrations for scalable and robust pipelines.

AWS CI/CD accelerates delivery, improves reliability, and empowers teams to adopt agile, DevOps, and modern software engineering practices in the AWS cloud environment.

---
## ⚠️ Top Disadvantages of AWS CI/CD:
1. **Steep Learning Curve**  
   - Requires knowledge of multiple AWS services and configurations.

2. **Complex IAM Setup**  
   - Misconfigured roles can cause security or access issues.

3. **Limited Multi-Cloud Support**  
   - AWS CI/CD tools are tightly bound to AWS; not ideal for hybrid environments.

4. **Initial Setup Effort**  
   - Building and connecting pipelines takes time and planning.

5. **Monitoring & Debugging Can Be Tricky**  
   - Requires integration with CloudWatch for visibility and troubleshooting.
---

# How does CodePipeline work?
> **AWS CodePipeline** orchestrates the flow of code changes through multiple stages of the software release process. Each stage represents a key step, such as source retrieval, build, testing, and deployment. Developers define the pipeline structure, specifying the sequence of stages and their associated actions. This enables end-to-end automation of the software delivery lifecycle, ensuring faster, consistent, and reliable releases.
---
# What's the difference between AWS CodePipeline and AWS CodeDeploy?

**CodePipeline** is the **orchestrator:** It defines the sequence of actions (source → build → test → deploy).

**CodeDeploy** is the **executor:** It performs the actual deployment when triggered by CodePipeline.

💡 Think of CodePipeline as the director of a play, and CodeDeploy as the actor performing the final scene

---
### 🛠️ **Difference Between CodePipeline and CodeDeploy**
| Feature                   | **AWS CodePipeline**                                                                                  | **AWS CodeDeploy**                                                                             |
| ------------------------- | ----------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| **Purpose**               | Orchestrates the entire CI/CD pipeline (source → build → test → deploy).                              | Handles the actual deployment of code to EC2, Lambda, or on-prem servers.                      |
| **Function**              | Automates end-to-end delivery workflow. Manages multiple stages like source, build, test, and deploy. | Automates just the deployment process, including rolling updates, blue/green deployments, etc. |
| **Scope**                 | High-level pipeline orchestration across various tools and services.                                  | Focused on managing and executing deployment strategies.                                       |
| **Integration**           | Integrates with CodeCommit, CodeBuild, Jenkins, GitHub, CloudFormation, etc.                          | Works with CodePipeline, GitHub, Jenkins, S3, and more to deploy the application.              |
| **Deployment Strategy**   | Doesn't deploy directly. Delegates to services like CodeDeploy or CloudFormation.                     | Supports advanced deployment strategies: in-place, blue/green, canary, and linear deployments. |
| **Monitoring & Rollback** | Coordinates but doesn’t directly manage rollback.                                                     | Offers detailed monitoring, rollback, and health checks during deployment.                     |

---

### 🚀 Quick Example:

Imagine you're deploying a web app:

* **CodePipeline**:

  1. Triggers on a code change in GitHub.
  2. Runs unit tests using CodeBuild.
  3. If successful, passes the artifact to **CodeDeploy**.

* **CodeDeploy**:

  1. Deploys the built artifact to EC2 instances.
  2. Performs health checks and rollbacks if needed.

---











