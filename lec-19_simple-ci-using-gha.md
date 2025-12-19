GitHub Actions:
- built-in CI/CD tool in GitHub
- automate build, test, and deploy workflows
- everything lives inside the repo

Why GitHub Actions:
- no external CI tool needed
- workflows triggered automatically
- supports Linux, Windows, macOS runners

---

### Setting up Git Repository

Before Actions:
- create a GitHub repository
- clone repo locally (SSH / HTTPS)
- add project code
- for Java → `pom.xml` is required

Command:
- `git clone <repo-url>`

---

### GitHub Actions Basics

Workflow:
- defined using YAML
- stored in `.github/workflows/`
- one repo can have multiple workflows

Workflow structure:
- `name` → workflow name
- `on` → trigger (push, pull_request, etc.)
- `jobs` → what runs
- `steps` → actions / commands inside job

Trigger example:
- run workflow on push to `main` branch

---

### Jobs & Runners

Jobs:
- collection of steps
- run independently unless linked

`runs-on`:
- defines machine type
- common values:
  - `ubuntu-latest` (most used)
  - `windows-latest`
  - `macos-latest`

Ubuntu preferred:
- faster
- more tooling support
- cheaper

---

### Actions & Steps

Actions:
- reusable components from marketplace
- example:
  - `actions/checkout` → fetch repo code
  - `actions/setup-java` → install JDK

Steps:
- either:
  - `uses` → predefined action
  - `run` → shell command

---

### Maven with GitHub Actions

Typical Java CI flow:
- checkout code
- set up JDK
- run Maven build

Maven build:
- `mvn package`
- compiles code
- runs tests
- creates `.jar` / `.war`

Caching:
- cache Maven dependencies
- reduces build time
- saves cost

---

### Workflow Execution

What happens:
- push code
- workflow triggered
- runner starts
- steps execute one by one
- logs generated for each step

Logs:
- very important for debugging
- every step has detailed output

---

### Cost Management (Important)

GitHub Actions cost depends on:
- runner time
- OS used
- workflow duration

Best practices:
- keep workflows short
- avoid unnecessary steps
- ensure jobs stop after completion
- don’t leave resources running

---

### Common Errors & Debugging

YAML issues:
- indentation mistakes
- wrong syntax
- missing fields

Version issues:
- incorrect JDK version
- incompatible Maven version

Permission issues:
- action doesn’t have access
- repo permissions not set properly

Always:
- read logs carefully
- errors usually very descriptive

---

### Key Takeaways

- GitHub Actions enables CI/CD inside GitHub
- workflows are YAML based
- triggers define when pipeline runs
- jobs run on virtual machines
- Maven integrates smoothly for Java
- logs + syntax correctness are critical
- good workflow design saves cost
