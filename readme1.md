# AWS 
# My_AWS_Note
Amazon Web Services as DevOps Enginner used in Real world:

1.AWS server List:

2.EC2

3.VPC

4.ELB

5.S3, S3FS,

6.IAM

7.AMI

8.RDS

9.Lambda

10.Cloud Watch, Cloud Trail, cloud Formation, Cloud Front

11.Autoscaling

12.Route53

13.AWS EKS & ECS , Openshift (Hands-on Experience)

14.Load balance ...ect!

---
**1.EC2:**
******
 Amazon Elastic Compute Cloud (Amazon EC2) is a web service that provides secure, resizable compute capacity in the cloud.
 Access reliable, scalable infrastructure on demand. Scale capacity within minutes with SLA commitment of 99.99% availability.
 Provide secure compute for your applications. Security is built into the foundation of Amazon EC2 with the AWS Nitro System.
 Optimize performance and cost with flexible options like AWS Graviton-based instances, Amazon EC2 Spot instances, and AWS Savings Plans.

---
**2.VPC:**
*****
A virtual private cloud is a virtual network that closely resembles a traditional networking that you operate in your own data centre, with the benefits of using the scalable infrastructure of AWS.
VPC is a virtual network of data center inside AWS for one client.
It is logically isolated from other virtual network in the AWS cloud.
 Maximum 5 VPC can be created in one region and 200 subnets in 1 VPC.
We can allocate maximum 5 Elastic IP.
 Once we created VPC, DHCP, NACL and security group will automatically created.
A VPC is confined to an AWS region and does not extend between regions.
Once the VPC is created you cannot change its CIDR block range.
 If you need a different CIDR size create a new VPC.
 The different subnets within a VPC cannot overlap.

---
**3.Elastic Load Balancing(ELB)**
******************************
Load balancing is the process of distributing incoming network traffic or computational workload across multiple resources, such as servers, to optimize resource utilization, improve performance, and ensure high availability of services.
Load balancers typically monitor the health and capacity of individual resources and direct traffic in a way that minimizes response time and maximizes throughput.
Types 
1.	Application Load Balancer
2.	Network Load Balancer.
3.	Gateway Load Balancer.
4.	Classic Load Balancer. 
---
**4. S3**
*********
Simple Storage Service is a scalable, Highly Available , Cost effective and secure cloud storage service provided by Amazon Web Services (AWS). 
It allows you to store and retrieve any amount of data from anywhere on the web.

(OR)

 Amazon Simple Storage Service (Amazon S3) is a scalable object storage service designed to store and retrieve any amount of data from anywhere on the web. It's commonly used to store files, backups, images, videos, and more.
It looks similar to your Google drive/ one drive and also allow unlimited amount of data (Highly scalable – Up to 5TD per file).

---
**5.IAM**
********
What is AWS IAM, and why is it important?

AWS IAM (Identity and Access Management) is a service provided by Amazon Web Services that helps you control access to your AWS resources. It allows you to manage user identities, permissions, and policies. 
You can IAM to control who is authenticated (Signed-In) and Authorized (has Permissions) to use resources.

************************************
why is it important?

IAM is important because it enhances security by ensuring that only authorized individuals or entities have access to your AWS resources, helping you enforce the principle of least privilege and maintain a secure environment.

***********************************
what is Authenticated and Authorization ?

	Authentication confirms that users are who they say they are. 
	Authorization gives those users permission to access a resource.
	While authentication and authorization might sound similar, they are distinct security processes in the world of identity and access management (IAM).

---
**6. IAM:**
********
 ==>An AMI (Amazon Machine Image) is essentially a pre-configured virtual machine that you can use as a template to launch EC2 (Elastic Compute Cloud) instances. AMIs can contain an operating system, application server, and pre-installed applications that you can use to quickly and easily launch an EC2 instance.

---
**7. RDS:**
************
==> Amazon Relational Database Service (Amazon RDS) is a web service that makes it easier to set up, operate, and scale a relational database in the AWS Cloud. It provides cost-efficient, resizable capacity for an industry-standard relational database and manages common database administration tasks.

---
**8. AWSLambda**
****************

==> Lambda is one of the most popular AWS services. It allows you to run code without servers, and you only pay when the service is actively being used. With Lambda, you no longer have to pay for idle server time or administer, operate, and wait for servers to be built to run your applications.

---
**9. AWS CloudWatch:**
****************
Amazon CloudWatch is a monitoring service for AWS cloud resources and your AWS-based applications. Amazon CloudWatch may be used to gather and track metrics, collect and monitor log files, create alarms, and automatically respond to changes in your AWS resources. 

---
**10. CloudTrail:**
*************************
==> AWS CloudTrail is an application program interface (API) call-recording and log-monitoring Web service offered by Amazon Web Services (AWS).
==> AWS CloudTrail allows AWS customers to record API calls, storing them in Amazon S3 buckets. API activity data included in the service includes the identity of an API caller, the time of the API call, the source of an API caller’s IP address, parameters of the API request and the response.

---
11. CloudFormation:
*************************
==> AWS CloudFormation is a service that helps users to set up their AWS resources. 
==> So they can spend less time managing those resources and more time focusing on their applications that run in AWS.
==> It enables developers to create and manage AWS resources in a declarative manner. 
==> For that able use JSON or YAML file called a CloudFormation template.

---
**12. AWS-Auto-Scaling:**
*************************
==> AWS Auto Scaling is a fully managed service, that allows you to provision and launch and terminate new instances as per demand. 
==> It monitors your applications and automatically adjusts capacity to maintain steady, predictable performance at the lowest possible cost. 
==> Using AWS Auto Scaling, it is easy to setup application scaling for multiple resources across multiple services in minutes.

**************
**13. Route 53:**
**************
==> You can use Route 53 in the Networking and Content Delivery section in AWS Console.
==> Route 53 is a highly available and scalable DNS web Service by Amazon.
==> It is a scalable (DNS) service that provides a reliable way to redirect traffic to applications. To achieve this domain names are translated to IP addresses to help computers connect better.
==> It is possible to connect queries to entities like Elastic Load Balancers in AWS using Amazon Route 53.

****************
**14. AWS-EKS**
**************
==> EKS (Elastic Kubernetes Service) is a managed Kubernetes service provided by AWS. With EKS, you can easily deploy and manage containerized applications using Kubernetes on AWS without needing to install, operate, and maintain your own Kubernetes control plane.

---

**15. ECS:**
************** 
==> ECS (Elastic Container Service) is a fully-managed container orchestration service that Amazon Web Services (AWS) provides.
==> It allows you to run and manage Docker containers on a cluster of virtual machines (EC2 instances) without having to manage the underlying infrastructure.

---
**16. Load-Balancing:**
**********************    
==> Load balancing is the distribution of workloads across multiple servers to ensure consistent and optimal resource utilization.
==> It is an essential aspect of any large-scale and scalable computing system, as it helps you to improve the reliability and performance of your applications.

---
