## lec 20 – GitHub Actions + Docker (Java Maven Project)

### Git Repository Setup

Repo setup:
- create repo on GitHub first
- clone locally using SSH / HTTPS
- make sure project structure is correct:
  - `src/`
  - `pom.xml`

Basic git flow:
- `git add .`
- `git commit -m "message"`
- `git push`
- local changes sync to remote repo

---

### GitHub Actions Overview

GitHub Actions:
- CI/CD tool built into GitHub
- workflows written in YAML
- stored inside `.github/workflows/`

Triggers:
- push
- pull request
- manual trigger (workflow_dispatch)

YAML caution:
- indentation matters
- spacing errors break workflows
- copy–paste preferred over manual typing

Multi-job workflows:
- multiple jobs can run in parallel
- jobs can run on:
  - ubuntu
  - windows
  - macOS

---

### Maven Build in CI

Maven basics:
- `pom.xml` defines:
  - dependencies
  - plugins
  - build config

CI build steps:
- checkout code
- set up JDK
- run Maven commands

Common command:
- `mvn clean package`
- compiles code
- runs tests
- produces JAR / WAR

GitHub provides ready-made Maven CI templates.

---

### Docker Integration

Docker setup:
- Dockerfile stored with project code
- Docker setup is independent of Java
- Docker used for containerizing the built app

Docker Hub:
- used to store Docker images
- images are pushed from CI pipeline

Important rule:
- NEVER hardcode credentials

---

### Secrets Management

GitHub Secrets:
- used to store sensitive data
- examples:
  - Docker Hub username
  - Docker Hub password / token

Usage:
- secrets referenced inside workflow
- credentials injected at runtime
- secure by default

---

### Building & Pushing Docker Images

CI flow:
- build Java app using Maven
- build Docker image
- tag image correctly
- login to Docker Hub
- push image

Image tagging:
- must match Docker Hub username
- example: `username/app-name:tag`

---

### Testing in CI

Basic testing:
- Maven tests during build
- ensures build correctness

Docker testing:
- container can be run for basic validation
- advanced tests require proper test code

---

### Security & Code Quality (Advanced)

Security scans:
- SAST → static code analysis
- DAST → runtime security testing
- Docker image scanning using Trivy

Linting & static analysis:
- Checkstyle
- CodeQL
- helps maintain code quality

---

### Key Takeaways

- GitHub Actions automates CI/CD
- YAML syntax must be precise
- Maven handles Java build lifecycle
- Docker packages application
- secrets must be stored securely
- CI pipeline can:
  - build
  - test
  - scan
  - publish images
- foundation for real-world DevOps pipelines
