# prerequisites

**1. kubectl** – A command line tool for working with Kubernetes clusters. For more information, see Installing or updating kubectl.

**2. eksctl** – A command line tool for working with EKS clusters that automates many individual tasks. For more information, see Installing or updating.

**3. AWS CLI** – A command line tool for working with AWS services, including Amazon EKS. For more information, see Installing, updating, and uninstalling the AWS CLI in the AWS Command Line Interface User Guide. After installing the AWS CLI, we recommend that you also configure it. For more information, see Quick configuration with aws configure in the AWS Command Line Interface User Guide.


----

Got it — here’s a **complete `prerequisites.md`** for your EKS installation guide, designed so anyone following it can set up their environment without surprises.

---
# **EKS Prerequisites**
Before installing Amazon EKS, make sure the following prerequisites are met.

---
## **1. AWS Account**

* You need an active AWS account.
* Ensure you have **IAM permissions** to create:

  * EKS clusters
  * VPCs
  * Fargate profiles
  * IAM roles

---
## **2. Install AWS CLI**

**Check if installed:**

```bash
aws --version
```

If not installed, [download AWS CLI v2](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html).

**Configure AWS CLI:**

```bash
aws configure
```

Enter:

* **AWS Access Key ID**
* **AWS Secret Access Key**
* **Default region name**
* **Output format** (e.g., `json`)

---
## **3. Install eksctl**
`eksctl` is a command-line tool for creating EKS clusters.

**Check if installed:**

```bash
eksctl version
```

**Install (Linux/macOS):**

```bash
curl --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
sudo mv /tmp/eksctl /usr/local/bin
```

**Windows:**
[Download eksctl binary](https://github.com/weaveworks/eksctl/releases/latest).

---
## **4. Install kubectl**

`kubectl` is the Kubernetes CLI to interact with your EKS cluster.

**Check if installed:**

```bash
kubectl version --client
```

**Install (Linux/macOS):**

```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl
sudo mv kubectl /usr/local/bin
```

**Windows:**
[Download kubectl binary](https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/).

---
## **5. Verify IAM Role Permissions**

Ensure your IAM user/role has at least:

* `AmazonEKSClusterPolicy`
* `AmazonEKSServicePolicy`
* `AmazonEKSFargatePodExecutionRolePolicy`
* `AmazonVPCFullAccess`
* `IAMFullAccess`

---
✅ **Once all these are done, proceed to [Install EKS](./installing-eks.md)**.
---

If you want, I can now create **`2048-app-deploy-ingress.md`** so that after installing EKS you can deploy a working sample app with ingress.
That would make your guide end-to-end instead of just cluster creation.


