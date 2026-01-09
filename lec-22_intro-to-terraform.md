## lec 22 – Terraform & Infrastructure as Code (IaC)

### What is Terraform

Terraform:
- open-source Infrastructure as Code (IaC) tool
- used to create, update, and delete infrastructure using code
- works with multiple cloud providers (AWS, Azure, GCP)

Key idea:
- infra is written as code, not created manually
- same way we manage application code

Key characteristics:
- platform agnostic (multi-cloud support)
- declarative → you define *what you want*, Terraform figures out *how*
- repeatable and automated

---

### Infrastructure as Code (IaC)

IaC:
- infrastructure defined using configuration files (`.tf`)
- avoids manual clicks on cloud consoles
- reduces human errors
- infra changes are version controlled (Git)

Benefits:
- consistency across environments
- easy rollback
- audit trail of infra changes

---

### Terraform Lifecycle Commands

Terraform follows a simple lifecycle:

#### terraform init
- initializes the working directory
- downloads required providers (AWS, Azure, etc.)
- sets up backend and modules
- locks provider versions

Run this **first**, always.

---

#### terraform plan
- compares:
  - current infrastructure (state)
  - desired infrastructure (code)
- shows what Terraform *will* do
- does NOT make changes
- used to review before applying

Think of it as a dry run.

---

#### terraform apply
- executes the plan
- creates / updates / deletes resources
- asks for confirmation before changes
- brings infra to desired state

---

#### terraform destroy
- deletes all resources defined in code
- cleans up infrastructure
- useful for labs, testing, cost control

---

### Why Use Terraform

Speed:
- infra created in minutes
- no manual setup

Consistency:
- same code → same infra every time

Version control:
- `.tf` files stored in Git
- infra changes are trackable
- easy rollback

Cost efficiency:
- destroy unused resources easily
- avoids forgotten running infra

---

### Supporting Tools (Ecosystem)

Configuration management:
- Ansible
- Puppet
- Chef
Used *after* infra is created (software setup)

Server templating:
- Docker
- Vagrant
Used for creating environments / images

Terraform’s role:
- infra provisioning
- not application configuration

---

### Practical Example (Discussed in Class)

EC2 creation using Terraform:
- define EC2 resource in `.tf` file
- specify:
  - instance type
  - AMI
  - region
- run:
  - `terraform init`
  - `terraform plan`
  - `terraform apply`

Terraform state:
- tracks real infra vs code
- stored in state file
- used to detect changes

---

### Key Takeaways

- Terraform = infra automation tool
- IaC brings software engineering practices to infra
- terraform init → plan → apply → destroy
- code-driven infra is:
  - faster
  - safer
  - reproducible
- Terraform is core to modern DevOps workflows
