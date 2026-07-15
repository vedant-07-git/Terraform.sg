# 🚀 Terraform Zero to Hero – Module 1: Infrastructure as Code (IaC)

> **Learning Terraform from Zero to Hero** 🚀
> This repository contains my Terraform learning notes, practical examples, interview preparation, and hands-on labs.

---

## 📚 Module 1: Infrastructure as Code (IaC)

### 📌 Topics Covered

* What is Infrastructure?
* What is Infrastructure as Code (IaC)?
* Why IaC is Needed
* Problems with Manual Infrastructure
* Benefits of IaC
* IaC Tools Comparison

  * Terraform
  * AWS CloudFormation
  * Ansible
  * Pulumi

---

# 1️⃣ What is Infrastructure?

## Definition

**Infrastructure** is the collection of resources required to run an application or website.

It includes both **hardware** and **software** resources.

### Infrastructure Components

* 🖥️ EC2 (Server)
* 🌐 Virtual Machine (VM)
* 🌍 VPC (Network)
* 💾 Storage (EBS, S3)
* 🗄️ Database (RDS)
* ⚖️ Load Balancer
* 🔒 Security Groups
* 👤 IAM Users & Roles
* 🌎 DNS
* 🔥 Firewall

### Example

To deploy an e-commerce application, you may need:

* VPC
* Public & Private Subnets
* Internet Gateway
* Route Tables
* Security Groups
* EC2 Instances
* RDS Database
* S3 Bucket
* Load Balancer

➡️ All these resources together are called **Infrastructure**.

---

# 2️⃣ What is Infrastructure as Code (IaC)?

## Definition

**Infrastructure as Code (IaC)** is the process of creating, configuring, and managing infrastructure using code instead of manually creating resources through a cloud console.

### Without IaC

* Login to AWS Console
* Create VPC
* Create Subnets
* Create Security Groups
* Launch EC2
* Create RDS

### With IaC

```bash
terraform apply
```

Terraform automatically creates all the required infrastructure.

> **Simple Definition:**
> Infrastructure as Code (IaC) means managing infrastructure using code instead of manual processes.

---

# 3️⃣ Why IaC is Needed

Managing infrastructure manually becomes difficult as projects grow.

### Problems Without IaC

* ❌ Time-consuming
* ❌ Human errors
* ❌ Inconsistent environments
* ❌ Difficult to scale
* ❌ Hard to reproduce infrastructure
* ❌ No version control
* ❌ Difficult disaster recovery

### Why We Use IaC

* ✅ Automation
* ✅ Consistency
* ✅ Repeatability
* ✅ Faster Deployment
* ✅ Easy Scaling
* ✅ Version Control
* ✅ Easy Rollback

---

# 4️⃣ Problems with Manual Infrastructure

### Example Scenario

A company needs:

* 50 EC2 Instances
* 20 Security Groups
* 10 Databases
* 5 Load Balancers

If an engineer creates everything manually, it may result in:

* Long deployment time
* Human mistakes
* Incorrect configurations
* Different naming conventions
* Missing resources
* Difficult recovery

### Manual Workflow

```text
Developer
     │
     ▼
AWS Console
     │
Click → Click → Click
     │
     ▼
Infrastructure Created
```

### Drawbacks

* Slow
* Error-prone
* Not Repeatable
* Difficult to Maintain
* No Automation

---

# 5️⃣ Benefits of IaC

* 🚀 Automation
* 🎯 Consistency
* 📂 Version Control
* ⚡ Faster Deployment
* 🔄 Easy Rollback
* 📈 Scalability
* ✅ Reduced Human Errors
* ♻️ Reusability
* 👥 Team Collaboration

---

# 6️⃣ IaC Tools Comparison

| Tool               | Developed By | Cloud Support | Language                               | Best For                                   |
| ------------------ | ------------ | ------------- | -------------------------------------- | ------------------------------------------ |
| Terraform          | HashiCorp    | Multi-Cloud   | HCL                                    | Infrastructure Provisioning                |
| AWS CloudFormation | AWS          | AWS Only      | JSON / YAML                            | AWS Infrastructure                         |
| Ansible            | Red Hat      | Multi-Cloud   | YAML                                   | Configuration Management                   |
| Pulumi             | Pulumi       | Multi-Cloud   | Python, JavaScript, TypeScript, Go, C# | Infrastructure Using Programming Languages |

