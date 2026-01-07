## lec 21 – CI/CD with Kubernetes (End-to-End Flow)

### CI/CD Overview

CI (Continuous Integration):
- automate merging of code changes
- frequent commits to main branch
- automated builds and tests
- goal → main branch always deployable

CD (Continuous Deployment):
- extends CI till deployment
- automates app deployment to environments
- focuses on zero downtime releases
- involves infra + application deployment

Key difference:
- CI → code integration + validation
- CD → delivery and deployment of validated code

---

### Kubernetes Setup for CI/CD

Cluster requirement:
- minimum 1-node Kubernetes cluster
- used for deploying applications

Ways to set up:
- VirtualBox + Vagrant
- Vagrant scripts automate VM creation
- easy copy–paste setup for lab environments

Shortcut approach:
- use pre-built VM / AMI with Kubernetes installed
- saves setup time
- commonly used in demos and labs

---

### GitHub Actions in CI/CD

GitHub Actions:
- CI/CD tool integrated into GitHub
- workflows defined using YAML
- handles build, test, deploy

Used for:
- CI pipeline (build + test)
- CD pipeline (deploy to Kubernetes)

---

### Custom / Self-Hosted Runners

Why custom runners:
- GitHub-hosted runners may not have:
  - kubectl
  - Docker
  - cluster access
- deployment needs direct access to infra

Self-hosted runner:
- your own machine acts as runner
- Linux preferred
- registered with GitHub repo/org

Setup steps:
- download runner package
- run `config.sh`
- register with repo
- assign labels
- runner listens for jobs

Once registered:
- GitHub sends jobs to your machine
- used mainly for CD steps

---

### CI/CD Flow with Kubernetes

Typical flow:
1. developer pushes code
2. GitHub Actions CI runs:
   - build
   - test
   - package
3. image built and pushed
4. CD pipeline triggers
5. deployment applied to Kubernetes cluster

CI and CD:
- often kept separate
- clearer responsibility
- easier debugging

---

### Testing Strategy

Testing stages:
- SIT (System Integration Testing)
- performance testing
- security testing

Automation:
- tests automated as part of pipeline
- reduces human error
- ensures consistency

---

### Project & Evaluation Notes

Team projects:
- CI/CD implemented as group
- presentations done as team

Important:
- every individual must understand project
- questions asked individually
- personal contribution matters

---

### Practical Takeaways

- CI/CD is core DevOps practice
- Kubernetes is deployment target
- GitHub Actions drives automation
- self-hosted runners enable real deployments
- CI ≠ CD (keep them separate)
- automation improves reliability and speed
