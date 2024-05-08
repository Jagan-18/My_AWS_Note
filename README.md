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



1.EC2:
******
 Amazon Elastic Compute Cloud (Amazon EC2) is a web service that provides secure, resizable compute capacity in the cloud.
 Access reliable, scalable infrastructure on demand. Scale capacity within minutes with SLA commitment of 99.99% availability.
 Provide secure compute for your applications. Security is built into the foundation of Amazon EC2 with the AWS Nitro System.
 Optimize performance and cost with flexible options like AWS Graviton-based instances, Amazon EC2 Spot instances, and AWS Savings Plans.


2.VPC:
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




3.Elastic Load Balancing(ELB)
******************************
Load balancing is the process of distributing incoming network traffic or computational workload across multiple resources, such as servers, to optimize resource utilization, improve performance, and ensure high availability of services.
Load balancers typically monitor the health and capacity of individual resources and direct traffic in a way that minimizes response time and maximizes throughput.
Types 
1.	Application Load Balancer
2.	Network Load Balancer.
3.	Gateway Load Balancer.
4.	Classic Load Balancer. 



4. S3
*****
Simple Storage Service is a scalable, Highly Available , Cost effective and secure cloud storage service provided by Amazon Web Services (AWS). 
It allows you to store and retrieve any amount of data from anywhere on the web.

(OR)

 Amazon Simple Storage Service (Amazon S3) is a scalable object storage service designed to store and retrieve any amount of data from anywhere on the web. It's commonly used to store files, backups, images, videos, and more.
It looks similar to your Google drive/ one drive and also allow unlimited amount of data (Highly scalable – Up to 5TD per file).


5.IAM
********

What is AWS IAM, and why is it important?

AWS IAM (Identity and Access Management) is a service provided by Amazon Web Services that helps you control access to your AWS resources. It allows you to manage user identities, permissions, and policies. 
You can IAM to control who is authenticated (Signed-In) and Authorized (has Permissions) to use resources.

===========================================================================================
why is it important?

IAM is important because it enhances security by ensuring that only authorized individuals or entities have access to your AWS resources, helping you enforce the principle of least privilege and maintain a secure environment.

===========================================================================================
what is Authenticated and Authorization ?

	Authentication confirms that users are who they say they are. 
	Authorization gives those users permission to access a resource.
	While authentication and authorization might sound similar, they are distinct security processes in the world of identity and access management (IAM).


********
#IAM:
********
 ==>An AMI (Amazon Machine Image) is essentially a pre-configured virtual machine that you can use as a template to launch EC2 (Elastic Compute Cloud) instances. AMIs can contain an operating system, application server, and pre-installed applications that you can use to quickly and easily launch an EC2 instance.




