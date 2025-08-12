# Install EKS

Please follow the prerequisites doc before this.

## Install using Fargate

```
eksctl create cluster --name demo-cluster --region us-east-1 --fargate
```

## Delete the cluster

```
eksctl delete cluster --name demo-cluster --region us-east-1
```

---

# View points for refe:

## **Installing EKS on AWS**

> This guide walks through creating and configuring an Amazon EKS (Elastic Kubernetes Service) cluster from scratch using **eksctl**.

---
## **1. Prerequisites**

Before you start, make sure you have:

* **AWS CLI** installed & configured:

```bash
aws configure
```

* **kubectl** installed:

```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl && sudo mv kubectl /usr/local/bin/
```

* **eksctl** installed:

```bash
curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
sudo mv /tmp/eksctl /usr/local/bin
```

* **IAM permissions** to create EKS, VPC, EC2, IAM roles, and security groups.

---
## **2. Create an EKS Cluster**

Run:

```bash
eksctl create cluster \
  --name my-eks-cluster \
  --version 1.29 \
  --region ap-south-1 \
  --nodegroup-name linux-nodes \
  --node-type t3.medium \
  --nodes 2 \
  --nodes-min 2 \
  --nodes-max 4 \
  --managed
```

**What this does:**

* Creates a VPC with public & private subnets.
* Deploys an EKS control plane.
* Creates a managed node group.

---
## **3. Verify Cluster**

```bash
aws eks list-clusters --region ap-south-1
kubectl get nodes
```

---
## **4. Update kubeconfig**

```bash
aws eks update-kubeconfig --name my-eks-cluster --region ap-south-1
```

Now `kubectl` commands will target your new cluster.

---

## **5. Deploy a Test App**

Example:

```bash
kubectl create deployment hello-world --image=nginx
kubectl expose deployment hello-world --type=LoadBalancer --port=80
kubectl get svc hello-world
```

---
## **6. Install AWS Load Balancer Controller (For Ingress)**

```bash
helm repo add eks https://aws.github.io/eks-charts
helm upgrade --install aws-load-balancer-controller eks/aws-load-balancer-controller \
  --set clusterName=my-eks-cluster \
  --set serviceAccount.create=false \
  --set serviceAccount.name=aws-load-balancer-controller \
  -n kube-system
```

---
## **7. Delete Cluster**
If you no longer need it:

```bash
eksctl delete cluster --name my-eks-cluster --region ap-south-1
```
---
✅ **You now have a working EKS cluster.**
From here, you can deploy apps, set up Ingress, or integrate with CI/CD.
---

