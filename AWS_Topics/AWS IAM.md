# AWS IAM (Identity and Access Management)

**Root user** – Account Owner that performs tasks requiring. (Admin)
**IAM** --> User within an account that performs daily tasks. (Other's)

# User, policies and groups and roles
---
# AWS Security: 
AWS Security refers to a range of qualities, tools, or features that make the public cloud service provider Amazon Web Services (AWS) secure.
There are many types of security services available but some of them are widely used by AWS, such as:
1. IAM
2. Key Management System (KMS)
3. Cognito
4. Web Access Firewall (WAF)

---
# ✅ IAM (Identity and Access Management):
------------------------------------------
**AWS IAM (Identity and Access Management)** is a **web service** that helps you **securely control access** to AWS resources.

* It allows you to manage **users**, **permissions**, and **roles**,It allows you to grant access to the different parts of the AWS platform.
* IAM controls **who is authenticated** (signed in) and **authorized** (has permission) to use resources.

---
## ✅ Key Functions of IAM:

* **Manage users** and their level of access to the AWS Console.
* **Grant access** to specific AWS services and resources.
* Create and assign **roles** for applications and services to access AWS securely.
* Enforce **security policies** like MFA, password policies, and access key rotation.

---

## ✅ Authentication vs Authorization
-----------------------------------------------------------------------------------------
| **Term**           | **Definition**                                                   |
| ------------------ | ---------------------------------------------------------------- |
| **Authentication** | Confirms **who the user is**. It verifies identity.              |
| **Authorization**  | Determines **what the user can do** after they're authenticated. |
-----------------------------------------------------------------------------------------

### 🔐 What is Authentication?

Authentication is the process of verifying that someone is who they claim to be. It's the **first step** in any security process.

**Examples of authentication methods:**
*  **Passwords** Usernames and passwords are the most common authentication factors. If a user enters the correct data, the system assumes the identity is valid and grants access.
*  **One-time pins.** Grant access for only one session or transaction.
*  **Authentication apps**. Generate security codes via an outside party that grants access. (e.g., Google Authenticator)
*  **Biometrics.** A user presents a fingerprint or eye scan to gain access to the system.


### 🔒 What is Authorization?
1. Authorization in system security is the process of giving the user permission to access a specific resource or function. This term is often used interchangeably with access control or client privilege.
2. Giving someone permission to download a particular file on a server or providing individual users with administrative access to an application are good examples of authorization.
3. In secure environments, authorization must always follow authentication. Users should first prove that their identities are genuine before an organization’s administrators grant them access to the requested resources.

---
## ✅ IAM  Key Components:
- **Users**: Individual identities with credentials (passwords, access keys) for AWS account access.
- **Groups**: Collections of users sharing common permissions, simplifying management.
- **Roles**: Identities with specific permissions that can be assumed by users, AWS services, or external entities.
- **Policies**: JSON documents that define permissions, specifying allowed or denied actions on AWS resources.

----

#### 👤 **Users** - IAM users represent individual people or entities (such as applications or services) that interact with your AWS resources. Each user has a unique name and security credentials (password or access keys) used for authentication and access control.
---

#### 🧑‍🤝‍🧑 **Groups** - IAM groups are collections of users with similar access requirements. Instead of managing permissions for each user individually, you can assign permissions to groups, making it easier to manage access control. Users can be added or removed from groups as needed.
---
#### 🎭 **Roles**: IAM roles are used to grant temporary access to AWS resources. Roles are typically used by applications or services that need to access AWS resources on behalf of users or other services. Roles have associated policies that define the permissions and actions allowed for the role.
---
#### 📜 **Policies**: IAM policies are JSON documents that define permissions. Policies specify the actions that can be performed on AWS resources and the resources to which the actions apply. Policies can be attached to users, groups, or roles to control access. IAM provides both AWS managed policies (predefined policies maintained by AWS) and customer managed policies (policies created and managed by you).
---

**Example Policy (Allow read-only access to EC2):**

```json
{
  "Version": "2012-10-17",
  "Statement": [{
    "Effect": "Allow",
    "Action": "ec2:DescribeInstances",
    "Resource": "*"
  }]
}
```
---
## How IAM Works (End-to-End)
1. **Account Setup**: Start with the root user, but create individual IAM users for daily tasks.
2. **User Creation**: Add users for each person or application needing access.
3. **Group Assignment**: Organize users into groups (e.g., Admins, Developers) and attach relevant policies.
4. **Policy Management**: Write or use AWS managed policies to define permissions. Attach policies to users, groups, or roles.
5. **Role Creation**: Create roles for specific tasks (e.g., EC2 access, cross-account access) and assign trust relationships.
6. **Authentication**: Users sign in with credentials; enable Multi-Factor Authentication (MFA) for extra security.
7. **Authorization**: IAM evaluates policies to determine if a request is allowed or denied.
8. **Monitoring & Auditing**: Use AWS CloudTrail and IAM Access Analyzer to monitor activity and review permissions.
9. **Best Practices**: Apply least privilege, rotate credentials, and regularly review permissions.

## Common Tasks
- Create users and groups.
- Attach policies to users, groups, or roles.
- Enable multi-factor authentication (MFA).
- Use roles for cross-account and service access.
- Audit permissions and activity.

## Example Policy
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "s3:ListBucket",
            "Resource": "arn:aws:s3:::example-bucket"
        }
    ]
}
```
---
## ✅ Tasks That Require Root User Credentials: 

Some AWS actions **can only be performed by the root user** (the account owner). These tasks involve **account-level configuration** and **critical recovery** actions:

1. **Change Account Settings**

   * Includes: account name, root email address, root user password, and root access keys.
   * Note: Other settings like contact info, billing preferences, and regions **do not** require root credentials.

2. **Restore IAM User Permissions**

   * If an IAM admin accidentally removes their own permissions, only the **root user** can sign in to **modify or reassign policies** and restore access.

3. **Activate IAM Access to the Billing Console**

   * Required to let IAM users access the **Billing and Cost Management Dashboard**.
   * Only the root user can enable this.
   * IAM users with `aws-portal:ViewBilling` can view **certain tax invoices**, but **some invoices (e.g., from AISPL or AWS Inc.) require root access**.

---

## ✅ Types of IAM Policies

IAM policies define what actions are allowed or denied for a user, group, or role. There are **three main types**:

### 1. **AWS Managed Policies**

* Created and maintained by AWS.
* You can **attach them directly** to users, groups, or roles.
* These are **read-only**, and updated automatically by AWS as needed.
* Each policy has its own **ARN** (Amazon Resource Name).

 **Example:** `AmazonS3ReadOnlyAccess`, `AmazonEC2FullAccess`

---
### 2. **Customer Managed Policies**

* Created and managed by **you (the customer)**.
* These are also **standalone policies** that you can reuse across multiple IAM entities (users, groups, roles).
* Created via the **AWS Management Console**, **CLI**, or **IAM API**.

**Best when you need:**

* Custom permissions
* Fine-grained access control
* Reusable policy logic
---
### 3. **AWS Managed Job Function Policies**

* Predefined policies created by AWS for **specific job roles**.
* Designed for common roles like **developer**, **database admin**, **network operator**, etc.
* Help reduce mistakes by giving only the required permissions for a role.
---
## ✅ What is an Inline Policy?

* An **inline policy** is a policy **embedded directly into a single IAM identity** (user, group, or role).
* It has a **1:1 relationship** with that identity — it cannot be reused or shared.
* When the identity is deleted, the policy is also deleted.
* Best used when permissions are **specific and unique** to one user or role.

> 🔹 If a policy could apply to more than one user or role, use a **managed policy** instead.
---

## ✅ What is a Permissions Boundary in IAM?
* A **permissions boundary** is an **advanced security control** that sets the **maximum permissions** an IAM identity (user or role) can have.
* Even if the identity has policies that allow actions, it **cannot exceed** the limits defined in the permissions boundary.
* It’s useful in scenarios like **delegated admin control**, **cross-account roles**, or **service control policies (SCPs)**.

> 🔐 **Effective Permissions = Identity Policy ∩ Permissions Boundary**

---

## ✅ Summary

| Concept                     | Description                                                                            |
| --------------------------- | -------------------------------------------------------------------------------------- |
| **Root User Tasks**         | Critical account tasks like restoring access, billing setup, changing root credentials |
| **AWS Managed Policy**      | Ready-to-use, maintained by AWS                                                        |
| **Customer Managed Policy** | Custom policy you create and manage                                                    |
| **Job Function Policy**     | Role-based policy (e.g., Developer, DB Admin)                                          |
| **Inline Policy**           | One-to-one policy embedded in a specific user/group/role                               |
| **Permissions Boundary**    | Defines **max permissions** an IAM entity can ever have                                |

---


