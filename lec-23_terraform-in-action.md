## lec 23 – AWS + Terraform (Networking & State Basics)

### Subnets in AWS

Subnet:
- range of IPs inside a VPC
- always belongs to **one VPC**
- tied to **one availability zone**

Types:
- Public Subnet
  - connected to Internet Gateway (IGW)
  - instances can access internet
- Private Subnet
  - no direct IGW connection
  - used for backend services, DBs

Key idea:
- public/private depends on **route table**, not subnet name

---

### Terraform Dependencies (Important)

Implicit dependency:
- Terraform figures out order automatically
- happens when one resource **references another**

Example:
- subnet refers to VPC ID
- Terraform creates VPC first, then subnet
- no need to manually specify order

This is why Terraform is declarative.

---

### VPC & Network Configuration

VPC:
- isolated virtual network in AWS
- created with a CIDR block

CIDR block:
- defines IP range and size of network
- example: `10.0.0.0/16`
- larger CIDR → more IPs

Routing Table:
- controls where traffic goes
- example:
  - `0.0.0.0/0 → IGW` → public subnet
- route table decides internet access

---

### Terraform State Management

State file:
- `terraform.tfstate`
- stores:
  - what Terraform created
  - current infra state
- used to calculate changes

Problem:
- multiple people editing infra
- local state causes conflicts

Solution:
- remote state
- store state in:
  - S3 bucket
  - DynamoDB for locking
- avoids race conditions

---

### Terraform File Structure (Common Practice)

Common files:
- `main.tf`
  - main resources / providers
- `network.tf`
  - VPC, subnets, IGW, route tables
- `compute.tf`
  - EC2, security groups
- `variables.tf`
  - input variables
- `outputs.tf`
  - output values

File names don’t matter to Terraform,
they matter to **humans** for clarity.

---

### Types of IPs in AWS

Private IP:
- internal to VPC
- used for service-to-service communication

Public IP:
- reachable from internet
- changes when instance stops/starts

Elastic IP (EIP):
- static public IP
- tied to AWS account
- can be reassigned to instances

---

### EC2 Basics

EC2 instance:
- cannot exist without an AMI

AMI:
- template for OS
- example:
  - Ubuntu
  - Amazon Linux
- defines:
  - OS
  - base packages

AMI is mandatory for EC2 creation.

---

### Variables in Terraform

Why variables:
- avoid hardcoding values
- reuse configs across environments

Types:
- Input variables
  - passed via `.tfvars` or CLI
- Output variables
  - show useful info (IP, DNS, etc.)
- Local variables
  - used inside a config
  - improve readability

---

### Key Takeaways

- subnet behavior depends on routing
- Terraform handles dependencies automatically
- state file is critical
- use remote state in teams
- CIDR defines network size
- EC2 always needs an AMI
- variables make Terraform reusable
