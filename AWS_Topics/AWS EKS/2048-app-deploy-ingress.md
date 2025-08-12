# 2048 App

## Create Fargate profile

```
eksctl create fargateprofile \
    --cluster demo-cluster \
    --region us-east-1 \
    --name alb-sample-app \
    --namespace game-2048
```

## Deploy the deployment, service and Ingress

```
kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.5.4/docs/examples/2048/2048_full.yaml
```



![Screenshot 2023-08-03 at 7 57 15 PM](https://github.com/iam-veeramalla/aws-devops-zero-to-hero/assets/43399466/93b06a9f-67f9-404f-b0ad-18e3095b7353)

---
# View Referal points

Gotcha — you’re talking about deploying the **2048 sample app** to **EKS** with **Ingress** (so it’s accessible via an AWS ALB or similar).
I’ll walk you through the **full setup** — container, service, ingress — exactly how DevOps engineers would do it.

---

## **1️⃣ Overview**

We’ll:

1. Deploy the 2048 app on EKS.
2. Create a Kubernetes **Deployment** + **Service**.
3. Expose it with **Ingress** using AWS Load Balancer Controller.

---

## **2️⃣ Prerequisites**

* EKS cluster running.
* `kubectl` configured (`aws eks update-kubeconfig`).
* AWS Load Balancer Controller installed:

```bash
helm repo add eks https://aws.github.io/eks-charts
helm upgrade --install aws-load-balancer-controller eks/aws-load-balancer-controller \
  --set clusterName=my-eks-cluster \
  --set serviceAccount.create=false \
  --set serviceAccount.name=aws-load-balancer-controller \
  -n kube-system
```

---

## **3️⃣ Kubernetes Manifests**

### **a) Deployment**

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: game-2048
  labels:
    app: game-2048
spec:
  replicas: 2
  selector:
    matchLabels:
      app: game-2048
  template:
    metadata:
      labels:
        app: game-2048
    spec:
      containers:
      - name: game-2048
        image: alexwhen/docker-2048
        ports:
        - containerPort: 80
```

---

### **b) Service**

```yaml
apiVersion: v1
kind: Service
metadata:
  name: game-2048-service
spec:
  type: NodePort
  selector:
    app: game-2048
  ports:
    - port: 80
      targetPort: 80
```

---

### **c) Ingress**

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: game-2048-ingress
  annotations:
    kubernetes.io/ingress.class: alb
    alb.ingress.kubernetes.io/scheme: internet-facing
    alb.ingress.kubernetes.io/target-type: ip
    alb.ingress.kubernetes.io/listen-ports: '[{"HTTP":80}]'
spec:
  rules:
    - host: game2048.example.com  # Replace with your domain
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: game-2048-service
                port:
                  number: 80
```

---

## **4️⃣ Deployment Steps**

```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
kubectl apply -f ingress.yaml
```

---

## **5️⃣ Verify**

* Run:

```bash
kubectl get ingress
```

* You’ll get an **ALB DNS name**.
* Point your domain (optional) to that ALB in Route53.

---

## **6️⃣ Notes**

* The ALB is created automatically by AWS Load Balancer Controller.
* If you don’t have a domain, you can use the ALB DNS directly.
* For HTTPS, you’d add:

  ```yaml
  alb.ingress.kubernetes.io/certificate-arn: arn:aws:acm:...
  alb.ingress.kubernetes.io/listen-ports: '[{"HTTP":80,"HTTPS":443}]'
  ```

---