---

# 7️⃣ Terraform

## Definition

Terraform is an **Infrastructure as Code (IaC)** tool developed by **HashiCorp** that automates infrastructure provisioning and management using code.

### Features

* Open Source
* Multi-Cloud Support
* Declarative Language (HCL)
* State Management
* Modular Design
* Version Control Friendly

### Example

```bash
terraform apply
```

---

# 8️⃣ AWS CloudFormation

## Definition

AWS CloudFormation is AWS's native Infrastructure as Code service used to provision and manage AWS resources using **JSON** or **YAML** templates.

### Advantages

* Native AWS Service
* Deep AWS Integration
* Managed by AWS

### Limitation

* Works only with AWS.

---

# 9️⃣ Ansible

## Definition

Ansible is an automation tool mainly used for **configuration management**, application deployment, and orchestration.

### Common Tasks

* Install Docker
* Install Nginx
* Configure Servers
* Create Users
* Deploy Applications

### Example

```bash
ansible-playbook install-nginx.yml
```

---

# 🔟 Pulumi

## Definition

Pulumi is an Infrastructure as Code tool that allows developers to create infrastructure using programming languages such as:

* Python
* JavaScript
* TypeScript
* Go
* C#

### Example

```python
import pulumi
```

---

# 📊 Terraform vs CloudFormation vs Ansible vs Pulumi

| Feature          | Terraform                   | CloudFormation          | Ansible                  | Pulumi                                     |
| ---------------- | --------------------------- | ----------------------- | ------------------------ | ------------------------------------------ |
| Type             | IaC                         | IaC                     | Configuration Management | IaC                                        |
| Multi-Cloud      | ✅                           | ❌                       | ✅                        | ✅                                          |
| AWS Support      | ✅                           | ✅                       | ✅                        | ✅                                          |
| Azure Support    | ✅                           | ❌                       | ✅                        | ✅                                          |
| GCP Support      | ✅                           | ❌                       | ✅                        | ✅                                          |
| Language         | HCL                         | JSON / YAML             | YAML                     | Python, JS, TS, Go, C#                     |
| State Management | ✅                           | ✅                       | ❌                        | ✅                                          |
| Best Use         | Infrastructure Provisioning | AWS-only Infrastructure | Server Configuration     | Infrastructure Using Programming Languages |

---

# 🔄 Real-Time DevOps Workflow

```text
Developer
      │
      ▼
Git Repository
      │
      ▼
CI/CD Pipeline (Jenkins / GitHub Actions)
      │
      ▼
Terraform
      │
      ▼
AWS Cloud
      │
      ├── VPC
      ├── EC2
      ├── RDS
      ├── S3
      ├── Load Balancer
      └── Security Groups
      │
      ▼
Ansible
      │
      ├── Install Docker
      ├── Install Nginx
      ├── Configure Servers
      └── Deploy Applications
```

---

# 🎯 Interview Questions

1. What is Infrastructure?
2. What is Infrastructure as Code (IaC)?
3. Why is IaC important in DevOps?
4. What are the problems with manual infrastructure?
5. What are the benefits of IaC?
6. What is Terraform?
7. How is Terraform different from AWS CloudFormation?
8. What is Ansible mainly used for?
9. What is Pulumi?
10. Why is Terraform preferred in multi-cloud environments?

---

# 📌 Quick Revision

* **Infrastructure** → Resources required to run an application.
* **IaC** → Managing infrastructure using code instead of manual processes.
* **Terraform** → Multi-cloud Infrastructure as Code tool.
* **AWS CloudFormation** → AWS-native IaC service.
* **Ansible** → Configuration management and automation.
* **Pulumi** → Infrastructure as Code using programming languages.

---

## 📖 Next Module

➡️ **Module 2: Terraform Introduction**

* What is Terraform?
* Why Terraform?
* Features
* Advantages
* Disadvantages
* Terraform Architecture
* Terraform Workflow
* Declarative vs Imperative
* Mutable vs Immutable Infrastructure

---

⭐ **If you find these notes helpful, don't forget to star this repository!**
